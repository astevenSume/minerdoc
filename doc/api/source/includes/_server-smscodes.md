# 服务端 - 短信验证码管理
## 获取所有短信验证码

### HTTP 请求

- GET `/v1/admin/smscodes`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "mobile": "13777777777",
        "action": "login",
        "code": "987654",
        "status": "active",
        "ctime": 1494901162595,
        "etime": 1494901162595
      },
      {
        "id": "123456790",
        "mobile": "13777777777",
        "action": "change-mobile",
        "code": "478912",
        "status": "expired",
        "ctime": 1494901162595,
        "etime": 1494901162595
      }
    ],
    "meta": {
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    }
  }
}
```

## 获取短信验证码

### HTTP 请求

- GET `/v1/admin/smscodes/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 短信验证码 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "mobile": "13777777777",
    "action": "login",
    "code": "987654",
    "status": "active",
    "ctime": 1494901162595,
    "etime": 1494901162595
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 短信验证码 ID    |         |
| mobile    | true    | string | 目标手机号        |        |
| action    | true    | string | 验证目的动作      |        |
| code      | true    | string | 短信验证码        |        |
| status    | true    | string | 验证码状态        |        |
| ctime     | false   | long   | 短信验证码创建时间 |         |
| etime     | false   | long   | 短信验证码过期时间 |         |

#### action 动作定义：

| 动作                    | 描述        |
| ----------------------- | ---------- |
| login                   | 登录或者注册 |
| 2-step                  | 支付两步验证 |
| change-mobile           | 更换手机号   |
| change-payment-password | 修改支付密码 |

#### status状态定义：

| 状态     | 描述  |
| -------- | ---- |
| active   | 激活 |
| expired  | 过期 |