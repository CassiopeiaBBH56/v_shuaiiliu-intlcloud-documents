## 下载与安装

### 相关资源
- 对象存储 COS 的 XML C++ SDK 源码下载地址：[ XML C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5 "cos-cpp-sdk-v5下载地址")。
- 示例 Demo 下载地址：[ COS XML C++ SDK 示例](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp "Cpp SDK 参考")。

### 环境依赖
- 依赖静态库：jsoncpp boost_system boost_thread Poco （在 lib 文件夹下）。
- 依赖动态库：ssl crypto rt z（需要安装）。
SDK 中提供了 JsonCpp 的库以及头文件。若您想要自行安装，请先按照以下步骤安装库并编译完成后，替换 SDK 中相应的库和头文件即可。若以上库已安装到系统，也可删除 SDK 中相应的库和头文件。

### 安装 SDK
#### 1. 安装 CMake 工具
```shell
yum install -y gcc gcc-c++ make automake
//安装 gcc 等必备程序包（已安装则略过此步）
yum install -y wget

// cmake 版本要大于3.5
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -zxvf cmake-3.5.2.tar.gz
cd cmake-3.5.2
./bootstrap --prefix=/usr
gmake
gmake install
```

####  2. 安装 Boost 的库和头文件
```java
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#Boost 库被安装在 /usr/local/lib 目录下
```

#### 3. 安装 OpenSSL
**方式一**
```shell
yum install openssl openssl-devel
```

**方式二**

```shell
wget https://www.openssl.org/source/openssl-1.0.1t.tar.gz  
tar -xzvf ./openssl-1.0.1t.tar.gz
cd openssl-1.0.1t/
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl

cd /usr/local/
ln -s ssl openssl
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig

# 添加头文件/库文件查找路径(可以写入到~/.bashrc中)
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. 安装 Poco 的库和头文件
从 [Poco 官网](https://pocoproject.org/download.html) 获取并安装 Poco 的库和头文件（下载 complete 版本）。
```shell
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```

>?您可以通过修改 `CMakeList.txt` 文件，指定本地 Boost 头文件路径，修改如下语句： 
```
SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
```

#### 5. 编译 COS CPP SDK 
下载 [XML C++ SDK 源码](https://github.com/tencentyun/cos-cpp-sdk-v5) 集成到您的开发环境，然后执行以下命令：
```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

>?[示例 Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp) 里面有常见 API 的例子。生成的 cos_demo 可以直接运行，生成的静态库名称为：libcossdk.a。生成的 libcossdk.a 放到您自己的工程里 lib 路径下，include 目录拷贝到自己的工程的 include 路径下。

## 开始使用
下面为您介绍如何使用 COS C++ SDK 完成一个基础操作，如初始化客户端、创建存储桶、查询存储桶列表、上传对象、查询对象列表、下载对象和删除对象。

>?关于文章中出现的 SecretId、SecretKey、Bucket 等名称的含义和获取方式请参阅 [COS 术语信息](https://intl.cloud.tencent.com/document/product/436/18507)。

### 初始化
配置文件各字段介绍：
```
// V5.4.3 版本之前的 SDK 配置文件请使用"AccessKey"
"SecretId":"COS_SECRETID", 
"SecretKey":"COS_SECRETKEY",

// COS 地域，地域及简称请参阅 https://intl.cloud.tencent.com/document/product/436/6224 
"Region":"Region",

// 签名超时时间, 单位：s    
"SignExpiredTime":360, 

// connect 超时时间, 单位：ms
"ConnectTimeoutInms":6000,

// http 超时时间, 单位：ms 
"HttpTimeoutInms":60000,  

// 上传文件分块大小，范围：1 MB~5 GB, 默认为 1 MB  
"UploadPartSize":1048576,  

// 单文件分块上传线程池大小       
"UploadThreadPoolSize":5, 

// 下载文件分片大小   
"DownloadSliceSize":4194304, 

// 单文件下载线程池大小 
"DownloadThreadPoolSize":5,   

// 异步上传下载线程池大小 
"AsynThreadPoolSize":2, 

// 日志输出类型，0：不输出，1：输出到屏幕，2：输出到 syslog   
"LogoutType":1,       

// 日志级别，1：ERR，2：WARN，3：INFO，4：DBG     
"LogLevel":3,                 
```

### 创建存储桶

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 指定配置文件路径，初始化 CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 构造创建存储桶的请求
    std::string bucket_name = "examplebucket-1250000000"; // Bucket名称
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    // 3. 调用创建存储桶接口
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. 处理调用结果
    if (result.IsSucc()) {
        // 创建成功
    } else {
        // 创建存储桶失败，可以调用 CosResult 的成员函数输出错误信息，如 requestID 等
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### 查询存储桶列表
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 指定配置文件路径，初始化 CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 构造上传文件的请求
    qcloud_cos::GetServiceReq req;
    qcloud_cos::GetServiceResp resp;
    qcloud_cos::CosResult result = cos.GetService(req, &resp);
    
    // 3. 获取响应信息
    const qcloud_cos::Owner& owner = resp.GetOwner();
    const std::vector<qcloud_cos::Bucket>& buckets = resp.GetBuckets();
    std::cout << "owner.m_id=" << owner.m_id << ", owner.display_name=" << owner.m_display_name << std::endl;
    
    for (std::vector<qcloud_cos::Bucket>::const_iterator itr = buckets.begin(); itr != buckets.end(); ++itr) {
        const qcloud_cos::Bucket& bucket = *itr;
        std::cout << "Bucket name=" << bucket.m_name << ", location="
            << bucket.m_location << ", create_date=" << bucket.m_create_date << std::endl;
    }
    
    // 4. 处理调用结果
    if (result.IsSucc()) {
        // 上传文件成功
    } else {
        // 上传文件失败，可以调用 CosResult 的成员函数输出错误信息，比如 requestID 等
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### 上传对象
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 指定配置文件路径，初始化 CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 构造上传文件的请求
    std::string bucket_name = "examplebucket-1250000000"; // 上传的目的Bucket名称
    std::string object_name = "exampleobject"; //exampleobject 即为对象键（Key），是对象在存储桶中的唯一标识。例如，在对象的访问域名 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg 中，对象键为 doc/pic.jpg。
    // request 的构造函数中需要传入本地文件路径
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA")； // 调用 Set 方法设置元数据等
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. 调用上传文件接口
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. 处理调用结果
    if (result.IsSucc()) {
        // 上传文件成功
    } else {
        // 上传文件失败，可以调用 CosResult 的成员函数输出错误信息，比如 requestID 等
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### 查询对象列表
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 指定配置文件路径，初始化 CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 构造创建存储桶的请求
    std::string bucket_name = "examplebucket-1250000000"; // 上传的目的Bucket名称
    qcloud_cos::GetBucketReq req(bucket_name);
    qcloud_cos::GetBucketResp resp;
    qcloud_cos::CosResult result = cos.GetBucket(req, &resp);   
    
    std::vector<qcloud_cos::Content> cotents = resp.GetContents();
    for (std::vector<qcloud_cos::Content>::const_iterator itr = cotents.begin(); itr != cotents.end(); ++itr) {
    	const qcloud_cos::Content& content = *itr;
        std::cout << "key name=" << content.m_key << ", lastmodified ="
            << content.m_last_modified << ", size=" << content.m_size << std::endl;
    }
    
    // 3. 处理调用结果
    if (result.IsSucc()) {
        // 上传文件成功
    } else {
        // 上传文件失败，可以调用 CosResult 的成员函数输出错误信息，比如requestID等
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### 下载对象
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 指定配置文件路径，初始化 CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 构造创建存储桶的请求
    std::string bucket_name = "examplebucket-1250000000"; // 上传的目的Bucket名称
    std::string object_name = "exampleobject"; // exampleobject 即为对象键（Key），是对象在存储桶中的唯一标识。例如，在对象的访问域名 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg 中，对象键为 doc/pic.jpg。
    std::string local_path = "/tmp/exampleobject";
    // request 需要提供 appid、bucketname、object,以及本地的路径（包含文件名）
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. 调用创建存储桶接口
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. 处理调用结果
    if (result.IsSucc()) {
        // 下载文件成功
    } else {
        // 下载文件失败，可以调用 CosResult 的成员函数输出错误信息，如 requestID 等
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### 删除对象
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 指定配置文件路径，初始化 CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 构造创建存储桶的请求
    std::string bucket_name = "examplebucket-1250000000"; // 上传的目标 Bucket 名称
    std::string object_name = "exampleobject"; // exampleobject 即为对象键（Key），是对象在存储桶中的唯一标识。例如，在对象的访问域名 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg 中，对象键为 doc/pic.jpg。
    // 3. 调用创建存储桶接口
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. 处理调用结果
    if (result.IsSucc()) {
        // 下载文件成功
    } else {
        // 下载文件失败，可以调用 CosResult 的成员函数输出错误信息，如 requestID 等
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```
