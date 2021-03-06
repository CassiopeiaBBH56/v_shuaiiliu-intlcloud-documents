## What is Content Delivery Network?

Content Delivery Network (CDN) is a layer of network architecture built on the internet that is composed of servers distributed across regions, which work together to provide faster delivery of internet content. These high-performance cache nodes store your content based on certain caching policies. When your user makes a request for your content, the request will be routed to the node closest to the user. Then, the node will respond to the request directly, greatly reducing the user access latency and improving availability.

CDN offers an effective solution to the following problems at the network level:
1. The long physical distance between user and business server causes the request to be forwarded over the network many times, leading to high latency and instability.
2. The ISP used by the user is different from the one where the business server resides, so the request needs to be forwarded between the ISPs after they are interconnected with each other.
3. The limited network bandwidth and processing capacity of business server result in slower response and lower availability when there are massive amounts of user requests.

CDN is easy to use. To connect to CDN, you do not need to adjust your business structure or handle any complex configurations. For more information, see [Getting Started](https://intl.cloud.tencent.com/doc/product/228/3149).

## How Does Acceleration Work?
For example, if your business origin server's domain name is ```www.test.com``` which has been connected to CDN, and the acceleration service has been activated, when a user makes an HTTP request, the request will be processed as shown below:
![](https://main.qcloudimg.com/raw/c1861d3811816821cda66e6daff48ced.jpg)

**The process is as detailed below:**
1. When a user makes an access request for an image resource (e.g., 1.jpg) at ```www.test.com```, a domain name resolution request will be initiated to the local DNS first.
2. When the local DNS resolves ```www.test.com```, it will find that CNAME ```www.test.com.cdn.dnsv1.com``` has been configured, so the resolution request will be sent to Tencent DNS (GSLB), Tencent Cloud's proprietary scheduling system, which will assign the optimal node IP for the request.
3. The local DNS receives the resolved IP returned by Tencent DNS.
4. The user receives the resolved IP.
5. The user makes an access request for 1.jpg to the received IP.
6. If the CDN node corresponding to the IP has already cached 1.jpg, data will be directly returned to the user (10), and the process ends; otherwise, the CDN node will initiate a request for 1.jpg to the origin server (6, 7, and 8). After receiving the resource, the CDN node will cache it (9) based on the caching policy configured (see [Cache Expiration Configuration](https://intl.cloud.tencent.com/doc/product/228/6290)) and return it to the user (10). Then, the process ends.
