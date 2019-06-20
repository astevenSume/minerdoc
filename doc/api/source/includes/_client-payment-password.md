# 客户端 - 用户支付密码
## 通过验证码设置用户支付密码

### HTTP 请求

- POST `/v1/payment-password/setpassword`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| method     | true    | int    | NA    | 设置支付密码方式: 1:旧密码方式设置, 2:短信验证码方式设置
| verify_code| false   | string | NA    | 手机验证码: (method为短信验证码方式时设置必填)
| oldpwd     | false   | string | NA    | 旧支付密码： (method旧密码方式设置时必填)
| newpwd     | true    | string | NA    | 新支付密码


- method 设置支付密码方式

| 状态       | 定义    |
| ----------| ------  |  
| 1         | 旧密码方式设置
| 2         | 短信验证码方式设置


> Response:

```json
{  
  "data": {
      "sign_salt": "123131331",
      "status": 1,
      "verify_step": 0
  }
}
```
### 响应数据

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| -------   | ------- | ------ | ----- | -----------
| sign_salt | true    | string | NA    | 支付密码的盐，客户端保存用于指纹支付等生物认证
| status    | true    | int    | 支付密码状态 |  0，1,2  |
| verify_step | true    | int  | 是否支持二次验证 |  0，1 |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 未设置  |
| 1         | 可用    |
| 2         | 停用   |

- verify_step 是否支持二次验证

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 仅密码验证  |
| 1         | 支持二次验证    |


## 获取用户支付密码状态

### HTTP 请求

- GET `/v1/payment-password/status`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------

> Response:

```json
{  
  "data": {
    "status": 1,
    "verify_step": 0,
	"is_lock":true,
	"lock_second":300,
	"fail_cnt":300,
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| status       | true    | int    | 支付密码状态 |  0，1,2  |
| verify_step  | true    | int  | 是否支持二次验证 |  0，1 |
| is_lock      | true    | bool | true:锁定  |  0，1 |
| lock_second  | true    | int  | 锁定倒计时 秒 |  0，1 |
| fail_cnt     | true    | int  | 失败次数   |  0，1 |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 未设置  
| 1         | 可用
| 2         | 停用   
 
 - verify_step 是否支持二次验证

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 仅密码验证  |
| 1         | 支持二次验证    |


## 设置是否二次验证

### HTTP 请求

- POST `/v1/payment-password/setverifystep`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 |
| ------- | ------- | ------ | ----- | -----------|
| verify_step | true    | int  | 是否支持二次验证 |  0，1 |
| token     | true    | string | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码，开启二次认证时为必填字段 | action: change-payment-password  |

```json
{
	"verify_step": 1,
	"token": "518358864332464",
	"verify_code": "123123"
}

```
 - verify_step 是否支持二次验证

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 仅密码验证  |
| 1         | 支持二次验证    |

> Response:

```json
{  
  "data": {
    "status": 1,
    "verify_step": 0
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| status       | true    | int    | 支付密码状态 |  0，1,2  |
| verify_step | true    | int  | 是否支持二次验证 |  0，1 |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 未设置  
| 1         | 可用
| 2         | 停用   
 
 - verify_step 是否支持二次验证

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 仅密码验证  |
| 1         | 支持二次验证    |



## 生成验证token信息（通过支付密码生成）

### HTTP 请求

- POST `/v1/payment-password/verifybypassword`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 |
| ------- | ------- | ------ | ----- | -----------|
| password | true   | string  | 支付密码 |     |

```json
{
	"password": "123456"
}
```

> Response:

```json
{
    "code": 200,
    "data": {
        "token": "476994147418504",
        "sign_salt": "249485747328026",
        "verify_step": 0
    }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| token       | true    | int    | 支付密码状态 |  用于二次认证的token  |
| verify_step | true    | int    | 是否支持二次验证 |  0，1 |
| sign_salt   | true    | string | NA    | 支付密码的盐，客户端保存用于指纹支付等生物认证 |

 - verify_step 是否支持二次验证

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 仅密码验证  |
| 1         | 支持二次验证    |

## 生成验证token信息（通过签名认证生成）

### HTTP 请求

- POST `/v1/payment-password/verifybysign`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 |
| ------- | ------- | ------ | ----- | -----------|
| timestamp   | true    | long   | NA    | 同步的服务端系统时间
| signature   | true    | string | NA    | 加密后的签名

```json
{
	"signature": "dc943ddf7b2ed4d29c59d7a86d77340f",
	"timestamp": 1554868412
}
```

> Response:

```json
{
    "code": 200,
    "data": {
        "token": "476994147418504",
        "sign_salt": "249485747328026",
        "verify_step": 0
    }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| token       | true    | int    | 支付密码状态 |  用于二次认证的token  |
| verify_step | true    | int    | 是否支持二次验证 |  0，1 |
| sign_salt   | true    | string | NA    | 支付密码的盐，客户端保存用于指纹支付等生物认证 |

 - verify_step 是否支持二次验证

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 仅密码验证  |
| 1         | 支持二次验证    |
