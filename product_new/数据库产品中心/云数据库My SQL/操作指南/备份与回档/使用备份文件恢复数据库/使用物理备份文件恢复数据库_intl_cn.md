## 操作场景
本文为您介绍使用下载到本地的物理备份文件在其他主机上恢复数据库的操作。

## 操作步骤
### 下载备份文件
具体步骤请参见：[备份下载](http://intl.cloud.tencent.com/document/product/236/7274)

### 解包备份文件
1. 由于备份文件先经过 qpress 压缩，后经过 xbstream 打包（xbstream 为 Percona 的一种打包/解包工具），所以下载备份文件后，应该先用 xbstream 将其解包。xbstream 工具可以通过 Percona XtraBackup 官网下载或者直接下载二进制包。
 - [Percona XtraBackup 官网下载安装](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)
 请选择 Percona XtraBackup 2.4.6 及以上的版本，安装介绍请参见 [官网文档](https://www.percona.com/doc/percona-xtrabackup/2.4/installation/yum_repo.html)。
 - 二进制包安装
通过 [XtraBackup-download](https://www.percona.com/downloads/Percona-XtraBackup-2.4/Percona-XtraBackup-2.4.13/binary/tarball/percona-xtrabackup-2.4.13-Linux-x86_64.libgcrypt145.tar.gz)  下载相应操作系统版本的 XtraBackup 二进制包。
>?目前 Windows 操作系统不支持 XtraBackup工具，仅 Linux 操作系统支持 XtraBackup工具。
2. 安装好 XtraBackup 之后，使用 xbstream 命令将备份文件解包到目标目录。
```
xbstream -x -C /data < ~/test.xb
```
解包结果如下图所示：
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

### 解压备份文件
因备份文件经过 quicklz 算法压缩，所以需要进行解压。需 [下载 qpress 工具](http://www.quicklz.com/) ，下载之后通过以下命令解出 qpress 二进制文件。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
使用 qpress 命令将目标目录下所有以`.qp`结尾的文件都解压出来。
```
xtrabackup --decompress --target-dir=/data
```
>?
>- `xtrabackup --decompress`会调用 qpress 工具，使用`--decompress`参数前需要安装 qpress。
>- Percona Xtrabackup 在2.4.6及以上版本中才支持`--remove-original`选项。
>- `xtrabackup`默认在解压缩时不删除原始的压缩文件，若想解压完删除原始的压缩文件，可在上面的命令中加上`--remove-original`参数。
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

###  Prepare 备份文件
备份解压出来之后，需要执行以下命令进行 apply log 操作。
```
xtrabackup --prepare  --target-dir=/data
```
执行后如果结果中包含以下输出，则表示 prepare 成功。
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	

### 修改配置文件
由于存在的版本问题，请将解压文件 backup-my.cnf 中以下参数注释掉。
- innodb_checksum_algorithm
- innodb_log_checksum_algorithm
- innodb_fast_checksum
- innodb_page_size 
- innodb_log_block_size
- redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### 修改文件属性
修改文件属性，并检查文件所属为 mysql 用户。
```
chown -R mysql:mysql /data
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

### 启动 mysqld 进程并登录验证
1. 启动 mysqld 进程。
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. 客户端登录 mysql 验证。
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

>!
>- 恢复完成后，表 mysql.user 中是不包含 TencentDB 中创建的用户，需要新建。
>- 新建用户前请执行以下 SQL：
```
delete from mysql.db where user<>'root' and char_length(user)>0;
delete from mysql.tables_priv where user<>'root' and char_length(user)>0;
flush privileges;
```
