工单
===
从终端用户的角度而言，工单即为请求(**request**)
对客服而言，终端用户的请求即为工单(**ticket**)

## 请求数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 工单id |
| typeId | string | 否 | 否 | 工单类型 |
| subject | string | 否 | 否 | 工单标题 |
| description|string|否|是|工单第一条回复内容 |
| status | string | 否 | 否 | 工单状态。系统预定的值有：<br>**OPEN**:未解决<br> **Pending**：等待客户回复<br>**Holding**：等待第三方响应<br> **Solved**:已解决 <br>**Closed**:已关闭 |
| requestorId | string | 是 | 否 | 请求工单的终端用户 |
| assigneeId | string | 是 |否 | 受理客服 |
| groupId |string | 是 | 否 | 受理工作组 |
| organizationId |string | 是 | 否 | 终端客户默认组织 |
| channel | [Channel](#工单渠道) | 否 | 否 | 工单渠道信息 |
| ticketFields | hash | 否 | 否 | 自定义字段 |
| createdAt | date | 是 | 否 | 创建日期 |
| updatedAt | date | 是 | 否 | 用户最后更新时间 |


## 工单数据格式

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| id | string |是 | 否 | 工单id |
| typeId | string | 否 | 否 | 工单类型 |
| tagsId | string array | 否 | 否 | 工单标签 |
| subject | string | 否 | 否 | 工单标题|
| description|string|否|是|工单第一条回复内容|
| status | string | 否 | 否 | 工单状态。系统预定的值有：<br>**OPEN**:未解决<br> **Pending**：等待客户回复<br>**Holding**：等待第三方响应<br> **Solved**:已解决 <br>**Closed**:已关闭 |
| priority | string | 否 | 否 | 优先级，取值：**normal**,**important**,**urgent**|
| requestorId | string | 否 | 否 | 工单请求用户 |
| submitterId | string | 否 | 否 | 工单提交者(代理终端用户提交工单) |
| organizationId | string | 是 | 否 | 工单请求用户的默认组织 |
| channel | [Channel](#工单渠道) | 否 | 否 | 工单渠道信息 |
| ticketFields | hash | 否 | 否 | 自定义字段 |
| createdAt | date | 是 | 否 | 创建日期 |
| updatedAt | date | 是 | 否 | 用户最后更新时间 |

##工单渠道

| 字段名 | 类型 | 只读 | 必须 | 描述 |
| --- | --- | --- | --- | --- |
| name | string |是 | 是 | 渠道名称 |

>*未完待续*

## 获取单个工单

> 客服

```http
GET /api/v2/tickets/1 HTTP/1.1
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

> 终端用户

```http
GET /api/v2/requests/1 HTTP/1.1
Host: yourdomain.ruoniu.com
Authorization: <json web token>
```

```http
HTTP1.1 200 OK

{
	"id": 1,
	"subject": "ticket subject",
	"description": "ticket description",
	...
}
```

### 请求路径

**客服**
`GET /api/v2/tickets/{id}`
<label class="bulk">BULK</label>
<label class="embed">embed</label> `type` `tags` `organization`

**终端用户**
`GET /api/v2/requests/{id}`
<label class="bulk">BULK</label>
<label class="embed">embed</label> `type` `tags` `organization`

