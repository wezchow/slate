工作组
===

一个客服可以属于多个工作组，反过来，一个工作组可以包含多个客服。
工单可以分配给一个工作组，并限制其仅在工作组内可见。

## 工作组数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 自动生成 |
| name | string | 否 | 是 | 工作组名称|
| description | string | 否 | 否 | 工作组描述 |
| creator |string | 是 | 否 | 创建者 |
| createdAt | date | 是 | 否 | 创建时间 |
| updatedAt | date | 是 | 否 | 更新时间 |

## 获取工作组

> 请求示例

```http
GET /api/v2/groups/321300006bd HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8
```

> 响应示例

```http
HTTP/1.1 200 OK
Content-Type:application/json

{
	"id":"321300006bd",
	"name":"售前",
	...
}
```

### 请求路径

`GET /api/v2/groups/{groupId}`

<label class="bulk">BULK</label>

## 列举工作组

> 请求示例

```http
GET /api/v2/groups HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8
```

> 响应示例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
	"results":[...]
}
```
### 请求路径
`GET /api/v2/groups`

## 创建工作组
> 请求示例

```http
POST /groups HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json

{
	"name":"售前"，
	"description":"",
}
```

> 响应示例

```http
HTTP/1.1 201 Created
Location:/api/v2/groups/321300006bd
Content-Type: application/json

{
	"id":"321300006bd",
	"name":"售前",
	"description":"",
	...
}
```

### 请求路径

`POST /api/v2/groups `

### 请求体字段
参考[工作组数据格式](#工作组数据格式)


## 更新工作组

> 请求示例

```http
PUT /api/v2/groups/321300006bd HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8

{
	"description":"售前工单处理组",
	...
}
```

> 响应示例

```http
HTTP/1.1 200 Ok

{
	"id":"321300006bd",
	"name":"售前",
	"description":"售前工单处理组",
	...
}
```

### 请求路径

`PUT /api/v2/groups/{groups}`

<label class="patch">PATCH</label>

### 请求体字段

参见 [工作组数据格式](#工作组数据格式)


## 删除工作组

> 请求示例

```http
DELETE /api/v2/groups/321300006bd HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```

> 响应示例

```http
HTTP/1.1 204 No Content
```

### 请求路径

`DELETE /api/v2/groups/{groupId}`

<label class="patch">bulk</label>


