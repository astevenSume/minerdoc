# 服务端 - 订单管理
## 获取所有订单

### HTTP 请求

- GET `/v1/admin/orders`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | -----  | ------- | -----------
| uid     | false   | int |    | 
| side     | false   | int | 0    | 指定只返回某一个方向的订单，可能的值有: 1-buy, 2-sell. 默认两个方向都返回。
| status   | false   | int | 所有状态 | 查询的订单状态
| page     | false   | int    | NA    | 当前显示分页号
| limit | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "5454937",
        "uid": "123123123",// 用户id
        "uip": "192.168.1.1", // 用户ip
        "euid": "123123123",// 承兑商id
        "euip": "192.168.1.1", // 承兑商ip
        "side": 1,
        "amount": "10.0000",
        "price": "4.73",
        "funds": "47.30",
        "fee": "0.05",
        "pay_id": "1231313123",
        "pay_type": 1, // 付款类型
        "pay_name": "张三", // 付款姓名  
        "pay_account": "13777777777", // 付款账号
        "pay_bank": "",
        "pay_bank_branch": "",
        "rid": "12312321321", // 区块记录id
        "ctime": 1530604762277,
        "utime": 1530604762277,
        "ftime": 0,
        "status": 1
      },
      ...
    ],
    "meta": {
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    }
  }
}
```

## 获取订单

### HTTP 请求

- GET `/v1/admin/orders/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 订单 id

> Response:

```json
{  
  "data": {
    "id": "5454937",
    "uid": "123123123",// 用户id
    "uip": "192.168.1.1", // 用户ip
    "euid": "123123123",// 承兑商id
    "euip": "192.168.1.1", // 承兑商ip
    "side": 1,
    "amount": "10.0000",
    "price": "4.73",
    "funds": "47.30",
    "fee": "0.05",
    "pay_id": "1231313123",
    "pay_type": 1, // 付款类型
    "pay_name": "张三", // 付款姓名  
    "pay_account": "13777777777", // 付款账号
    "pay_bank": "",
    "pay_bank_branch": "",
    "rid": "12312321321", // 区块记录id
    "ctime": 1530604762277,
    "utime": 1530604762277,
    "ftime": 0,
    "status": 8
  }
}
```

### 响应数据

| 字段名称         | 是否必须 | 类型   | 描述        | 取值范围     |
| --------------- | ------- | ------ | ---------- | ----------- |
| id              | true    | long   | 订单ID      |             |
| uid             | true    | long   | 用户ID      |             |
| uip             | true    | long   | 用户IP      |             |
| euid            | true    | long   | 承兑商ID     |             |
| euip            | true    | long   | 承兑商IP     |             |
| side            | true    | string | 订单方向     | 1：买, 2：卖 |
| amount          | true    | string | 订单数量     |            |
| price           | true    | string | 订单价格     |             |
| funds           | true    | string | 成交总金额   |             |
| fee             | true    | string | 成交手续费   |             |
| pay_name        | true    | string | 付款姓名       |            |
| pay_id          | true    | long   | 付款方式ID   |            |
| pay_type        | true    | long   | 付款类型     |            |
| pay_account     | true    | string | 付款账号     |            |
| pay_bank        | false   | string | 付款银行     |            |
| pay_bank_branch | false   | string | 付款银行     |            |
| rid             | false   | long   | eos区块记录id |             |
| ctime           | true    | long   | 订单创建时间  |             |
| utime           | true    | long   | 订单更新时间  |             |
| ftime           | false   | long   | 订单终结时间  |             |
| status          | true    | int | 订单状态      | 见客户端OTC订单      |


## 取消订单

### HTTP 请求

- POST `/v1/admin/orders/cancel`

```json
{
  "id": "11",
  "uid": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| id          | true    | string    |     | 申述ID
| uid         | true    | string |        | 用户ID

> Response:


### 响应数据
返回的错误码。


## 确认收款

### HTTP 请求

- POST `/v1/admin/orders/confirm`

```json
{
  "id": "11",
  "uid": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| id          | true    | string    |     | 申述ID
| uid         | true    | string |        | 用户ID

> Response:


### 响应数据
返回的错误码。


## 解决订单

### HTTP 请求

- POST `/v1/admin/orders/resolve`

```json
{
  "id": "11",
  "uid": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| id          | true    | string    |     | 申述ID
| uid         | true    | string |        | 用户ID

> Response:


### 响应数据
返回的错误码。


## 确认买家已付款

### HTTP 请求

- POST `/v1/admin/orders/pay`

```json
{
  "id": "11",
  "uid": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| id          | true    | string    |     | 申述ID
| uid         | true    | string |        | 用户ID

> Response:


### 响应数据
返回的错误码。

