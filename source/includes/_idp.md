# 用户认证

## 用户注册

```
POST /signup 
Content-Type:application/json

{
	"email":"example@company.com"
}
```

> 用户注册成功会发送用户激活URL至提供的邮箱，URL中包含用激活接口需要的code

## 用户激活

```
POST /activate
Content-Type:application/json

{
	"email":"email@company.com",
	"code":"iwe3rlmvo93raaefi19",
	"password":"<password>"
}



HTTP/1.1 200 
Content-Type:application/json

{
	"jwt":"<json web token>",
	"userInfo":"..."
}
```


## 用户登录

```
POST /login
Content-Type:application/json

{
	"email":"email@company.com",
	"password":"<password>"
}



HTTP/1.1 200 
Content-Type:application/json

{
	"jwt":"<json web token>",
	"userInfo":"..."
}
```