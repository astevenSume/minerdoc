# 客户端 - USDT 账户

## USDT 账户详情

### HTTP 请求

- GET `/v1/usdt` 

> Response:

```json
{
    "code": 200,
    "data": {
        "address": "1GPa2CEu887nocR2MVzc993q925xHMRmpJ",
        "status": 1,
        "symbal": "USDT",
        "precision": 4,
        "balance": {
            "available": "0.0000",
            "frozen": "0.0000",
            "mortgaged": "0.0000"
        }
    }
}
```

### 响应数据

| 参数名称   | 是否必须 | 类型   | 描述     | 取值范围   |
| --------- | ------- | ------ | ------- | ----- |
| address   | true    | string | 账户地址 |       |
| status    | true    | int    | 账户状态 | 0： 账户被锁定 1： 正常   |
| symbol    | true    | string | 货币符号 | usdt  |
| precision | true    | int    | 货币精度 |       |
| balance   | true    | object | 账户余额 |       |

#### balance 字段说明

| 参数名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | --------- | ------ |
| available | true    | string | 可用余额   |        |
| frozen    | true    | string | 冻结余额   |        |
| mortgaged | true    | string | 已抵押余额 |        |

## USDT 账户余额

### HTTP 请求

- GET `/v1/usdt/balance` 

> Response:

```json
{
    "code": 200,
    "data": {
        "available": "0.0000",
        "frozen": "0.0000",
        "mortgaged": "0.0000"
    }
}
```

### 响应数据

| 参数名称   | 是否必须 | 类型   | 描述     | 取值范围 |
| --------- | ------- | ------ | ------- | ------- |
| available | true    | string | 可用余额 |         |
| frozen    | true    | string | 冻结余额 |         |
| mortgaged | true    | string | 抵押余额 |         |

## 给钱包地址转账 USDT

（需要支付密码&二次验证）

### HTTP 请求

- POST `/v1/usdt/transfer` 

```json
{
  "method": "address",
  "address": "1PTeEUpofUTeXDwKtJMo2YKwVKsKRjtPya",
  "amount": "0.05",
  "memo": "",
  "fee": "0.01",
  "token": "518358864332464",
  "verify_code": "123456"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述      | 取值范围 |
| --------- | ------- | ------ | -------- | ------- |
| method    | true    | string | 转账方式  | address |
| address   | true    | string | 收款地址  |         |
| amount    | true    | string | 转账金额  |         |
| memo      | false   | string | 备注信息  |         |
| fee       | false   | string | 转账手续费 |        |
| token     | true    | string | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码， 开启二次认证时为必填字段 | action: change-payment-password  |

> Response:

```json
{
  "data": {
    "id": "12345677"
  }
}
```

### 响应数据

| 参数名称  | 是否必须 | 类型   | 描述   | 取值范围 |
| -------- | ------- | ------ | ----- | ------- |
| id       | true    | long   | 转账ID |        |

## 抵押 USDT

### HTTP 请求

- POST `/v1/usdt/mortgage` 

```json
{
  "amount": "1.0000"
}
```

### 请求参数

| 参数名称  | 是否必须 | 类型   | 描述     | 取值范围 |
| -------- | ------- | ------ | ------- | ------- |
| amount   | true    | string | 抵押金额 |         |

> Response:

```json
{
  "data": {
    "id": "12345677"
  }
}
```

### 响应数据

| 参数名称 | 是否必须 | 类型   | 描述       | 取值范围 |
| ------- | ------- | ------ | --------- | ------- |
| id      | true    | long   | 财务记录ID |         |

## 赎回 USDT

### HTTP 请求

- POST `/v1/usdt/release` 

```json
{
  "amount": "1.0000"
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述     | 取值范围 |
| ------- | ------- | ------ | ------- | ------ |
| amount  | true    | string | 赎回金额 |        |

> Response:

```json
{
  "data": {
    "id": "12345678"
  }
}
```

### 响应数据

| 参数名称 | 是否必须 | 类型   | 描述       | 取值范围 |
| ------- | ------- | ------ | --------- | ------- |
| id      | true    | long   | 财务记录ID |         |

## 获取所有财务记录列表

### HTTP 请求

- GET `/v1/usdt/records` 

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| type      | false   | string | NA    | 记录类型
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 20    | 每页显示条数

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 2,
                "uid": 166717822901157888,
                "type": 3,
                "status": 1,
                "txid": "",
                "amount": "1.0000",
                "utime": 1554999087881,
                "ctime": 1554999087881,
                "block_num": "",
                "fee": "",
                "memo": ""
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
| id             | true    | long   | 记录 ID     |           |
| type           | true    | string | 类型       | 类型参见下表 |
| from           | true    | long   | 付款账号    |           |
| to             | true    | long   | 收款账号    |           |
| amount         | true    | long   | 金额        |           |
| fee            | true    | long   | 手续费      |           |
| memo           | true    | long   | 备注        |            |
| status         | true    | string | 状态        | 状态参见下表 |
| txid           | true    | string | 交易 ID     |           |
| block_num      | true    | string | 区块号      |           |
| ctime          | true    | long   | 发起时间    |           |
| utime          | true    | long   | 最后更新时间 |           |

#### type 类型定义:

| 类型        | 描述     |
| ----------- | ------- |
| 1           | 转入（充值） |
| 2           | 转出（提现） |
| 3           | 抵押    |
| 4           | 赎回    |

#### status 抵押赎回状态定义： 

| 状态       | 描述    |
| ---------- | ------- |
| 0          | 状态未知 |
| 1          | 抵押中 |
| 2          | 已抵押   |
| 3          | 抵押失败   |
| 4          | 赎回中   |
| 5          | 已赎回   |
| 6          | 赎回失败   |

#### status 充值状态定义： 

| 状态       | 描述    |
| ---------- | ------- |
| 100        | 状态未知 |
| 101        | 充值中   |
| 102        | 已充值   |
| 103        | 充值失败   |

#### status 提现状态定义： 

| 状态            | 描述        |
| --------------- | ---------- |
| 200             | 状态未知    |
| 201             | 已提交      |
| 202             | 已取消      |
| 203             | 审批通过    |
| 204             | 审批拒绝    |
| 205             | 转账中      |
| 206             | 已确认      |
| 207             | 失败      |

## 获取财务记录

### HTTP 请求

- GET `/v1/usdt/records/{id}` 

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 记录 id

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 2,
        "uid": 166717822901157888,
        "from": "",
        "to": "",
        "type": 3,
        "status": 1,
        "txid": "",
        "amount": "1.0000",
        "utime": 1554999087881,
        "ctime": 1554999087881,
        "block_num": "",
        "fee": "",
        "memo": ""
    }
}
```

### 响应数据

返回的主数据对象是一个对应财务记录对象。 

`

## 获取推荐手续费

### HTTP 请求

- GET `/v1/usdt/calculatefee` 

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| amount      | true    | string    | NA    | 转账金额

> Response:

```json
{
    "code": 200,
    "data": {
        "half_hour_cny": "6711.5243",
        "hour_cny": "2695.1790",
        "two_hour_cny": "158.5399",
        "four_hour_cny": "52.8466",
        "half_hour_btc": "0.1141",
        "hour_btc": "0.0458",
        "two_hour_btc": "0.0027",
        "four_hour_btc": "0.0009",
        "half_hour_usdt": "946.6184",
        "hour_usdt": "380.1381",
        "two_hour_usdt": "22.3611",
        "four_hour_usdt": "7.4537"
    }
}
```

### 响应数据

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
|  half_hour_cny     | true    | string    | NA    | 半小时手续费(人民币)
|  hour_cny          | true    | string    | NA    | 一小时手续费(人民币)
|  two_hour_cny      | true    | string    | NA    | 两小时手续费(人民币)
|  four_hour_cny     | true    | string    | NA    | 四小时手续费(人民币)
|  half_hour_btc     | true    | string    | NA    | 半小时手续费(比特币)
|  hour_btc          | true    | string    | NA    | 一小时手续费(比特币)
|  two_hour_btc      | true    | string    | NA    | 两小时手续费(比特币)
|  four_hour_btc     | true    | string    | NA    | 四小时手续费(比特币)
|  half_hour_usdt    | true    | string    | NA    | 半小时手续费(泰达币)
|  hour_usdt         | true    | string    | NA    | 一小时手续费(泰达币)
|  two_hour_usdt     | true    | string    | NA    | 两小时手续费(泰达币)
|  four_hour_usdt    | true    | string    | NA    | 四小时手续费(泰达币)

