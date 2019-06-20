# 客户端 - 用户相关

## 用户登录或者注册
### HTTP 请求

- POST `/v1/user/login`

```json
{
  "mobile": "13777777777",
  "national_code": "+86",
  "verify_code": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| -----------   | ------- | ------ | ----- | -----------
| mobile        | true    | string | NA    | 手机号
| national_code | true    | string | +86   | 国家地区
| verify_code    | true    | string | NA    | 验证码
| invite_code    | false    | string | NA    | 邀请码
| nick    | false    | string | NA    | 邀请码

> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "national_code": "86",
    "mobile": "13777777777",
    "status": "active",
    "ctime": 1494901162595,
    "ltime": 1494901162595,
    "first": true,
    "sign_salt": "67043894549786794",
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| uid          | true    | long   | 用户 ID     |         |
| name         | true    | string | 用户姓名     |         |
| national_code  | true    | string | 国家地区     |        
| mobile       | true    | string | 手机号       |         |
| status       | true    | int | 用户状态     | 1, 2, 3, 4 |
| exchanger    | true    | int   | 是否是承兑商  | 0不是 1是  2审核中   
| ctime        | false   | long   | 用户创建时间  |         |
| utime        | false   | long   | 用户更新时间  |         |
| ltime        | false   | long   | 用户登陆时间  |         |
| first     | false | bool | 是否第一次登录 | true是 |
| sign_salt    | true    | string | 签名的盐     |         |

- 用户状态定义： 

| 状态       | 描述  |
| --------- | ----- |
| 1    | 激活   |
| 2   | 审核中 |
| 3  | 禁用   |
| 4   | 删除   |


## 用户更新token
### HTTP 请求

- POST `/v1/user/relogin`


### 请求参数
无

> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "national_code": "86",
    "mobile": "13777777777",
    "status": "active",
    "ctime": 1494901162595,
    "ltime": 1494901162595,
    "first": true,
    "sign_salt": "67043894549786794",
  }
}
```


## 获取用户信息

### HTTP 请求

- GET `/v1/user/info`

> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "national_code": "86",
    "mobile": "13777777777",
    "status": 1,
    "exchanger": 0,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595
  }
}
```

### 响应数据
返回当前用户对象。

## 更新用户信息
### HTTP 请求

- PUT `/v1/user/info`

```json
{
  "name": "姓名",
}
```

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| name     | true    | string | NA    | 用户姓名

> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "countrycode": "+86",
    "mobile": "13777777777",
    "status": "active",
    "exchanger": false,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回当前用户对象。


## 用户签名认证登录
### HTTP 请求

- POST `/v1/user/sign`

```json
{
	"uid": "166717822901157888",
	"timestamp": 1554627817,
	"signature":"eb4bd8ebba6c63457cb16811d67a909b"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| uid         | true    | string | NA    | 用户uid
| timestamp   | true    | long   | NA    | 同步的服务端系统时间
| signature   | true    | string | NA    | 加密后的签名

- 签名加密规则(md5加密两次)

```text
  source = md5(timestamp{同步的服务端系统时间}uid{用户id}timestamp{同步的服务端系统时间})
  签名 = md5({source}+{签名的盐：sign_salt})
  eg:
  source = "timestamp1554629465uid166717822901157888timestamp1554629465"
  sign_salt = "67043894549786794"
  signature = md5(md5(source) + sign_salt)
```


> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "national_code": "86",
    "mobile": "13777777777",
    "status": "active",
    "sign_salt": "67043894549786794",
    "ctime": 1494901162595,
    "ltime": 1494901162595,
    "first": true
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| uid          | true    | long   | 用户 ID     |         |
| name         | true    | string | 用户姓名     |         |
| national_code  | true    | string | 国家地区     |        
| mobile       | true    | string | 手机号       |         |
| status       | true    | int | 用户状态     | 1, 2, 3, 4 |
| exchanger    | true    | int   | 是否是承兑商  | 0不是 1是     
| ctime        | false   | long   | 用户创建时间  |         |
| utime        | false   | long   | 用户更新时间  |         |
| ltime        | false   | long   | 用户登陆时间  |         |
| first        | false   | bool   | 是否第一次登录 | true是 |
| sign_salt    | true    | string | 签名的盐     |         |


- 用户状态定义： 
| 状态       | 描述  |
| --------- | ----- |
| 1    | 激活   |
| 2   | 审核中 |
| 3  | 禁用   |
| 4   | 删除   |


## 获取用户设置
### HTTP 请求

- GET `/v1/user/setting`

> Response:

```json
{
    "code": 200,
    "data": {
        "uid": 168909270450962432,
        "wealth_notice": true,
        "order_notice": true
    }
}
```

## 获取用户设置
### HTTP 请求

- POST `/v1/user/setting`

```json
{
    "wealth_notice": true,
    "order_notice": true
}
```
### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| wealth_notice  | true| bool | false    | 资产通知
| order_notice   | true| bool   | false | 新订单通知

> Response:

```json
{
    "code": 200
}
```

