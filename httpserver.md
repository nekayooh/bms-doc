
## postgresdriver
### 快捷导航
[* 通用格式化说明](#通用格式化说明)<br>
[* 通用权限验证说明](#通用权限验证说明)<br>
[* 通用按钮说明](#通用按钮说明)<br>
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
|HttpPort|int|是|无|绑定运行端口|
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
#### <div id="通用按钮说明">* 通用按钮说明</div>
##### 1、示例:
```
{
    "icon": "shape-square-plus text-red-400", //显示图标
    "name": "多选删除", //显示名称
    "modal": false, //是否弹窗打开
    "template": "42c593e7-079e-41f0-8826-2211fbf1a06a", //绑定方法页面
    "permission": "" //权限验证
}
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|icon|string|是|无|显示图标|
|name|string|是|无|显示名称|
|modal|bool|是|无|是否弹窗打开|
|template|uuid|是|无|绑定方法页面|
|permission|string|否|无|[通用权限验证](#通用权限验证说明)|
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
|repeat|string|否|无|自动重复渲染，如果有值，[通用格式化](#通用格式化说明)数据，取default数据(name对应名称，data对应字段，保存类型jsonb)|
|permission|[通用权限验证](#通用权限验证说明)|否|无|类型为input时生效，验证输入框是否能操作|
|action|uuid|否|无|类型为input时生效，监听字段改变，执行对应方法|
|option|array|否|无|类型为label时生效，根据不同判断，返回不同样式(permission[通用权限验证](#通用权限验证说明)，value返回对应样式，默认底色为系统底色)|
#### <div id="通用输入字段说明">* 通用输入字段说明</div>
##### 1、示例:
```
{
    "name": "文字框示例", //显示名称
    "disabled": false, //是否禁止编辑
    "must": true, //是否必须有值（不为空）
    "itype": "string", //格式化类型
    "data": "string", //绑定字段
    "value": "", //默认值
    "fix": 2, //类型为float时生效，格式化小数点数量
    "option": [
          {
            "name": "选项一",
            "value": "1"
          },
          {
            "name": "选项二",
            "value": "2"
          },
          {
            "name": "选项三",
            "value": "3"
          }
    ], //类型为select时生效，选项名称和值
    "option": "", //类型为select时生效，选项名称和值，绑定default里面数据
    "rows": "", //类型为textarea时生效，文本域行数
    "image": "", //类型为richtext时生效，保存图片位置，为空
    "resize": "", //类型为image，images时生效，例：200x200(长x宽)
}
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|disabled|bool|是|无|是否禁止编辑|
|must|bool|是|无|是否必须有值（不为空）|
|itype|string|是|无|格式化类型，int，string，float，file，files，image，images，date，datetime，richtext，textarea，select，bool|
|data|string|是|无|绑定字段|
|value|string|是|kind.0.name|[通用格式化](#通用格式化说明)数据，取prepare数据|
|fix|int|否|无|类型为float时生效，格式化小数点数量|
|option|array/string|否|无|类型为select时生效，选项名称和值，[通用格式化](#通用格式化说明)数据，取default数据(name对应名称，data对应值)|
|rows|int|否|无|类型为textarea时生效，文本域行数|
|image|string|否|无|类型为richtext时生效，保存图片位置，为空|
|resize|string|否|无|类型为image，images时生效，例：200x200(长x宽)|
#### <div id="表格说明">表格说明(table)</div>
##### 1、示例:
```
{
    "default": [], //基础语句集合
    "prepare": [], //数据语句集合
    "query": [], //查询语句集合
    "head": [], //表头集合
    "name": "表格框示例", //显示名称
    "itype": "table", //模块类型
    "param": [], //默认获取参数
    "button": [], //顶部按钮集合
    "menu": [], //右键菜单集合
    "multiple": [], //多选右键菜单集合
    "refresh": true, //是否刷新上级页面
    "config": { //默认基础配置
      "page": "0", //默认页数
      "sort": "id", //默认检索字段
      "status": "down", //默认检索字段顺序
      "count": "50" //默认页数
    },
    "placeholder": "名称", //搜索框显示默认文字
    "export": true, //是否允许导出
    "other": "共计 <% total.0.total %> 条数据" //底部显示额外信息
    "action": "" //点击执行对应方法
  }
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|default|array|否|无|基础语句集合，第一次执行返回所有数据，[通用查询语句](#通用查询语句说明)|
|prepare|array|是|无|数据语句集合，每次执行返回所有数据，返回名为total为总查询数量，[通用查询语句](#通用查询语句说明)|
|query|array|是|无|查询语句集合，每次执行返回名为query数据，[通用查询语句](#通用查询语句说明)|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|itype|string|是|table|模块类型，不可修改|
|param|array|是|无|默认获取参数，{name(原数据字段名):xxx,data(新数据字段名):xxx}，sql调用方式：<% param.新字段名 %>|
|button|array|是|无|顶部按钮集合，[通用按钮](#通用按钮说明)|
|menu|array|是|无|右键菜单集合，[通用按钮](#通用按钮说明)|
|multiple|array|是|无|多选右键菜单集合，[通用按钮](#通用按钮说明)|
|refresh|bool|是|无|是否刷新上级页面|
|config.page|string|是|无|默认页数|
|config.sort|string|是|无|默认检索字段|
|config.status|string|是|无|默认检索字段顺序|
|config.count|string|是|无|默认页数|
|placeholder|string|是|无|搜索框显示默认文字|
|export|bool|是|无|是否允许导出|
|other|string|是|无|底部显示额外信息，[通用格式化](#通用格式化说明)数据，取prepare数据(name对应名称，data对应值）|
|action|uuid|否|无|点击执行对应方法|
##### 3、替换说明:
|字段|说明|
|:-:|:-|
|<% uuid %>|替换格式化传入参数uuid，多个参数格式化为"'uuid1','uuid2',..."，单个参数格式化为"'uuid1'"|
|<% repeat %>|获取重复字段语句，select后使用|
|<% select %>|格式化查询语句，where后使用|
#### <div id="树形说明">树形说明(tree)</div>
##### 1、示例:
```
{
    "query": [], //查询语句集合
    "name": "树形框示例", //显示名称
    "itype": "tree", //模块类型
    "param": [], //默认获取参数
    "menu": [], //右键菜单集合
    "refresh": true, //是否刷新上级页面
    "action": "" //点击执行对应方法
  }
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|query|array|是|无|查询语句集合，每次执行返回名为query数据(uuid当前UUID，name显示名称，parent父级UUID)，[通用查询语句](#通用查询语句说明)|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|itype|string|是|tree|模块类型，不可修改|
|menu|array|是|无|右键菜单集合，[通用按钮](#通用按钮说明)|
|refresh|bool|是|无|是否刷新上级页面|
|action|uuid|否|无|点击执行对应方法|
##### 3、替换说明:
|字段|说明|
|:-:|:-|
|<% uuid %>|替换格式化传入参数uuid，多个参数格式化为"'uuid1','uuid2',..."，单个参数格式化为"'uuid1'"|
#### <div id="树形表格说明">树形表格说明(treetable)</div>
##### 1、示例:
```
{
    "default": [], //基础语句集合
    "default_menu": [], //树形菜单集合
    "default_refresh": true, //是否每次刷新基础语句
    "prepare": [], //数据语句集合
    "query": [], //查询语句集合
    "head": [], //表头集合
    "name": "树形表格示例", //显示名称
    "itype": "treetable", //模块类型
    "param": [], //默认获取参数
    "button": [], //顶部按钮集合
    "menu": [], //右键菜单集合
    "multiple": [], //多选右键菜单集合
    "refresh": true, //是否刷新上级页面
    "config": { //默认基础配置
      "page": "0", //默认页数
      "sort": "id", //默认检索字段
      "status": "down", //默认检索字段顺序
      "count": "50" //默认页数
    },
    "placeholder": "名称", //搜索框显示默认文字
    "export": true, //是否允许导出
    "other": "共计 <% total.0.total %> 条数据" //底部显示额外信息
    "action": "" //点击执行对应方法
  }
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|default|array|否|无|基础语句集合，根据default_refresh执行返回所有数据，[通用查询语句](#通用查询语句说明)|
|default_menu|array|是|无|树形菜单集合，[通用按钮](#通用按钮说明)|
|default_refresh|bool|是|无|是否每次刷新基础语句|
|prepare|array|是|无|数据语句集合，每次执行返回所有数据，返回名为total为总查询数量，[通用查询语句](#通用查询语句说明)|
|query|array|是|无|查询语句集合，每次执行返回名为query数据，[通用查询语句](#通用查询语句说明)|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|itype|string|是|treetable|模块类型，不可修改|
|param|array|是|无|默认获取参数，{name(原数据字段名):xxx,data(新数据字段名):xxx}，sql调用方式：<% param.新字段名 %>|
|button|array|是|无|顶部按钮集合，[通用按钮](#通用按钮说明)|
|menu|array|是|无|右键菜单集合，[通用按钮](#通用按钮说明)|
|multiple|array|是|无|多选右键菜单集合，[通用按钮](#通用按钮说明)|
|refresh|bool|是|无|是否刷新上级页面|
|config.page|string|是|无|默认页数|
|config.sort|string|是|无|默认检索字段|
|config.status|string|是|无|默认检索字段顺序|
|config.count|string|是|无|默认页数|
|placeholder|string|是|无|搜索框显示默认文字|
|export|bool|是|无|是否允许导出|
|other|string|是|无|底部显示额外信息，[通用格式化](#通用格式化说明)数据，取prepare数据(name对应名称，data对应值）|
|action|uuid|否|无|点击执行对应方法|
##### 3、替换说明:
|字段|说明|
|:-:|:-|
|<% uuid %>|替换格式化传入参数uuid，多个参数格式化为"'uuid1','uuid2',..."，单个参数格式化为"'uuid1'"|
|<% repeat %>|获取重复字段语句，select后使用|
|<% select %>|格式化查询语句，where后使用|
#### <div id="分组表格说明">分组表格说明(grouptable)</div>
##### 1、示例:
```
{
    "default": [], //基础语句集合
    "default_button": [], //分组按钮集合
    "default_menu": [], //分组菜单集合
    "default_refresh": true, //是否每次刷新基础语句
    "prepare": [], //数据语句集合
    "query": [], //查询语句集合
    "head": [], //表头集合
    "name": "分组表格示例", //显示名称
    "itype": "treetable", //模块类型
    "param": [], //默认获取参数
    "button": [], //顶部按钮集合
    "menu": [], //右键菜单集合
    "multiple": [], //多选右键菜单集合
    "refresh": true, //是否刷新上级页面
    "config": { //默认基础配置
      "page": "0", //默认页数
      "sort": "id", //默认检索字段
      "status": "down", //默认检索字段顺序
      "count": "50" //默认页数
    },
    "placeholder": "名称", //搜索框显示默认文字
    "export": true, //是否允许导出
    "other": "共计 <% total.0.total %> 条数据" //底部显示额外信息
    "action": "" //点击执行对应方法
  }
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|default|array|否|无|基础语句集合，根据default_refresh执行返回所有数据，[通用查询语句](#通用查询语句说明)|
|default_button|array|是|无|分组按钮集合，[通用按钮](#通用按钮说明)|
|default_menu|array|是|无|分组菜单集合，[通用按钮](#通用按钮说明)|
|default_refresh|bool|是|无|是否每次刷新基础语句|
|prepare|array|是|无|数据语句集合，每次执行返回所有数据，返回名为total为总查询数量，[通用查询语句](#通用查询语句说明)|
|query|array|是|无|查询语句集合，每次执行返回名为query数据，[通用查询语句](#通用查询语句说明)|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|itype|string|是|grouptable|模块类型，不可修改|
|param|array|是|无|默认获取参数，{name(原数据字段名):xxx,data(新数据字段名):xxx}，sql调用方式：<% param.新字段名 %>|
|button|array|是|无|顶部按钮集合，[通用按钮](#通用按钮说明)|
|menu|array|是|无|右键菜单集合，[通用按钮](#通用按钮说明)|
|multiple|array|是|无|多选右键菜单集合，[通用按钮](#通用按钮说明)|
|refresh|bool|是|无|是否刷新上级页面|
|config.page|string|是|无|默认页数|
|config.sort|string|是|无|默认检索字段|
|config.status|string|是|无|默认检索字段顺序|
|config.count|string|是|无|默认页数|
|placeholder|string|是|无|搜索框显示默认文字|
|export|bool|是|无|是否允许导出|
|other|string|是|无|底部显示额外信息，[通用格式化](#通用格式化说明)数据，取prepare数据(name对应名称，data对应值）|
|action|uuid|否|无|点击执行对应方法|
##### 3、替换说明:
|字段|说明|
|:-:|:-|
|<% uuid %>|替换格式化传入参数uuid，多个参数格式化为"'uuid1','uuid2',..."，单个参数格式化为"'uuid1'"|
|<% repeat %>|获取重复字段语句，select后使用|
|<% select %>|格式化查询语句，where后使用|
#### <div id="操作说明">操作说明(operate)</div>
##### 1、示例:
```
{
    "default": [], //基础语句集合
    "prepare": [], //数据语句集合
    "query": [], //查询语句集合
    "name": "操作页面示例", //显示名称
    "itype": "operate", //模块类型
    "param": [], //默认获取参数
    "menu": [], //右键菜单集合
    "uuid": 1, //生成id数量
    "back": false, //是否完成时返回
    "refresh": true, //是否刷新上级页面
    "import": true //是否允许批量导入
  }
```
##### 2、说明:
|字段|类型|必须|示例值|说明|
|:-:|:-:|:-:|:-:|:-|
|default|array|否|无|基础语句集合，第一次执行返回所有数据，[通用查询语句](#通用查询语句说明)|
|prepare|array|是|无|数据语句集合，每次执行返回所有数据，返回名为total为总查询数量，[通用查询语句](#通用查询语句说明)|
|query|array|是|无|查询语句集合，每次执行返回名为query数据(uuid当前UUID，name显示名称，parent父级UUID)，[通用查询语句](#通用查询语句说明)|
|name|string|是|无|显示名称，可[通用格式化](#通用格式化说明)|
|itype|string|是|operate|模块类型，不可修改|
|menu|array|是|无|右键菜单集合，[通用按钮](#通用按钮说明)|
|uuid|bool|是|无|生成id数量，调用方式<% uuid.第几个 %>|
|back|bool|是|无|是否完成时返回|
|refresh|bool|是|无|是否刷新上级页面|
|import|bool|是|无|是否允许批量导入|
##### 3、替换说明:
|字段|说明|
|:-:|:-|
|<% uuid %>|替换格式化传入参数uuid，多个参数格式化为"'uuid1','uuid2',..."，单个参数格式化为"'uuid1'"|
|<% repeat %>|获取重复字段语句，set后使用，保存在jsonb类型里面|
#### <div id="确认框说明">确认框说明(confirm)</div>
#### <div id="信息说明">信息说明(info)</div>
(待定)
#### <div id="图表说明">图表说明(chart)</div>
(待定)
