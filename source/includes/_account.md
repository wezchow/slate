# 云客服平台帐号

[toc]
	
## 申请创建帐号

> 请求示例

```http
POST /account/apply HTTP/1.1
Host: ruoniu.com
Content-Type: application/json

{
	"email":"youremail@company.com"
}
```

> 响应示例

```http
HTTP/1.1 200 OK
```

> 系统会向申请创建帐号的邮箱发送创建帐号的URL，其中包含创建帐号所需要的code

### 请求路径

`POST /account/apply `

### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | -----------| -----------
email | string | 是|创建帐号的email


## 创建帐号

> 请求示例

```http
POST /account HTTP/1.1
Content-Type: application/json

{
	"slug":"qiniu", 
	"title":"七牛云存储", 
	"code":"<code>", 
	"username":"", 
	"password":"<password>" 
}
```

> 响应示例

```http
HTTP/1.1 201 Created
Content-Length: 28

{
	"token":"<json web token>"
}
```

### 请求路径

`POST /account`

### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | ----------- | -----------
slug |string| 是|系统默认分配域名 https://`<slug>`.ruoniu.com
title |string| 是| 公司名称
code |string| 是| 较验码
username |string| 是| 用户名
password |string| 是|密码

### 错误码

Http Status Code | Api Code| 描述
--------- | ----------- | -----------
400 |10000| 域名已被使用

## 品牌设置

> 请求示例

```http
PUT /account/branding HTTP/1.1
Content-Type: application/json
Host:yourdomain.ruoniu.com
Authorization:"bearer <json web token>"

{
	"title":"七牛云存储", 
	"logoUrl":"https://dn-ruoniu.qbox.me/5512e5b213b3434f8c000004",
	"faviconUrl":"https://dn-ruoniu.qbox.me/5512e5b213b3434f8c000004",
	"website":"www.yourdomain.com",
	"slogan":"简单，可信赖"
}
```
### 请求路径
`PUT /account/branding`<label class="patch">PATCH</label>
### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | ----------- | -----------
title |string| 是|公司名称
logoUrl |string| 否| 公司logo，在终端用户页面显示
faviconUrl |string| 否| 公司favicon，所有页面显示
website |string| 否| 用户网站
slogan |string| 否|公司口号，页面加载时显示

## 更新用户名密码登录方式

> 请求示例

```http
PUT /account/identify/usernamepassword HTTP/1.1
Content-Type: application/json
Host:yourdomain.ruoniu.com
Authorization:"bearer <json web token>"

{
	"type":"endUser",
	"loginEnabled":true,
	"signupEnabled":true,
	"passwordPolicy":"low",
	"signupEmailTpl":"",
	"forgotEmailTpl":"",
	"expiresInMinute":43200
}
```

### 请求路径
`PUT /account/identify/usernamepassword`

### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | ----------- | -----------
type |string| 是| 用户类型，取值endUser或agent
loginEnabled |bool| 否| 是否允许登录
signupEnabled |bool| 否| 是否允许注册，对agent无效
passwordPolicy |string| 否| 密码策略，取以下值：<br/>**none**:非空必填<br/>**low**:6个任意字符（默认值）<br/>**fair**:至少8字符，至少包含一个大写，一个小写，一个数字<br>**good**:在fair的基础上，至少包含一个特殊字符!@#$%^&*()-=+
signupEmailTpl |string| 否| 用户注册邮件模板
forgotEmailTpl |string| 否| 忘记密码邮件模板
expiresInMinute |string| 否|登录签发token的有效期

## 添加OAuth2.0登录方式

> 请求示例

```http
PUT /account/identify/oauth2 HTTP/1.1
Content-Type: application/json
Host:yourdomain.ruoniu.com
Authorization:"bearer <json web token>"

{
	"name":"qiniu",
	"type":"endUser",
	"logoUrl":"https://dn-ruoniu.qbox.me/5512e5b213b3434f8c000004",
	"clientId":"wh1qSmv0VGC1vM0SIBsdLgih",
	"secretId":"edP5HxBZ2fjstjFIJqODzU6IL******",
	"authUrl":"https://portal.qiniu.com/oauth/authorize",
	"scope":"user:email",
	"tokenUrl":"https://portal.qiniu.com/oauth/token",
	"userInfoUrl":"https://portal.qiniu.com/api/account/info",
	"userInfoMapping":"email:data.email",
	"enabled":true
}
```
> 返回示例

```http
HTTP/1.1 201 Created
Location:https://yourdomain.ruoniu.com/api/v2/account/identify/oauth2/5512e50001
Content-Type:application/json

{
	"id":"5512e50001",
	"name":"qiniu",
	"type":"endUser",
	"logoUrl":"https://dn-ruoniu.qbox.me/5512e5b213b3434f8c000004",
	"clientId":"wh1qSmv0VGC1vM0SIBsdLgih",
	"secretId":"edP5HxBZ2fjstjFIJqODzU6IL******",
	"authUrl":"https://portal.qiniu.com/oauth/authorize",
	"scope":"user:email",
	"tokenUrl":"https://portal.qiniu.com/oauth/token",
	"userInfoUrl":"https://portal.qiniu.com/api/account/info",
	"userInfoMap":"email:data.email",
	"enabled":true,
	"creator":"5538b43513b3431619001698",
	"createAt":1433490673,
	"updatedAt":1433490673
}
```


### 请求路径
`POST /account/identify/oauth2`

### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | ----------- | -----------
name |string| 是| 名称，如GitHub, Weibo
logoUrl |string| 否| 登录图标
clientId |string| 是| OAuth2 ClientId
secretId |string| 是| OAuth2 SecretId
authUrl |string|是| OAuth2 Auth Url
scope |string| 是| 授权范围
tokenUrl | string| 是| 交换token Url
userInfoUrl | string|是 |获取用户信息 Url
userInfoMap | string|否 |用户信息映射关系描述，至少需要指明email,userId字段的映射关系，不指定表明使用默认映射关系，即**email:email,userId:userId**
enabled |bool| 是| 是否启用


## 更新OAuth2.0登录方式

> 请求示例

```http
PATCH /account/identify/oauth2/5512e50001 HTTP/1.1
Content-Type: application/json
Host:yourdomain.ruoniu.com
Authorization:"bearer <json web token>"

{
	"enabled":false
}
```
> 返回示例

```http
HTTP/1.1 200 OK
Location:https://yourdomain.ruoniu.com/api/v2/account/identify/oauth2/5512e50001
Content-Type:application/json

{
	"name":"qiniu",
	"type":"endUser",
	"logoUrl":"https://dn-ruoniu.qbox.me/5512e5b213b3434f8c000004",
	"clientId":"wh1qSmv0VGC1vM0SIBsdLgih",
	"secretId":"edP5HxBZ2fjstjFIJqODzU6IL******",
	"authUrl":"https://portal.qiniu.com/oauth/authorize",
	"scope":"user:email",
	"tokenUrl":"https://portal.qiniu.com/oauth/token",
	"userInfoUrl":"https://portal.qiniu.com/api/account/info",
	"userInfoMapping":"email:data.email",
	"enabled":false,
	"creator":"5538b43513b3431619001698",
	"createAt":1433490673,
	"updatedAt":1433590673
}
```

### 请求路径
`PUT /account/identify/oauth2/{id}`
<label class="patch">PATCH</label>

### 请求体字段

参考添加OAuth2.0登录方式请求体字段

## 删除OAuth2.0登录方式

### 请求路径
`DELETE /account/identify/oauth2/{id}`


> 请求示例

```http
DELETE /account/identify/oauth2/5512e50001 HTTP/1.1
Content-Type: application/json
Host:yourdomain.ruoniu.com
Authorization:"bearer <json web token>"
```
> 返回示例

```http
HTTP/1.1 204 No Content
```

## 更新JWT 单点登录

> 请求示例

```http
PUT /account/identify/sso/jwt HTTP/1.1
Content-Type: application/json
Host:yourdomain.ruoniu.com
Authorization:"bearer <json web token>"

{
	"type":"endUser",
	"enabled":true,
	"signUrl":"https://www.yourdomain.com/login",
	"signoutUrl":"https://www.yourdomain.com/login"
}
```

### 请求路径
`PUT /account/identify/sso/jwt`

<label class="patch">PATCH</label>

### 请求体字段

字段 | 类型|必填|描述
--------- | ----------- | ----------- | -----------
type |string| 是| 用户类型，取值endUser或agent
enabled |bool| 否| 是否启用
signUrl |bool| 否| 用户登录地址
logoutUrl |bool| 否| 登出跳转地址