# 服务端 - USDT账户


## 获取所有地址

### HTTP 请求

- GET `/v1/admin/usdt/addresses`

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
        "address": "13TASu2eYYRn9PfrMZyfwBJFryoV2oqj7m",
        "user_id": "123456",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": "123456790",
        "address": "3MbYQMMmSkC3AgWkj9FMo5LsPTW1zBTwXL",
        "user_id": "4567890",
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

## 获取地址

### HTTP 请求

- GET `/v1/admin/usdt/addresses/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 地址 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "address": "13TASu2eYYRn9PfrMZyfwBJFryoV2oqj7m",
    "user_id": "123456",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ----------- | ------- |
| id        | true    | string | 地址 ID     |         |
| address   | true    | string | usdt 地址   |         |
| user_id   | true    | string | 所属用户     |         |
| ctime     | false   | long   | 地址创建时间  |         |
| utime     | false   | long   | 地址更新时间  |         |
| dtime     | false   | long   | 地址被删时间  |         |



## 获取所有钱包

### HTTP 请求

- GET `/v1/admin/usdt/wallets`

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
        "status": 1,
        "balance": "2000.0000",
        "available": "1000.0000",
        "frozen": "1000.0000",
        "mortgaged": "0",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456790",
        "user_id": "12345679",
        "status": 1,
        "balance": "10000.0000",
        "available": "10000.0000",
        "frozen": "0",
        "mortgaged": "0",
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

- GET `/v1/admin/usdt/wallets/{id}`

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
    "status": 1,
    "balance": "2000.0000",
    "available": "1000.0000",
    "frozen": "1000.0000",
    "mortgaged": "0",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | string   | 钱包 ID    |         |
| user_id   | true    | string   | 所属用户    |         |
| status    | true    | int      | 账户状态    | 1：正常  0：账户被锁定 |
| balance   | true    | string | 账户余额     |          |
| available | true    | string | 可用余额     |          |
| frozen    | true    | string | 冻结金额     |         |
| mortgaged | true    | string | 抵押金额     |         |
| ctime     | false   | long   | 钱包创建时间  |         |
| utime     | false   | long   | 钱包更新时间  |         |

#### 状态定义：

|状态|描述|
| -- | -- |
|0|锁定|
|1|正常|


## 获取转入转出记录列表

### HTTP 请求

- GET `/v1/admin/usdt/turnrecords`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 10    | 每页显示条数

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "2",
                "uid": "166717822901157888",
                "type": 3,
                "status": 1,
                "step": "",
                "desc": "", 
                "txid": "",
                "amount": "1.0000",
                "utime": 1554999087881,
                "ctime": 1554999087881,
                "fee": "0.5",
                "fee_onchain": "0.0002",
                "memo": "",
				"from":"",
				"to":"",
				"mobile":"111"
            }
        ],
        "meta": {
            "total": 2,
            "page": 1,
            "limit": 1,
            "total_page": 2,
            "offset": 0
        }
    }
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述       | 取值范围    |
| -------------- | ------- | ------ | ---------- | --------- |
| id             | true    | string | 记录 ID     |           |
| uid            | true    | string | otc用户 ID     |           |
| type           | true    | int    | 类型       | 类型参见客户端-USDT账户 |
| from           | true    | string | 付款账号    |           |
| to             | true    | string | 收款账号    |           |
| amount         | true    | string   | 金额        |           |
| fee            | true    | string   | 手续费      |           |
| fee_onchain    | true    | string   | 链上手续费  |           |
| memo           | true    | string   | 备注        |            |
| status         | true    | int    | 状态        | 状态参见客户端-USDT账户 |
| step           | true    | string | 流程阶段    |       |
| desc           | true    | string | 订单状态描述信息    |       |
| txid           | true    | string | 交易 ID     |           |
| ctime          | true    | long   | 发起时间    |           |
| utime          | true    | long   | 最后更新时间 |           |
| mobile         | true    | string | 手机号      |            |

## 获取抵押赎回记录列表

### HTTP 请求

- GET `/v1/admin/usdt/transrecords`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 10    | 每页显示条数

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "2",
                "uid": "166717822901157888",
                "type": 3,
                "status": 1,
                "step": "",
                "desc": "",                 
                "amount": "1.0000",
                "utime": 1554999087881,
                "ctime": 1554999087881,
                "fee": "",               
                "memo": "",
				"from":"",
				"to":""
				"mobile":"111"
            }
        ],
        "meta": {
            "total": 2,
            "page": 1,
            "limit": 1,
            "total_page": 2,
            "offset": 0
        }
    }
}
```

## 获取提现申请记录列表

### HTTP 请求

- GET `/v1/admin/usdt/cashrecords`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 10    | 每页显示条数

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "2",
                "uid": "166717822901157888",
                "type": 3,
                "status": 1,
                "txid": "",
                "amount": "1.0000",
                "utime": 1554999087881,
                "ctime": 1554999087881,
                "fee": "",
                "memo": "",
				"from":"",
				"to":""
				"mobile":"111"
            }
        ],
        "meta": {
            "total": 2,
            "page": 1,
            "limit": 1,
            "total_page": 2,
            "offset": 0
        }
    }
}
```

## 审批通过提现申请

### HTTP 请求

- POST `/v1/admin/usdt/cashrecords/approve`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | -------- | ----- | -----------
| id        | true    | string   | NA    | 当前显示分页号
| uid       | true    | string   | 10    | 每页显示条数

> Response:

```json
{
    "code": 200
}
```


## 审批拒绝提现申请

### HTTP 请求

- POST `/v1/admin/usdt/cashrecords/reject`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | -------- | ----- | -----------
| id        | true    | string   | NA    | 当前显示分页号
| uid       | true    | string   | 10    | 每页显示条数

> Response:

```json
{
    "code": 200
}
```

## usdt账户锁定

### HTTP 请求

- POST `/v1/admin/usdt/lock`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | -------- | ----- | -----------
| uid       | true    | string   | 10    | 每页显示条数

> Response:

```json
{
    "code": 200
}
```

## usdt账户解锁

### HTTP 请求

- POST `/v1/admin/usdt/unlock`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | -------- | ----- | -----------
| uid       | true    | string   | 10    | 每页显示条数

> Response:

```json
{
    "code": 200
}
```