## 操作场景

您可以使用云服务器控制台进行创建、查看、更新和删除等操作，管理安全组及安全组规则。同时我们还提供典型场景配置案例供您参考。

## 前提条件

已登录 [腾讯云云服务器控制台](https://console.cloud.tencent.com/cvm/index)。

<span id="common"></span>
## 操作步骤

### 创建安全组

1. 在左侧导航栏中，单击【[安全组](https://console.cloud.tencent.com/cvm/securitygroup)】，进入安全组管理页面。
2. 单击【新建】，弹出“新建安全组”窗口。
3. 选择模板，输入安全组的名称（例如 my-security-group），提供备注说明。
4. 单击【确定】，完成创建。

### 向安全组中添加规则

1. 在左侧导航栏中，单击【[安全组](https://console.cloud.tencent.com/cvm/securitygroup)】，进入安全组管理页面。
2. 选择需要添加规则的安全组 ID/名称，进入该安全组管理页面。
3. 选择“安全组规则” > “入出站规则/出站规则”页签，单击【添加规则】，填写所需信息。
4. 单击【完成】。

### 配置 CVM 实例关联安全组

#### 方式一

1. 在左侧导航栏中，单击【[实例](https://console.cloud.tencent.com/cvm/index)】，进入实例管理页面。
2. 在需要关联安全组的实例行的“操作”列中，单击【更多】，选择【安全组】>【配置安全组】。
3. 在弹出的“配置安全组”窗口中，选择一个或多个安全组，单击【确定】。

#### 方式二

1. 在左侧导航栏中，单击【[安全组](https://console.cloud.tencent.com/cvm/securitygroup)】，进入安全组管理页面。
2. 在需要关联实例的安全组行的“操作”列中，单击【管理实例】，进入关联实例页面。
3. 在“云主机”页签下，单击【新增关联】。
4. 在弹出的“新增实例关联”窗口中，选择一个或多个实例，单击【确定】。

### 导入/导出安全组规则

1. 在左侧导航栏中，单击【[安全组](https://console.cloud.tencent.com/cvm/securitygroup)】，进入安全组管理页面。
2. 选择需要导入/导出安全组规则的安全组 ID/名称，进入该安全组管理页面。
3. 选择“安全组规则” > “入站/出站规则”页签，单击【导入规则】。
>? 如果您原来已有规则，则建议您先导出现有规则，否则导入新规则时，将覆盖原有规则。如果原来为空规则，则可先导出模板，编辑好模板文件后，再将文件导入。
4. 在弹出的“批量导入-入站/出站规则”窗口中，选择模板文件，单击【开始导入】。

### 克隆安全组

1. 在左侧导航栏中，单击【[安全组](https://console.cloud.tencent.com/cvm/securitygroup)】，进入安全组管理页面。
2. 在需要克隆的安全组行的“操作”列中，单击【更多】，选择【克隆】。
3. 在弹出的“克隆安全组”窗口中，选定目标地域、目标项目，输入新名称，单击【确定】。
>! 若新安全组需关联 CVM ，请重新进行安全组配置。

### 删除安全组

1. 在左侧导航栏中，单击【[安全组](https://console.cloud.tencent.com/cvm/securitygroup)】，进入安全组管理页面。
2. 在需要删除的安全组行的“操作”列中，单击【更多】，选择【删除】。
3. 在弹出的提醒框中，单击【确定】。
>! 若当前安全组有关联的 CVM ，则需要先解除安全组才能进行删除。

<span id="typical"></span>
## 典型场景配置

>? 以下仅为典型场景安全组入站规则的配置，如果您的实例需要对外访问（例如软件升级等），您可以放通出站规则下所有端口。
>
为了您实例的安全性和支撑典型使用场景，需要您执行以下操作：
1. 进行合理的端口放通策略。
2. 登录 [安全组规则配置界面](https://console.cloud.tencent.com/cvm/securitygroup/detail/)，并按以下模版配置入站规则。
>! 
> - 您可在来源处设置**地址段**或**安全组**。 
> - 在配置安全组规则时，如果在来源/目标中输入安全组 ID ，表示仅将此安全组 ID 所绑定的 CVM、弹性网卡的内网 IP 地址作为来源/目标，不包括外网 IP 地址。
> - 请确保您已放通相应出站规则。
> 
<table>
<tr>
	<th>使用场景</th>
	<th>类型</th>
	<th>来源</th>
	<th>协议端口</th>
	<th>策略</th>
</tr>
<tr>
	<td>SSH 远程登录 Linux 实例</td>
	<td>Linux 登录</td>
	<td>0.0.0.0/0	</td>
	<td>TCP:22</td>
	<td>允许</td>
</tr>
<tr>
	<td>RDP 远程登录 Windows 实例</td>
	<td>Linux 登录</td>
	<td>0.0.0.0/0	</td>
	<td>TCP:3389</td>
	<td>允许</td>
</tr>
<tr>
	<td>公网 ping CVM 实例</td>
	<td>Ping</td>
	<td>0.0.0.0/0	</td>
	<td>ICMP</td>
	<td>允许</td>
</tr>
<tr>
	<td rowspan="2">CVM 实例作 Web 服务器</td>
	<td>HTTP（80）</td>
	<td>0.0.0.0/0	</td>
	<td>TCP:80</td>
	<td>允许</td>
</tr>
<tr>
	<td>HTTPS（443）</td>
	<td>0.0.0.0/0	</td>
	<td>TCP:443</td>
	<td>允许</td>
</tr>
<tr>
	<td>FTP 上传或下载文件</td>
	<td>自定义</td>
	<td>0.0.0.0/0	</td>
	<td>TCP:20,21</td>
	<td>允许</td>
</tr>
<tr>
	<td rowspan="2">FTP 上传或下载文件（被动模式）</td>
	<td rowspan="2">自定义</td>
	<td rowspan="2">0.0.0.0/0	</td>
	<td>TCP:21</td>
	<td rowspan="2">允许</td>
</tr>
<tr>
	<td>TCP:1024-65535	</td>
</tr>
<tr>
	<td>Webshell 登录云服务器</td>
	<td>自定义</td>
	<td>115.159.198.247</br>
	115.159.211.178</br>
	116.119.28.7.195</br>
	117.119.28.22.215</br>
	118.119.29.96.147</br>
	119.211.159.185.38</td>
	<td>TCP:22</td>
	<td>允许</td>
</tr>
</table>
上表仅包含部分常用端口，其余常用端口详情参见 <a href="https://cloud.tencent.com/document/product/213/12451">服务器常用端口</a>。
