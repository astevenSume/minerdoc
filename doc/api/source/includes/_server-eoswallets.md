# 服务端 - EOS Wallet 钱包数据
## 获取所有钱包

### HTTP 请求

- GET `/v1/admin/eoswallets`

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
        "user_id": "12345678",
        "status": "working",
        "balance": "2000.0000",
        "available": "1000.0000",
        "game": "1000.0000",
        "trade": "0",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456790",
        "user_id": "12345679",
        "status": "lock",
        "balance": "10000.0000",
        "available": "10000.0000",
        "game": "0",
        "trade": "0",
        "ctime": 1494901162595,
        "utime": 1494901162595
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

## 获取钱包

### HTTP 请求

- GET `/v1/admin/eoswallets/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 钱包 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "user_id": "12345678",
    "status": "working",
    "balance": "2000.0000",
    "available": "1000.0000",
    "game": "1000.0000",
    "trade": "0",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 钱包 ID     |         |
| user_id   | true    | long   | 所属用户    |         |
| status    | true    | string | 账户状态    | working：正常  lock：账户被锁定 |
| balance   | true    | string | 账户余额     |          |
| available | true    | string | 可用余额     |          |
| game      | true    | string | 冻结游戏金额  |         |
| trade     | true    | string | 冻结交易金额  |         |
| ctime     | false   | long   | 钱包创建时间  |         |
| utime     | false   | long   | 钱包更新时间  |         |

#### 状态定义：

|状态|描述|
| -- | -- |
|working|正常|
|lock|锁定|

## 创建钱包

### HTTP 请求

- POST `/v1/admin/eoswallets`

```json
{
  "user_id": "12345678",
  "status": "working",
  "balance": "0",
  "available": "0",
  "game": "0",
  "trade": "0",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| user_id     | true    | string |         | 所属用户
| status      | true    | string |         | 账户状态 
| balance     | true    | long   |         | 账户余额 
| available   | true    | long   |         | 可用余额 
| game        | true    | long   |         | 冻结游戏金额
| trade       | true    | long   |         | 冻结交易金额

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "user_id": "12345678",
    "status": "working",
    "balance": "0",
    "available": "0",
    "game": "0",
    "trade": "0",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应钱包完整对象。

## 更新钱包

### HTTP 请求

- PUT `/v1/admin/eoswallets/{id}`

```json
{
  "user_id": "12345678",
  "status": "working",
  "balance": "2000.0000",
  "available": "1000.0000",
  "game": "1000.0000",
  "trade": "0",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| user_id     | false   | string |        | 所属用户
| status      | true    | string |        | 账户状态 
| balance     | true    | long   |        | 账户余额 
| available   | true    | long   |        | 可用余额 
| game        | true    | long   |        | 冻结游戏金额
| trade       | true    | long   |        | 冻结交易金额

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "user_id": "12345678",
    "status": "working",
    "balance": "2000.0000",
    "available": "1000.0000",
    "game": "1000.0000",
    "trade": "0",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应钱包完整对象。