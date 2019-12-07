
## postgresdriver
### 快捷导航
[* 通用格式化说明](#通用格式化说明)<br>
[* 通用权限验证说明](#通用权限验证说明)<br>
[* 通用查询语句说明](#通用查询语句说明)<br>
[* 通用表格字段说明](#通用表格字段说明)<br>
[* 通用输入字段说明](#通用输入字段说明)<br>
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

#### <div id="通用格式化说明">* 通用格式化说明</div>
格式化模板：<% 查询集合.0(为数字取对应下标的对象[array]).name(不为为数字取对应对象值[map])<br>例：<% query.0.name %>为取query集合下面的0号元素的name
#### <div id="通用权限验证说明">* 通用权限验证说明</div>
传入参数为当前页面param与所选参数的集合，后者覆盖前者，调用字段value(object)，采用javascript语句，返回bool
#### <div id="通用查询语句说明">* 通用查询语句说明</div>
##### 1、示例:
```
{
    "Name":"查询/执行Query名",
    "Error":"失败时返回值",
    "Sentence":"select now()"
}
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|Name|string|是|无|查询/执行Query名|
|Error|string|否|默认返回值|查询/执行查询失败时返回值|
|Sentence|string|是|无|1、begin：启动事务<br>2、commit：提交事务<br>3、rollback：回滚事务<br>4、查询sql语句/存储过程/函数：支持动态防注入替换，替换模板<% 传递调用参数(优先)/查询集合.0(为数字取对应下标的对象[array]).name(不为为数字取对应对象值[map])，例：<% query.0.name %>为取query集合下面的0号元素的name|
#### <div id="通用表格字段说明">* 通用表格字段说明</div>
##### 1、示例:
```
{
    "name": "名称", //显示名称
    "itype": "string", //格式化类型
    "show": true, //默认是否显示
    "select": true, //是否允许高级搜索
    "data": "name" //绑定字段
    "repeat": "" //自动重复渲染
    "permission": "" //类型为input时生效，验证输入框是否能操作
    "action": "" //类型为input时生效，监听字段改变，执行对应方法
    "option":  [
          {
            "permission": "value.name.indexOf('测试')>-1",
            "value": "bg-blue-500"
          }
    ] //类型为label时生效，根据不同判断，返回不同样式
}
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|itype|string|是|无|格式化类型，index(不支持高级搜索)，int，string，float+小数点数量(非必须)，file，files，image，images，date，datetime，input，label|
|show|bool|是|无|默认是否显示|
|select|bool|是|无|是否允许高级搜索|
|data|string|是|无|绑定字段|
|repeat|string|否|无|自动重复渲染，如果有值，绑定default下面的查询语句(name对应名称，data对应字段，保存类型jsonb)|
|permission|[通用权限验证](#通用权限验证说明)|否|无|类型为input时生效，验证输入框是否能操作|
|action|uuid|否|无|类型为input时生效，监听字段改变，执行对应方法|
|option|array|否|无|类型为label时生效，根据不同判断，返回不同样式(permission[通用权限验证](#通用权限验证说明)，value返回对应样式，默认底色为系统底色)|
#### <div id="通用输入字段说明">* 通用输入字段说明</div>
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
