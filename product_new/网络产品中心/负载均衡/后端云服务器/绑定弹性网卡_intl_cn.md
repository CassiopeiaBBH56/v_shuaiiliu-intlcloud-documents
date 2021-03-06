## 弹性网卡简介
[弹性网卡（Elastic Network Interface，ENI）](http://intl.cloud.tencent.com/document/product/576/18525)是一种可以绑定私有网络内 CVM 实例上的虚拟网卡。弹性网卡可以自由地在相同私有网络、可用区下的 CVM 间自由迁移，通过弹性网卡可以实现高可用集群搭建、低成本故障转移和精细化的网络管理。
CLB 的后端服务支持 CVM 和 ENI，即 CLB 支持绑定 CVM 和 ENI。CLB 与后端服务之间使用内网通信，当 CLB 绑定多台 CVM 和 ENI 时，访问流量会被转发到 CVM 的内网 IP 和 ENI 的内网 IP上。

>CLB 支持绑定弹性网卡功能正在内测中，如需使用，请通过 [工单申请](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB)。

## 前提条件
ENI 必须先绑定在某台云服务器上，CLB 才能绑定该 ENI。CLB 只做负载均衡转发流量，并不实际处理业务逻辑，因此需要计算资源 CVM 实例来处理用户请求。请先前往 [弹性网卡控制台](https://console.cloud.tencent.com/vpc/eni)，将所需的弹性网卡与云服务器做绑定。
![](https://main.qcloudimg.com/raw/ad2a5587ac58da1c4a930db935f998af.png)

## 操作步骤
1. 您需要先配置负载均衡监听器，详情请参见 [负载均衡监听器概述](http://intl.cloud.tencent.com/document/product/214/6151)。
2. 单击已创建完毕的监听器左侧的【+】展开域名和 URL 路径，选中具体的 URL 路径，在监听器右侧查看已绑定的后端服务。
![](https://main.qcloudimg.com/raw/12da12bb7b9c4be7baa6a7d911eea9d3.png)
3. 单击【绑定】，即可在弹出框中选择需绑定的后端服务器，并配置服务端口和权重，弹出框中可选择与 CLB 同私有网络的所有可被绑定的 CVM 和 ENI。
![](https://main.qcloudimg.com/raw/873717f962d4ec2c862abe6512b4d2cb.png)
4. 绑定完毕的配置详情如下。
![](https://main.qcloudimg.com/raw/698acc505124c04cb626a8ca4abc1498.png)
