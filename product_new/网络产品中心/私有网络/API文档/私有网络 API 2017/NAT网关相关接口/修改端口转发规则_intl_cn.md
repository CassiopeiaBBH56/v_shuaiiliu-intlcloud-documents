## 1. 接口描述
本接口（ModifyDnaptRule）用于修改 NAT 网关端口转发规则。
接口请求域名：`vpc.api.qcloud.com`

使用该接口前请前往 <a href="https://intl.cloud.tencent.com/doc/product/215/1682" title="网关说明" >NAT 网关说明</a> 了解 NAT 网关特性。

## 2. 输入参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见 [公共请求参数](https://intl.cloud.tencent.com/doc/api/229/6976) 页面。其中，此接口的 Action 字段为 ModifyDnaptRule。

| 参数名称 | 是否必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| vpcId | 是 | String | 私有网络 ID，如：vpc-8e0ypm3z |
| natId | 是 | String | NAT 网关 ID，如：nat-dqbak2vy |
| oldProto | 是 | String | 原协议，可选值：tcp、udp |
| oldEip | 是 | String | 原外部 IP，即关联弹性 IP |
| oldEport | 是 | String | 原外部端号 |
| proto | 否 | String | 新协议，可选值：tcp、udp |
| eip | 否 | String | 新外部 IP，即关联弹性 IP |
| eport | 否 | String | 新外部端号 |
| pip | 否 | String | 新内部 IP |
| pport | 否 | String | 新内部端号 |
| description | 否 | String | 新规则描述 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 错误码。0：成功, 其他值：失败|
| message | String | 错误信息|

## 4. 错误码表
以下错误码表仅列出了该接口的业务逻辑错误码，更多公共错误码详见<a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC错误码">VPC错误码</a>。

| 错误码 | 描述 |
|---------|---------|
| 29151 | 规则描述长度超过限制|
| 29152 | 规则冲突，弹性 IP 已存在|
| 29153 | 内部 IP未绑定任何实例|
| -3325 | 弹性 IP 不存在|
| -3326 | 内部 IP 不在 VPC 内|
| -3327 | 规则冲突，内部 IP 已存在|
| -3328 | 端口转发规则数量达到上限|
| -3344 | 内部 IP 不在子机内|

## 5. 示例
输入
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=ModifyDnaptRule
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
&vpcId=vpc-d8vg6rev
&natId=nat-k6npdayk
&oldProto=tcp
&oldEip=139.199.232.178
&oldEport=303
&proto=tcp
&eip=139.199.232.178
&eport=304
&pip=10.90.90.11
&pport=304
&description=test
</pre>
输出
```
{
	"code": "0",
	"message": ""
}
```
