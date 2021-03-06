## 即时通信 IM 配置变更需求工单的提交方式
1. 登录 [即时通信 IM 工单页面](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1)。
2. 选择【选择常见问题】为【申请配置审批】。
3. 根据 [即时通信 IM 配置变更需求工单模版](https://intl.cloud.tencent.com/document/product/1027/31416#.E4.BA.91.E9.80.9A.E4.BF.A1-im-.E9.85.8D.E7.BD.AE.E5.8F.98.E6.9B.B4.E9.9C.80.E6.B1.82.E5.B7.A5.E5.8D.95.E6.A8.A1.E7.89.88) 中对应模版填写配置变更所需信息，填写手机号等联系方式。
4. 单击【提交工单】。
 >工单提交后，我们将在一个工作日内处理完毕。

## 即时通信 IM 配置变更需求工单模版

### 群组不同优先级的消息的频率控制
> 配置变更类型：群组不同优先级的消息的频率控制
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态：// 要修改哪种群组形态，例如 Private, ChatRoom 等
> 聊天类消息频率控制：// 最多 N 条/秒
> 点赞类消息频率控制：// 最多 M 条/秒
> 成员变更通知频率控制：// 最多 K 条/秒

### 群下行消息带自定义字段
> 配置变更类型：群下行消息带自定义字段
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态：// 需要修改哪种群组形态，例如 Private, ChatRoom 等
> 自定义字段类型：//群维度自定义字段、群成员维度自定义字段或用户资料自定义字段
> 需要携带的自定义字段名称：// 已经在控制台添加的自定义字段的名称，支持携带多个字段，需要与自定义字段类型对应

### 新增群组形态
> 配置变更类型：新增群组形态
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态名称： // 新增的群组形态名称，不能为默认的产品形态，如 Private,Public， ChatRoom，AVChatRoom 等
> 参考的群组形态：// 要参考的群组形态，如 Private，Public 等
> 在参考的群组形态基础上修改的特性： // 详细说明在参考的群组形态基础上需要变更的特性


### 修改群组形态
> 配置变更类型：修改群组形态
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态名称： //群组形态名称，如 Private, ChatRoom 等
> 需要修改的特性： // 详细说明需要变更的特性


### 定期踢掉群内不在线成员
> 配置变更类型：定期踢掉群内不在线成员
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态名称： //群组形态名称，如 Private, ChatRoom 等
> 是否允许定期踢掉不在线成员：// 


### 定期计算群内在线成员数量
> 配置变更类型：定期计算群内在线成员数量
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态名称： //群组形态名称，如 Private, ChatRoom 等
> 是否定期计算在线成员数量：// 是/否

### 自动回收群组
> 配置变更类型：自动回收群组
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 群组形态名称： //群组形态名称，如 Private, ChatRoom 等
> 群组回收时间（单位为秒）：// 该时间内不活跃的群组将会被回收(群组不活跃是指群组中既没人发言，也没有成员变更)

### 修改每日创建群组配额
> 配置变更类型：修改每日创建群组配额
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 每天最多新增群个数：// 仅为新增群组数，创建之后销毁不计入总数

### REST API 调用频率调整
> 配置变更类型：REST API 调用频率调整
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> ServiceName/Command: // 填请求的 REST API 名称, 如 group_svc/get_group_list
> 预期最大频率: // 最多 XXX 次每分钟，默认6000次每分钟


### HTTPS 证书签发
> 配置变更类型：HTTPS 证书签发
> SDKAppID：// 请在这里填写您的 App 在即时通信 IM 中的 SDKAppID
> 回调域名: //  请在这里填写您的回调地址的域名，如`https://www.example.com`
