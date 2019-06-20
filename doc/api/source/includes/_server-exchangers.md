# 服务端 - 承兑商管理
## 获取所有承兑商

### HTTP 请求

- GET `/v1/admin/exchangers`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| mobile   | false   | string | NA    | 根据手机号筛选
| wechat   | false   | string | NA    | 根据微信号筛选
| status   | false   | string | NA    | 根据状态筛选
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "user_id": "456574355345",
        "wechat": "123456788",
        "mobile": "13701090888",
        "telegram": "",
        "status": 1,
        "from": 1,
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "user_id": "123456790",
        "wechat": "42342423",
        "mobile": "13701090666",
        "telegram": "",
        "status": 1,
        "from": 1,
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
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

## 获取承兑商

### HTTP 请求

- GET `/v1/admin/exchangers?uid=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| uid      | true    | long    | NA    | 用户 id

> Response:

```json
{  
  "data": {
    "user_id": "456574355345",
    "wechat": "123456788",
    "mobile": "13701090888",
    "telegram": "",
    "status": 1,
    "from": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| user_id   | true    | string | 用户 ID      |         |
| wechat    | false   | string | 联系微信号    |         |
| mobile    | true    | string | 联系手机号    |         |
| telegram  | false   | string | 联系telegram  |         |
| status    | true    | int    | 承兑商状态     | 见下表   |
| from      | true    | int    | 申请渠道      | 见下表   |
| ctime     | false   | long   | 承兑商创建时间 |         |
| utime     | false   | long   | 承兑商更新时间 |         |
| dtime     | false   | long   | 承兑商被删时间 |         |

- 承兑商状态 status 定义：

| 状态      | 描述   |
| --------- | ----- |
| 0         | 禁用   |
| 1         | 启用 |

- 承兑商申请渠道 from 定义：

| 状态      | 描述   |
| --------- | ----- |
| 0         | 申请   |
| 1         | 指定   |

## 创建承兑商

后台创建的承兑商申请渠道为指定1

### HTTP 请求

- POST `/v1/admin/exchangers`

```json
{
  "user_id": "456574355345",
  "wechat": "123456788",
  "mobile": "13701090888",
  "telegram": "",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型    | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| user_id   | true    | string |        | 用户 ID
| wechat    | false   | string |        | 联系微信号
| mobile    | true    | string |        | 联系手机号
| telegram  | false   | string |        | 联系telegram

> Response:



### 响应数据
返回的错误码。

## 更新承兑商

### HTTP 请求

- PUT `/v1/admin/exchangers`

```json
{
  "user_id":"123456",
  "wechat": "123456788",
  "mobile": "13701090888",
  "telegram": "",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| user_id   | true    | string |        | 承兑商 user_id
| wechat    | false   | string |        | 联系微信号
| mobile    | false   | string |        | 联系手机号
| telegram  | false   | string |        | 联系telegram


### 响应数据
返回的错误码。
