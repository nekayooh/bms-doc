
## postgresdriver

### 1) 示例配置（config.json）

```
{
  "Version": "0.0.1",//插件版本
  "Key":"",//验证秘钥
  "Name": "postgresdriver",//名称
  "Address": "localhost",//插件地址
  "GRPC": "localhost:20001",//GRPC通信地址
  "Port": 20002,//绑定端口地址
  "Thread": 32,//声明并发协程数量
  "PGUrl": ""//PostgreSQL连接字符串
}
```

### 2) 配置说明

|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|Version|string|是|无|插件版本|
|Key|string|是|无|验证秘钥|
|Name|string|是|postgresdriver|插件名称，不可修改|
|Address|string|是|无|插件运行地址，当前地址或者远程地址|
|GRPC|string|是|无|GRPC通信地址，当前地址或者远程地址，默认端口20001|
|Port|int|否|无|运行绑定端口地址，为空则自动分配|
|Thread|int|是|无|声明并发协程数量|
|PGUrl|string|是|无|PostgreSQL连接字符串|

### 3) 调用方式示例

```
query, _ := BMSClient.Msg(context.Background(), &proto.SendMsg{
	Name: "postgresdriver",
	Uuid: BMSConfig.UUID,
	Auth: BMSConfig.Name,
	Json: []byte("{\"Data\":{},\"Query\":[]}"),
})
```

### 4) 传递JSON说明:

|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|Data|map|是|无|传递调用参数|
|Query|array|是|无|查询数据对象集合|

#### Query对象示例:
```
{
    "Name":"查询/执行Query名",
    "Error":"失败时返回值",
    "Sentence":"select now()"
}
```

#### Query对象说明:

|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|Name|string|是|无|查询/执行Query名|
|Error|string|否|默认返回值|查询/执行查询失败时返回值|
|Sentence|string|是|无|1、begin：启动事务<br>2、commit：提交事务<br>3、rollback：回滚事务<br>4、查询sql语句/存储过程/函数：支持动态防注入替换，替换模板<% 传递调用参数(优先)/查询集合.0(为数字取对应下标的对象[array]).name(不为为数字取对应对象值[map])，例：<% query.0.name %>为取query集合下面的0号元素的name|
