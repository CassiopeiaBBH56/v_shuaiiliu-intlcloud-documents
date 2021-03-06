You can modify the configuration of the origin server for your domain name:
- Multi-site active-active IPs 
When multiple IPs are configured as the origin server, CDN uses a polling policy to randomly select an IP for origin-pull. It also performs origin server detection, so that when an origin server IP is found to be exceptional, it will be blocked for a period of time (60 seconds by default) and skipped during polling.
- Domain name origin server
A specified domain name can be set as the origin server, which should be different from the accelerated domain name.
- COS bucket origin server
A public domain name of the selected COS bucket can be used as an origin server for CDN origin-pull.
- Slave origin server configuration
Tencent Cloud CDN supports configuring an external domain name as a hot backup slave origin server. When an origin-pull request to the master origin server fails (e.g., 4XX, 5XX, or TCP connection errors), it will be forwarded to the slave origin server. Configuring a slave origin server can effectively reduce the failure rate of origin-pull and improve the service quality. The hot backup slave origin server does not support HTTPS origin-pull for the time being; therefore, when you configure a certificate for a domain name with a slave origin server, do not select HTTPS origin-pull.
>- Only origin servers of the domain names connected by you can be modified, while those of CDN accelerated domain names automatically created by [COS](https://intl.cloud.tencent.com/product/cos) buckets cannot.
>- According to applicable regulations, if an origin server is at an accelerated domain name of Tencent Cloud CVM, the domain name configured for the host header should have the ICP filing completed through Tencent Cloud.

## Configuration Guide
### Viewing the Configuration
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the row of the domain name to be edited and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/4e3c48f2ce14d2c9e3faf91597b1855d.jpg)
3. On the "Basic Configuration" page, you can see the **Origin Server Information** module where you can view the current origin server configuration of the domain name.
 ![](https://main.qcloudimg.com/raw/e547a4f48a0012d596be7de37694068d.jpg)

## Modifying Origin Server
1. On the "Basic Configuration" page, you can see the "Origin Server Information" module.
 ![](https://main.qcloudimg.com/raw/cacaa282099503853d960bcd69482351.jpg)
2. Click the **Edit** icon in the top-right corner of the master origin server to modify its type:
![](https://main.qcloudimg.com/raw/0442fbc0938c8182b81b83c77afa0d09.jpg)

**External Origin**: The origin server address can be configured as multiple IPs or one single domain name. Origin-pull to the specified port is supported in the format of "domain name:PORT/IP:PORT" in the value range from 0 to 65535.
- If the origin server address is configured as IPs, the weight of the origin server IPs can be configured in the format of IP:PORT:WEIGHT in the value range from 0 to 1000.
	- The weight cannot be set for single origin server.
	- If the origin server is multiple IPs, it is not allowed to set origin-pull weight only for certain IPs.
	- If the origin server is in domain name format, the weight cannot be set. Instead, only IP origin servers support weight configuration.
	- Weight can be configured in the format of IP:PORT:WEIGHT, where PORT can be omitted. In this case, the format is IP::WEIGHT.
	- Currently, only IPv4 addresses support weight configuration, while IPv6 addresses do not.

**COS Origin**: Specify a COS bucket as the origin server.


### Adding a Slave Origin Server
1. If the origin server of a domain name is an **external origin**, you can add a hot backup slave origin server for it. When an origin-pull request to the master origin server fails (e.g., 4XX, 5XX, or TCP connection errors), it will be forwarded to the slave origin server.
 ![](https://main.qcloudimg.com/raw/cacaa282099503853d960bcd69482351.jpg)
2. A slave origin server can only be added for an external origin. The origin server address can be configured as multiple IPs or one domain name. Origin-pull to the specified port is supported in the port range from 0 to 65535.
 ![](https://main.qcloudimg.com/raw/08dc5e26f2a7c36eca385375e3290c41.jpg)

### Modifying Slave Origin Server
After adding a slave origin server, you can perform master/slave switch quickly or modify or delete the slave origin server in the console.
![](https://main.qcloudimg.com/raw/08756e81a68f7e04f079289c95d33cd1.jpg)

## Configuration Case
A user requests `http://www.test.com/1.jpg` which is not hit on any node. The request is forwarded to the origin server.
1. If the origin server is configured as follows:
 ![](https://main.qcloudimg.com/raw/cacaa282099503853d960bcd69482351.jpg)
If the resource is not cached on the server `1.1.1.1`, a 404 error will be directly returned. In this case, after receiving the response, the CDN node at the origin-pull layer will directly return the request to the requesting client, and the client cannot obtain the image.
2. If the origin server is configured as follows:
 ![](https://main.qcloudimg.com/raw/08756e81a68f7e04f079289c95d33cd1.jpg)
If the resource is not cached on the server `1.1.1.1`, a 404 error will be directly returned. In this case, after receiving the response, the CDN node at the origin-pull layer will request the resource again to the slave origin server `2.2.2.2`. If `2.2.2.2` returns a 200 status code, the node will send the successfully obtained content to the requesting client, and the client will successfully obtain the image.
