申请域名型证书，可以通过以下方式验证域名的所有权：

### 1. 手动 DNS 验证
通过解析指定的 DNS 记录验证您的域名所有权，指定如`主机记录 –> TXT记录类型 –> 记录值`的解析格式。

例如为申请证书的域名 www.domain.com 添加一条记录类型为TXT的DNS记录，`www.domain.com –> TXT –> 201704262209564gw0...hj37i4xai8m7uii2a23l`：

![](https://main.qcloudimg.com/raw/88ddec5704c06a811f789bcde7d6fab9.png)

以腾讯云云解析平台为例说明如何进行操作：

#### 1.1 添加域名

单击【添加解析】，在弹窗内输入您要解析域名的主域名`domain.com`，并点【确定】

![](https://main.qcloudimg.com/raw/96822fe8c2b7b53870a0488f69db557d.png)

#### 1.2 添加解析记录

域名添加完成后，单击右侧的【解析】进入域名解析页面。  

![](https://main.qcloudimg.com/raw/63910230c0120875d5c730583338699d.png)

单击【添加记录】  

![](https://main.qcloudimg.com/raw/f933ee8ef54a53496cb60adb0f3fb9f0.png)

#### 1.3 完成指定的 TXT 记录添加

TXT 记录是对域名进行标识和说明的一种方式：

- **记录类型选择为 TXT**
- 主机记录根据证书详情填入，如：`_dnsauth`
- 线路类型选择默认
- 记录值为系统提供的文本内容，此处为`201712270743...t5bfctnq`，注意**记录值须完整填写**
- TTL选择默认值 600 秒即可

![](https://main.qcloudimg.com/raw/a54456bbbac2ef3b99b38e526c1d6be2.png)

解析添加成功后如下：
![](https://main.qcloudimg.com/raw/0e4c416a842754b43c84668518c16200.png)

www.domain.com TXT 记录值的系统会定时检查，若能检测到并且与指定的值匹配，即可完成域名所有权验证。

### 2. 自动DNS验证
> 注：仅限使用云解析的域名

如果申请证书的域名已经在云解析平台进行解析，可以选择自动验证。
系统为将为该域名自动添加指定的DNS解析记录，记录被检测匹配成功，完成域名所有权验证后，该记录将自动清除。

### 3. 文件验证

#### 3.1 指定目录下创建文件
按指定文件目录、文件名、文件内容新增文件，例如

| 文件目录| 文件名 |文件内容 |
|---------|---------|---------|
| /.well-known/pki-validation | fileauth.txt | 201608241742072yvt8bxp9jv0ycginrnnebwgy1nvwgvxtssucy39w7b20nelfa |

如果申请文件验证的域名是`example.www.domain.com`，那么进行验证访问的链接地址是 `http://example.www.domain.com/.well-known/pki-validation/fileauth.txt` 或者 `https://example.www.domain.com/.well-known/pki-validation/fileauth.txt`  

> 对于 www 开头的二级域名，如：`www.domain.com`，在对该域名本身添加文件验证信息之外，还需增加对其主域名`domain.com`的文件验证，验证值与验证方法与该二级域名文件验证相同。  

如果申请文件验证的域名是泛域名`*.domain.com`，那么进行验证访问的链接地址是 `http://domain.com/.well-known/pki-validation/fileauth.txt` 或者 `https://domain.com/.well-known/pki-validation/fileauth.txt`

访问链接可获取到内容为`201608241742072yvt8bxp9jv0ycginrnnebwgy1nvwgvxtssucy39w7b20nelfa`。

> http 和 https 访问支持任意一个均可；
> 文件验证不支持任何形式的跳转，需要直接响应 200 状态码和文件内容。

#### 3.2 等待审核
建立完成文件后，请耐心等待 CA 机构扫描审核。证书颁发完成后，文件和目录即可清除。

#### 3.3 Window 系统不支持创建/.well-known 目录问题
在 Windows 下无法通过`右键=>新建`命令来创建以点开头的文件和文件夹，例如`.log`，会提示必须输入文件名。
可以通过命令行来创建：

新建文件夹
```
mkdir .well-known
```
