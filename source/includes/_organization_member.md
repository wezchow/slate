
组织成员
===

## 组织成员数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 自动生成 |
| userId | string | 否 | 是 | 用户id|
| organizationId | string | 否 | 是 | 组织id |
| default | bool | 否 | 是 | 是否为默认组织|
| creator |string | 是 | 是 | 创建者 |
| createdAt | date | 是 | 否 | 创建时间 |
| updatedAt | date | 是 | 否 | 更新时间 |



## 获取组织成员

```http
GET /api/v2/organizations/321300006bd/members?start=0&limit=20 HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8
```

> 响应示例

```http
HTTP/1.1 200 OK

{
	"results":[
		{
			"id":"100023",
			"userId":"123",
			"groupId":"321300006bd",
			...
		}
		...
	],
	"paging":{
		...
	}
}
```

### 请求路径
`GET /api/v2/organizations/{groupId}/members	`

<label class="paging">paging</label>

<label class="include">include</label> `users` 

<label class="sort">sort</label> `createAt` `updateAt`


## 添加组织成员

```http
POST /api/v2/organizations/321300006bd/members HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8

{
	"userId":"123"
}
```

> 批量添加

```http
POST /api/v2/organizations/321300006bd/members HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8

{
	"userIds":["123","124"]
}
```

### 请求路径
`POST /api/v2/organizations/{groupId}/members	`

<label class="bulk">bulk</label> 

###  请求数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| userId | string |否 | 否 | 添加单个成员 |
| userIds | string | 否 | 是 | 批量添加成员|

## 移除组织成员

```http
DELETE /api/v2/organizations/321300006bd/members/123 HTTP/1.1
Host:yourdomain.ruoniu.com
Authorization:bearer <json web token>
Content-Type: application/json; charset=utf-8
```

> 批量移除

```http
DELETE /api/v2/organizations/321300006bd/members?userIds=123,124 HTTP/1.1
...
``` 

将endUser从指定的组织中移除

### 请求路径

`DELETE /api/2/organizations/{groupId}/members/{userId}`

<label class="bulk">bulk</label> 
