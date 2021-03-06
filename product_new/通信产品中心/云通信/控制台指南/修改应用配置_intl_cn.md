## 操作场景
为方便对应用进行管理，云通信 IM 为您提供了可以界面操作的控制台。
登录云通信 IM [控制台](https://console.cloud.tencent.com/avc)， 在【应用列表】页，单击对应 SDKAppID 的右侧的【应用配置】，进入应用详情页，这里可以对应用进行基础配置的管理、帐号体系集成管理和功能配置管理等。下文将对控制台【应用配置】进行详细说明：
![](https://main.qcloudimg.com/raw/8948c71a8b8da5a9a11372c66e5d0715.png)
## 操作指南
### 基础配置
基础配置可以为应用配置基础的信息。详细操作如下：
![](https://main.qcloudimg.com/raw/aadc211502d6ace3dd1524ad605dfecf.png)

#### 应用信息
- **说明**
控制台【应用信息】可以为创建的应用修改应用的基础信息。
- **操作**
单击【应用信息】同行的【编辑】，进入应用设置的编辑状态，可以修改【应用名称】、【应用类型】以及【应用简介】，修改完成后单击【保存】即可。


#### 应用平台
- **说明**
选择应用所属的平台。
- **操作**
单击【应用平台】同行的【编辑】，进入应用平台的编辑状态，勾选对应的平台后单击【保存】即可。
![](https://main.qcloudimg.com/raw/a40bfc6fa3f60e2aa351e218613fc663.png)


#### 帐号体系集成
- **说明**
【帐号体系集成】可以为应用集成帐号所需信息，可以进行添加管理员帐号和下载公私钥操作。
- **操作**
 <span id="AddAdmin"></span>
 - **添加管理员**
单击【帐号体系集成】同行的【编辑】，输入管理员帐号，如需添加多个管理员，可单击【+添加管理员】输入管理员帐号，单击【保存】即可。
![](https://main.qcloudimg.com/raw/651b73f62d02f3662fb10b28d8b38bb9.png)
 - **下载公私钥**
添加完管理员后，在【帐号体系集成】下即可看到【下载公私钥】，单击【下载公私钥】保存到本地计算机即可。
![](https://main.qcloudimg.com/raw/f1852b9e26cb51a39708c4c1c7a0078c.png)


### 功能配置
功能配置可以开通一些特色功能。界面如下：
![](https://main.qcloudimg.com/raw/5d247a5f023a4f77f20036b640587185.png)
   
#### 	多端登录
- **说明**
  可以配置 Windows、iOS、Android 及 Web 端的登录状态。
- **操作**
  单击【多端在线】同行的【编辑】，选择单端登录、双端登录、三端登录或多端登录后，单击【保存】，您可以将鼠标移动至“?”处，查看配置说明。
	
#### Web 端登录支持
- **说明**
可以配置 Web 端实例同时在线个数。
- **操作**
单击【多终端】同行的【编辑】，选择在线个数，单击【保存】即可。


#### 消息
- **说明**
可以开启客户端拉取单聊消息漫游、消息推送、单聊消息检验关系链，生效时间为5分钟。
- **操作**
单击【消息】同行的【编辑】，将需要开启的消息类型对应的按钮置为<img src="https://main.qcloudimg.com/raw/062b909f41618b918f0a869be3f2f93c.png"  style="margin:0;">，单击【保存】即可。如果需要关闭，则将需要关闭的消息类型对应的按钮置为<img src="https://main.qcloudimg.com/raw/1e8eda9846a0b665510e8a5732a7f18a.png"  style="margin:0;">，单击【保存】即可。

#### 消息漫游时长
- **说明**
     提供单聊及群聊消息支持文字及自定义消息漫游时长延长服务。
- **操作**
     在消息漫游下拉框中选择希望延长的时间后，单击【保存】，请仔细阅读弹出的对话框后，单击【确定】实现配置。
#### 用户资料
- **说明**
如果现有用户资料字段不能满足您的需求，可以自定义用户资料。
- **操作**
在【用户资料】下，单击【+新增自定义字段】输入字段相关信息，保存即可。

#### 好友自定义字段
- **说明**
如果现有好友字段不能满足您的需求，可以自定义用户资料。
- **操作**
在【好友自定义字段】下，单击【+新增自定义字段】输入字段相关信息，保存即可。

#### 群成员自定义字段
- **说明**
如果现有群成员字段不能满足您的需求，可以自定义用户资料。
- **操作**
在【群成员自定义字段】下，单击【+新增自定义字段】填写字段名称，选择群组型态及权限，单击【确定添加】即可。

#### 群维度自定义字段
- **说明**
如果现有群维度字段不能满足您的需求，可以自定义用户资料。
- **操作**
在【群维度自定义字段】下，单击【+新增自定义字段】填写字段名称，选择群组型态及权限，单击【确定添加】即可。

### Crash 配置
腾讯云的 Crash 是腾讯 Bugly 互通的一款产品，它为移动开发者提供专业的异常上报和运营统计，帮助开发者快速发现并解决异常，同时掌握产品运营动态，及时跟进用户反馈，如果不需要使用产品可以选择不开通。
Crash 配置指南：
1. 单击【Carsh】。
2. 跳转到 Bugly 首页，可以新建应用或者直接设置您的应用错误上报信息。
3. 可以参考 [Bugly 文档中心](https://bugly.qq.com/docs/) 设置您对应的信息。


### 开发辅助工具
开发者辅助工具只需要填写 UserID 和私钥就可以快速生成一个 UserSig 用来测试，需要注意的是私钥必须是您自己在基础配置中帐号体系集成下载的私钥，且私钥必须为完整的内容，详细操作可参考 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1027/31308)。
![](https://main.qcloudimg.com/raw/5e366ad4a30da4ad1ba728d33360f64d.png)

