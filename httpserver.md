
## postgresdriver
### 快捷导航
[表格说明(table)](#表格说明)<br>
[树形说明(tree)](#树形说明)<br>
[树形表格说明(treetable)](#树形表格说明)<br>
[分组表格说明(grouptable)](#分组表格说明)<br>
[操作说明(operate)](#操作说明)<br>
[确认框说明(confirm)](#确认框说明)<br>
[信息说明(info)](#信息说明)<br>
[图表说明(chart)](#图表说明)<br>

### 1) 示例配置（config.json）

```
{
  "Version": "0.0.1",//插件版本
  "Key":"",//验证秘钥
  "Name": "httpserver",//名称
  "Address": "localhost",//插件地址
  "GRPC": "localhost:20001",//GRPC通信地址
  "Port": 20002,//绑定端口地址
  "Thread": 32,//声明并发协程数量
  "HttpPort": 80, //绑定运行端口
  "HttpTLS": false, //是否开启TLS
  "HttpCert": "", //TLS证书文件地址
  "HttpKey": "", //TLS密钥文件地址
  "Clear": 1 //清除未使用资源时间周期(h)
}
```

### 2) 配置说明

|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|Version|string|是|无|插件版本|
|Key|string|是|无|验证秘钥|
|Name|string|是|httpserver|插件名称，不可修改|
|Address|string|是|无|插件运行地址，当前地址或者远程地址|
|GRPC|string|是|无|GRPC通信地址，当前地址或者远程地址，默认端口20001|
|Port|int|否|无|运行绑定端口地址，为空则自动分配|
|Thread|int|是|无|声明并发协程数量|
|HttpPort|int|是|无|绑定运行端口||
|HttpTLS|bool|是|无|是否开启TLS|
|HttpCert|string|是|无|TLS证书文件地址|
|HttpKey|string|是|无|TLS密钥文件地址|
|Clear|int|是|无|清除未使用资源时间周期(h)|

### 3) 调用方式示例

(待定)

### 4) 传递JSON说明:

(待定)

### 5) 其他说明:

#### <div id="表格说明">表格说明(table)</div>
#### <div id="树形说明">树形说明(tree)</div>
#### <div id="树形表格说明">树形表格说明(treetable)</div>
#### <div id="分组表格说明">分组表格说明(grouptable)</div>
#### <div id="操作说明">操作说明(operate)</div>
#### <div id="确认框说明">确认框说明(confirm)</div>
#### <div id="信息说明">信息说明(info)</div>
(待定)
#### <div id="图表说明">图表说明(chart)</div>
(待定)
