[//]: # (chinagitpath:XXXXX)

创建完规则，即可编写 SQL 对某一类 Topic 中数据的处理。物联网通信控制台提供了 SQL 填写的方式来简化 SQL 语句的生成，即在红框的条件中对 Topic 数据进行筛选。
![](https://main.qcloudimg.com/raw/4a9e8f0f4731648d1613e55380511266.png)

下图中示例表达的规则：
将 Topic 为```E23VBC3GE8/device_02/event```中的 JSON 消息的```action targetDevice count```字段提取出来，再通过```count <=3```对数据进行过滤，得到最终处理过的数据用于下一步数据转发。
![](https://main.qcloudimg.com/raw/bdeab8841c4f62434bb925fecfd27a00.png)

## 行为 Action
当从 Topic 提取到了感兴趣的字段后，就要考虑对其进行一些操作，比如转发或者存储等。目前支持的操作有：
- 数据转发到另一个 Topic
- 数据转发到第三方服务
- 数据转发到消息队列 CKafka
- 数据转发到消息队列 CMQ-Topic
- 数据转发到时序数据库 CTSDB
- 数据转发到云数据库 MySQL
- 数据转发到云数据库 MongoDB

## 参考

### Topic 通配符的详细定义

如果想要监听多个 Topic，可以使用```#```和```+```通配符来定义多个 Topic。
 - ```#```代表 0 个或多个任意 Topic 段，只能放在 Topic 的最后。
 - ```+```代表 1 个任意 Topic 段，可以放在 Topic 的中间。

例如： ```house_monitor/+/get```
可监听```house_monitor/thermometer/get```和```house_monitor/door/get``` 等 Topic；
但不可监听 ```house_monitor/door/switch/get```，因为```+```只能代表 1 个 Topic 段。

例如： ```house_monitor/#```
可监听 ```house_monitor/thermometer``` 和```house_monitor/door/switch/get``` 等 Topic；
但 ```house/#/get``` 是非法的，因为```#```只能放在 Topic 结尾。

### 条件的详细定义
[条件]表达式用于过滤 Topic 中的消息，只有当消息满足[条件]表达式时，才会被提取并进行后续的处理，下表是支持的表达式：

|操作符 | 描述 | 举例|
|---|---|---|
|= | 相等 | color = 'red'|
|<> | 不等于           | color <> ‘red’|
|AND    | 逻辑与           | color = ‘red’ AND siren = ‘on’|
|OR | 逻辑或           | color = ‘red’ OR siren = ‘on’|
|( )    | 括号代表一个整体  | color = ‘red’ AND (siren = ‘on’ OR isTest)|
|+  | 算术加法          | 4 + 5|
|-  | 算术减           | 5 - 4|
|/  | 除             | 20 / 4|
|*  | 乘             | 5 * 4|
|%  | 取余数           | 20 % 6|
|<  | 小于                | 5 < 6|
|<= | 小于或等于     | 5 <= 6|
|>  | 大于                | 6 > 5|
|>= | 大于或等于     | 6 >= 5|
|CASE … WHEN … THEN … ELSE …END |Case 表达式               | CASE col WHEN 1 THEN ‘Y’ WHEN 0 THEN ‘N’ ELSE ‘’ END as flag|
|IN                             | 仅支持枚举，不支持子查询  | 比如 where a in(1,2,3); 不支持以下形式： where a in(select xxx)|
