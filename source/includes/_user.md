用户
===
[TOC]

用户分为三种角色：

1. endUser, 即终端用户
2. agent, 即客服
3. administrator, 即系统管理员，拥有管理系统的权限


## 所有用户共用数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 创建用户自动生成 |
| name | string | 否 | 是 | 用户名称 |
| roleId | string |否 | 否 | 用户角色，缺省为空表示endUser |
| email | string | 否 | 是 | 用户邮箱 |
| avatarUrl|string|否|否|用户头像|
| createdAt | date | 是 | 否 | 创建日期 |
| updatedAt | date | 是 | 否 | 用户最后更新时间 |
| verified | bool | 否 | 否 | 用户对应的认证方式是否已认证 |
| phone | string | 否 | 否 | 用户手机 |
| ticketRestriction | string | 否 | 否 | 可见工单范围: `"org"`, `"grp"`, `"assigned"`, `"requested"`, `null` |
|identities|identify array|否|否|用户认证方式信息|
| userFields | hash | 否 | 否 | 自定义字段 |

### identify
| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| providerName | string |是 | 是 | oauth2, ssojwt |
| providerId | string | 否 | 否 | 用户名称 |
| accessToken | string | 否 | 否 | oauth2专用 |
| refreshToken | string | 否 | 否 | oauth2专用 |
| expiresInSeconds | int | 否 | 否 | accessToken过期时间 |
| userId | string | 否 | 否 | 此认识方式的唯一标识 |


## endUser的数据格式
| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |


## agent和administrator的数据格式
| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |


## 获取单个用户

> 请求示例

```http
GET /api/v2/users/321300006bd HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization: bearer <json web token>
```

> 响应示例

```http
HTTP/1.1 200 OK
Content-Type:application/json

{
	"id":"321300006bd",
	"email":"email@company.com",
	"name":"user name",
	...
}
```

### 请求路径

`GET /api/v2/users/{userId}`

<label class="buld">BULK</label>
<label class="embed">embed</label>

### 查询参数

名称 | 取值
--------- | ----------- | ----------- | -----------
embed |role,organization,group



## 列举用户

> 请求示例

```http
GET /api/v2/users?start=0&limit=20 HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type:application/json
```

> 响应示例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
	"results":[...],
	"paging":{
		"next":"/api/v2/users?start=20&limit=20",
        "count":100,
        "limit":20,
        "start":0
	}
}
```

<label class="paging">paging</label>

<label class="sort">sort</label> `createdAt` `updatedAt`

<label class="include">include</label> `role`  

<label class="fields">fields</label> 

<label class="filter">filter</label> `role=endUser`  `role=!endUser` `role=admin` `role=agent` 

## 创建用户

> 请求示例

```http
POST /api/v2/users HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json

{
	"email":"email@company.com",
	"name":"user nickname",
	"password":"aoiwezi230Xwe_+*",
	"roleId":"agent"
}
```

> 响应示例

```http
HTTP/1.1 201 Created
Location:/api/v2/users/321300006bd
Content-Type: application/json

{
	"id":"321300006bd",
	"email":"email@company.com",
	"nickname":"user nickname",
	"roleId":"agent"
}
```

### 请求路径

`POST /api/v2/users `

### 请求体字段
参考[用户格式](#所有用户共用数据格式)，除此之外，还可以指定以下字段：

字段 | 类型|必填|描述
--------- | ----------- | -----------| -----------
password | string | 否|用户密码，如果设置，则邮箱默认将被设置为已验证，且不发送邮件给用户


### 错误码

HttpStatus | ApiCode| 描述
--------- | ----------- | -----------
400 |11000| email 已被注册
400 |11001| roleId 角色不存在


## 更新用户

> 请求示例

```http
PUT /api/v2/users/321300006bd HTTP/1.1
Content-Type: application/json

{
	"nickname":"Mr Wang",
	...
}
```

> 响应示例

```http
HTTP/1.1 200 Ok
Content-Length: 28

{
	"name":"Mr Wang",
	"updatedAt":1433670249,
	...
}
```

### 请求头

`PUT /api/v2/users/{userId}`
<label class="patch">PATCH</label>

### 请求体字段

参见 [创建用户](#创建用户)

### 错误码

HttpStatus | ApiCode| 描述
--------- | ----------- | -----------
400 |10000| 域名已被使用

<label class="patch">PATCH</label>
<label class="bulk">BULK</label>

## 更新用户密码

如果更新的用户是当前授权用户，需要提供oldpassword，管理员可以设置agent, endUser的密码，无需提供oldpassword，设置其它人的密码需要开启此项功能

> 请求示例

```http
PUT /api/v2/user/321300006bd/password HTTP/1.1
Authorization bearer <json web token>

{
	"oldpassword":"abc123",
	"password":"123abc"
}
```

### 请求路径

`PUT /api/v2/users/{uid}/password HTTP/1.1`

### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | ----------- | -----------
password |string| 是|新密码
oldpassword |string| 否| 旧密码


## 删除用户

```http
DELETE /api/v2/users/321300006bd HTTP/1.1
Authorization:bearer <json web token>
```

```http
HTTP/1.1 204 No Content
```
### 请求路径
`DELETE /api/v2/users/{uid} HTTP1.1`
<label class="bulk">BULK</label>