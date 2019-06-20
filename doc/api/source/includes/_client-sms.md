# 客户端 - 验证码

## 发送验证码

向指定的手机号码发送短信验证码。

### HTTP 请求

- POST `/v1/sms/sendcode`

```json
{
  "national_code": "86",
  "action": "login",
  "mobile": "13777777777"
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| -------------- | ------- | -----  | ----- | -----------
| national_code  | true    | string | NA    | 国家代码(如美国：+1)或地区代码(如香港：+852)
| mobile  		 | true    | string | NA    | 目标手机号
| action  		 | true    | string | NA    | 验证目的动作
| invite_code    | true    | string | NA    | 邀请码(action=login时首次登陆需要邀请码)

#### action 动作定义：

| 动作 | 描述 |
| ----------------------- | ----------- |
| login                   | 登录或者注册 |
| payment                 | 添加修改支付方式 |
| 2-step                  | 支付两步验证 |
| change-mobile           | 更换手机号   |
| change-payment-password | 修改支付密码   |

> Response:

```json
{
    "code": 200,
    "data": {
        "first": true
    }
}
```

### 响应数据

返回是否首次登陆,first=true需要带邀请码重新请求验证码。

## 登录账号请求发送验证码

向登录账号的手机号码发送短信验证码。

### HTTP 请求

- POST `/v1/sms/usersendcode`

```json
{
  "action": "login"
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| -------------- | ------- | -----  | ----- | -----------
| action  		 | true    | string | NA    | 验证目的动作

> Response:

```json
{
    "code": 200
}
```


