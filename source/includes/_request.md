终端用户工单
===
从终端用户的角度而言，定义工单为请求(**request**)

## 请求数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 请求id |
| typeId | string | 否 | 否 | 类型 |
| subject | string | 否 | 否 | 标题 |
| description|string|否|是|第一条回复内容 |
| status | string | 否 | 否 | 状态。系统预定的值有：<br>**OPEN**:未解决<br> **Pending**：等待客户回复<br>**Holding**：等待第三方响应<br> **Solved**:已解决 <br>**Closed**:已关闭 |
| requestorId | string | 是 | 否 | 请求的终端用户 |
| assigneeId | string | 是 |否 | 受理客服 |
| groupId |string | 是 | 否 | 受理工作组 |
| organizationId |string | 否 | 否 | 终端客户组织 |
| channel | [Channel](#工单渠道) | 否 | 否 | 工单渠道信息 |
| ticketFields | hash | 否 | 否 | 自定义字段 |
| createdAt | date | 是 | 否 | 创建日期 |
| updatedAt | date | 是 | 否 | 用户最后更新时间 |

##工单渠道

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| name | string |是 | 是 | 渠道名称 |

>*未完待定*

## 获取请求工单

```http
GET /api/v2/requests/1 HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization: <json web token>
```

```http
HTTP/1.1 200 OK

{
	"id": 1,
	"subject": "ticket subject",
	"description": "ticket description",
	...
}
```

### 请求路径

`GET /api/v2/requests/{id}`
<label class="bulk">BULK</label>
<label class="embed">embed</label> `types` `tags` `organizations` `groups`

## 列举请求

```http
GET /api/v2/requests HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization: <json web token>
```

```http
HTTP/1.1 200 OK

{
	"results":[
		{...}
	],
	"paging":{
		...
	}
}
```

### 请求路径

`GET /api/v2/requests`
<label class="paging">paging</label>
<label class="sort">sort</label>
<label class="include">include</label> `types` `assignees` `groups` `organizations`
<label class="filter">filter</label> `typeId` `assigneeId` `groupId` `organizationId`
<label class="fields">fields</label>


