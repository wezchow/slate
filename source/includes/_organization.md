组织
===

一个用户可以属于一个或多个组织，反过来，一个组织也可以包含一个或多个用户。如果一个用户属于多个组织，需要指定一个为其默认组织。

一个组织可以与一个工作组关联起来，这样来自此组织的工单将会被自动分配给被关联起来的工作组。

另外，可以设置组织内的其它用户共享该组织的工单。

## 组织数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 自动生成 |
| name | string |否 | 是 | 组织名称 |
| groupId | string | 否 | 否 | 关联的工作组 |
| description | string | 否 | 否 | 工作组描述 |
| domain | string | 否 | 否 | 组织域名，邮件域名与此域名一至的用户自动归入此组织 |
| tagsId | string array | 否 | 否 | 标签，来自此组织的工单自动被添加这些标签 |
| shareTickets |bool | 否 | 否 | 此组织的工单可以被组织内其它成员查看 |
| shareReply |bool | 否 | 否 | 组织内其它成员可回复工单 |
| creator |string | 是 | 否 | 创建者 |
| createdAt | date | 是 | 否 | 创建时间 |
| updatedAt | date | 是 | 否 | 更新时间 |

## 获取组织

> 请求示例

```http
GET /api/v2/organizations/321300006bd HTTP/1.1
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
	"name":"momo",
	...
}
```


> 批量获取

```http
GET /api/v2/organizations?id=org1,org2 HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8
```

```http
HTTP/1.1 200 OK

{
	"results":[...]
}
```

### 请求路径

`GET /api/v2/organizations/{organizationsId}`

<label class="bulk">BULK</label>

<label class="embed">embed</label> `groups` `tags`

## 列举组织

> 请求示例

```http
GET /api/v2/organizations HTTP/1.1
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
`GET /api/v2/organizations`

<label class="paging">paging</label>

<label class="include">include</label> `groups` `tags`

<label class="sort">sort</label> `createAt` `updateAt`

<label class="filter">filter</label> `name` `domain`

## 创建组织
> 请求示例

```http
POST /organizations HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json

{
	"name":"qiniu",
	"domain":"qiniu.com",
	"description":""
}
```

> 响应示例

```http
HTTP/1.1 201 Created
Location:/api/v2/organizations/321300006bd
Content-Type: application/json

{
	"id":"321300006bd",
	"name":"qiniu",
	"description":"",
	...
}
```

### 请求路径

`POST /api/v2/organizations `

### 请求体字段

参见 [组织数据格式](#组织数据格式)

## 更新组织

> 请求示例

```http
PUT /api/v2/organizations/321300006bd HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8

{
	"description":"details",
	...
}
```

> 响应示例

```http
HTTP/1.1 200 Ok

{
	"id":"321300006bd",
	"description":"details",
	...
}
```

### 请求路径

`PUT /api/v2/organizations/{organizations}`

<label class="patch">PATCH</label>

### 请求体字段

参见 [组织数据格式](#组织数据格式)


## 删除组织

> 请求示例

```http
DELETE /api/v2/organizations/321300006bd HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```

> 响应示例

```http
HTTP/1.1 204 No Content
```

> 批量删除请求示例

```http
DELETE /api/v2/organizations?ids=org1,org2 HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
```


### 请求路径

`DELETE /api/v2/organizations/{organizationId}`

<label class="patch">bulk</label>


