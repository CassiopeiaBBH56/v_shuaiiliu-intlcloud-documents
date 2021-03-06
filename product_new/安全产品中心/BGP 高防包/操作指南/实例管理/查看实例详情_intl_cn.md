## 基本信息
登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP 高防包】>【防护配置】，从实例下拉菜单中选择目标实例，在【服务包信息】区域即可查看该实例的基本信息。
![](https://main.qcloudimg.com/raw/dd5af2fd4bc4482b7a4625302b33be11.png)

### 服务包名
该 BGP 高防包实例的名称，用于辨识与管理 BGP 高防包实例。长度为1 - 20个字符，不限制字符类型。资源名称由用户根据实际业务需求自定义设置，具体操作请参考 [设置资源名称](https://intl.cloud.tencent.com/document/product/1029/31755)。

### 所在地区
 [购买 BGP 高防包](https://intl.cloud.tencent.com/document/product/1029/31748) 时选择的【地域】。

### 绑定 IP
该 BGP 高防包实例所防护业务的实际 IP。

### 保底防护峰值
该 BGP 高防包实例的保底防护带宽能力，即 [购买](https://intl.cloud.tencent.com/document/product/1029/31748) 时选择的【保底防护峰值】。若未开启弹性防护，则保底防护峰值为高防服务实例的最高防护峰值。

### 当前状态
BGP 高防包实例当前的使用状态。状态包括运行中，清洗中以及封堵中等。

### 到期时间
根据 [购买](https://intl.cloud.tencent.com/document/product/1029/31748) 时选择的【购买时长】以及具体的提支付购买订单的具体时间计算所得，精确到秒级。腾讯云会在此时间前的第7天，通过站内信、短信及邮件的方式向腾讯云账号的创建者以及所有协作者推送服务即将到期并提醒及时续费的信息。

## 弹性防护信息
登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP 高防包】>【防护配置】，从实例下拉菜单中选择目标实例，在【弹性防护】区域即可查看该实例的弹性防护信息。
![](https://main.qcloudimg.com/raw/eae8c95abe37a189eb9e6dcb4014b4ef.png)

### 当前状态
表示弹性防护是否开启。若 [购买 BGP 高防包实例](https://intl.cloud.tencent.com/document/product/1029/31748) 时未开启弹性防护，用户可在使用过程中自助开启，具体操作请参见 [配置弹性防护](https://intl.cloud.tencent.com/document/product/1029/31756)。

### 弹性峰值
该 BGP 高防包实例的最大弹性防护带宽能力。用户可以根据自身业务需求，随时 [调整弹性防护峰值](https://intl.cloud.tencent.com/document/product/1029/31756)。
>仅当弹性防护已开启时，该参数项才可见。

## DDoS 防护
登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/overview)，选择【BGP 高防包】>【防护配置】，从实例下拉菜单中选择目标实例，在【DDoS 防护】区域即可查看该实例的 DDoS 防护策略信息。
![](https://main.qcloudimg.com/raw/2bc835ded4fc3d1a629db69d69b9e5ea.png)
### 防护状态
表示 DDoS 防护是否开启，默认为开启<img src="https://main.qcloudimg.com/raw/9f12e685bdc6e7269f8b6d56932972e5.png"  style="margin:0;">状态。关闭防护功能后，若遭受 DDoS 攻击可能会导致服务器瘫痪，请谨慎操作。

### 清洗阈值
清洗阈值是高防产品启动清洗动作的阈值。当流量小于阈值时，即使检测到攻击也不会进行清洗操作。
>若明确该清洗阈值，可参考 [配置清洗阈值与防护等级](https://intl.cloud.tencent.com/document/product/1029/31760) 进行自定义设置。若无法明确该清洗阈值，DDoS 防护系统将根据 AI 算法自动学习并生成一套专属的默认阈值。

### 防护等级
防护等级分为宽松、正常和严格，默认为【正常】。用户可根据实际业务需求进行自定义设置，具体操作请参考 [配置清洗阈值与防护等级](https://intl.cloud.tencent.com/document/product/1029/31760)。
各个防护等级的具体防护操作如下表：

<table>
    <tr>
        <th>防护等级</th>
        <th>防护操作</th>
				<th>描述</th>
    </tr>
    <tr>
        <td>宽松</td>
        <td><ul><li>过滤明确攻击特征的 SYN、ACK 数据包。</li>
                     <li>过滤不符合协议规范的 TCP、UDP、ICMP 数据包。</li>
                     <li>过滤具有明确攻击特征的 UDP 数据包。</li></ul></td>
				<td>清洗策略相对宽松，仅对具有明确攻击特征的攻击包进行防护。<br/>建议在怀疑有误杀时启用，遇到复杂攻击时可能会有攻击透传。</td>
    </tr>
    <tr>
        <td>正常</td>
        <td><ul><li>过滤明确攻击特征的 SYN、ACK 数据包。</li>
                     <li>过滤不符合协议规范的 TCP、UDP、ICMP 数据包。</li>
                     <li>过滤具有明确攻击特征的 UDP 数据包。</li>
                     <li>过滤常见基于 UDP 的攻击数据包。</li>
                     <li>对部分访问源 IP 进行主动验证。</li></ul></td>
				<td>清洗策略适配绝大多数业务，可有效防护常见攻击。<br/>默认为正常模式。</td>
    </tr> 
		<tr>
        <td>严格</td>
        <td><ul><li>过滤明确攻击特征的 SYN、ACK 数据包。</li>
                     <li>过滤不符合协议规范的 TCP、UDP、ICMP 数据包。</li>
                     <li>过滤具有明确攻击特征的 UDP 数据包。</li>
                     <li>过滤常见基于 UDP 的攻击数据包。</li>
                     <li>对部分访问源 IP 进行主动验证。</li>
                     <li>过滤 ICMP 攻击包。</li>
                     <li>过滤常见的 UDP 攻击数据包。</li>
                     <li>UDP 数据包严格检查。</li></ul></td>
				<td>清洗策略相对严格，建议在正常模式出现攻击透传时使用。</td>
    </tr>
</table>

 >如果业务需要使用 UDP，建议联系 [腾讯云技术支持](https://intl.cloud.tencent.com/support) 进行策略定制，以免严格模式影响业务。

### 业务场景
BGP 高防包提供业务场景设置功能，通过用户创建业务应用场景，后台收集、识别并自动生成高级防护策略，实现灵活的配置或维护防护策略，具体操作请参见 [配置业务场景](https://intl.cloud.tencent.com/document/product/1029/31761)。
### 高级策略
BGP 高防包提供面向 DDoS 攻击的高级防护策略功能，用户可针对自身业务防护需求对 DDoS 防护策略进行调整和优化。通过黑白名单、禁用协议、禁用端口、报文特征过滤策略以及空连接防护，为业务提供针对性防护。新增、管理高级策略的操作具体请参考 [管理 DDoS 高级防护策略](https://intl.cloud.tencent.com/document/product/1029/31762)。
### DDoS 攻击告警阈值
表示触发推送 DDoS 攻击告警信息动作的阈值。当检测到的告警指标小于设定阈值时，系统不会给指定用户群体发送 DDoS 攻击告警信息。


