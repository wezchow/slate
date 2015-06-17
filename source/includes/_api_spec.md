# 客户支持API规范

## 请求方法及响应

方法|描述 |响应
-----|---|---
GET|获取资源，如获取ticket|200，返回请求的资源体
POST|创建资源，如创建ticket|201，返回创建的资源体
PUT|整体更新资源，如更新ticket|200，返回更新后的资源体
PATCH|部分更新资源，如更新ticket的subject|200，返回更新后的资源体。支持PATCH的接口将标记 <label class="patch">PATCH</label>
DELETE|删除资源|204，返回空


## HTTP响应状态码

状态码|描述
-----|---
200|GET,PUT,PATCH返回，表示请求成功
201|POST返回，表示创建了新的资源
204|DELETE返回，表示删除了资源
400|PUT,PATCH,POST返回，表示请求内容格式有误，不符合指定的要求，例如非法的JSON结构体
401|用户认证失败，例如token缺失，type错误，过期等
403|用户认证成功，但是没有相应的操作权限
404|请求的资源不存在
422|不能处理的请求，例如，上传的文件格式，大小不合要求，Required字段不在请求体中
500|服务端错误

## 请求HTTP头

### Content-Type
如无特别说明，所有请求及返回的Content-Type皆为application/json。
### Authorization
如无特别说明，所有的请求都要包含以下的Authorization
 `bearer <json web token>`

## 变量命名规则
使用驼峰式,首字符小写，例如使用`createdAt`而不是`created_at`。虽然后者有利用人眼阅读，但为了兼容js的命名规范使用前者。

## 嵌入文档

支持嵌入文档将会标记
<label class="embed">embed</label>
>默认获取Ticket的返回格式如下

```json
{
	"id":1,
	"userId":"aiw29300",
	...
}
```

>通过在url中指定`embed=user` ,可获取以下形式

```json
{
	"id":1,
	"user":{
		"id":"aiw29300",
		"avatarUrl":"https://www.domain.com/avatarUrl",
		...
	}
}
```

## List接口

### 分页

> 分页请求示例

```http
GET /api/v2/tickets?start=40,limit=20 HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```

> 分页响应示例

```http
HTTP/1.1 200 OK
Content-Type:application:json


{
	results:[
		{...},
		{...},
	],
	paging:{
		previous: "/api/v2/tickets?start=20,limit=20",
		next: "/api/v2/tickets?start=60,limit=20",
		count:100,
		limit:20,
		start:40
	}
}
```

并非所有list接口都会分页，例如工单类型，优先级等就不会分页。
如果分页会在文档中明确说明。对于分页的list接口，应指定以下两个查询参数
1. **start**,启始位置
2. **limit**,限制的返回条目数

支持分页将会标记
<label class="paging">paging</label>

### 指定字段
通过fields查询参数指定需要列出的字段
`GET /api/v2/tickets?fields=subject`

> 指定字段请求示例

```http
GET /api/v2/tickets?fields=subject,createdAt  HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```

>  指定字段响应示例

```http
HTTP/1.1 200 OK
Content-Type:application/json


{
	results:[
		{subject:"ticket subject"}
	],
	...
}
```

支持指定字段将会标记
<label class="fields">fields</label>

### 排序

查询参数`sort` 指定排序字段，`-` 指定排序方式
例如:

> 按*createdAt*倒排序请求示例

```http
GET /api/v2/tickets?sort=-createdAt  HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```


支持排序字段将会标记
<label class="sort">sort</label>

### 过滤
以`key`=`value`形式查询参数作为过滤条件

> 过滤`status=open` 请求示例

```http
GET /api/v2/tickets?status=open  HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```

支持过滤将会标记
<label class="filter">filter</label>

### 包含

> include请求示例

```http
GET /api/v2/tickets?include=users,tags  HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```
>include 响应示例

```http
HTTP/1.1 200 OK
Content-Type:application/json

{
	results:[
		{...}
	],
	users:[
		{...}
	],
	tags:[
		{...}
	]
}
```

查询参数include指定需要包含的引用对像。

支持包含将会标记
<label class="include">include</label>

## 批量操作
支持的请求方法包含`GET`,` PUT`, `DELETE`,`PATCH`

> 请求示例

```http
GET /api/v2/tickets?ids=1,2  HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```

>响应示例

```http
HTTP/1.1 200 OK 
Content-Type:application/json

{
	data:[
		{
			id:1,
			...
		},{
			id:2,
			...
		}
	]
}
```

支持批量将会标记
<label class="bulk">bulk</label>

