# 客户端 - EOS账户

## EUSD 账户详情
### HTTP 请求

- GET `/v1/eos`

> Response:

```json
{
  "data": {
        "address": "fooc2hefm2ei",
        "balance": {
            "available": 998844201,
            "frozen": 1081299,
            "game": 0,
            "trade": 1081299
        },
        "precision": 4,
        "state": "working",
        "symbol": "EUSD",
        "uid": "167453165686358016"
    }
}
```

### 响应数据

| 参数名称   | 是否必须 | 类型   | 描述     | 取值范围  |
| --------- | ------- | ------- | -------- | -------- |
| address   | true    | string | 账户地址  |          |
| state    | true    | string | 账户状态  | working：正常  lock：账户被锁定 |
| symbol    | true    | string | 货币符号  | EUSD     |
| precision | true    | int    | 货币精度  |          |
| balance   | true    | object | 账户余额  |          |

#### balance 字段说明
### 请求参数

| 参数名称    | 是否必须 | 类型   | 描述     | 取值范围 |
| ---------- | ------- | ------ | ------- | ------ |
| available  | true    | bigint | 可用余额 |         |
| frozen     | true    | bigint | 冻结余额 =  游戏冻结 + 转账冻结|         |
| game       | true    | bigint | 游戏冻结 |         |
| trade      | true    | bigint | 转账冻结 |         |


## 给手机号转账 EUSD
（需要支付密码&二次验证）

### HTTP 请求

- POST `/v1/eos/transfer`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| token     | true    | string | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码，开启二次认证时为必填字段 | action: change-payment-password  |


```json
{
  "national_code": "+86",
  "mobile": "13999999999",
  "amount": 500,
  "memo": "",
  "token": "518358864332464",
  "verify_code": "123456"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述      | 取值范围 |
| --------- | ------- | ------ | --------- | ------- |
| national_code | true  | string | 区域码   | 86... |
| mobile    | true    | string | 收款手机   | 仅支持平台内用户的手机号 |
| amount    | true    | string | 转账金额   |        |
| memo      | false   | string | 备注信息   |        |]
| token     | true    | string | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码，开启二次认证时为必填字段 | action: change-payment-password  |
> Response:

```json
{
  "code": 200
}
```


## 获取所有财务记录列表

### HTTP 请求

- GET `/v1/eos/records`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| type      | false   | string | NA    | 记录类型
| page      | false   | int    | 1    | 当前显示分页号
| limit     | false   | int    | 10    | 每页显示条数

> Response:

```json
{
  "data": {
    "list": [
        {
            "id": 5,
            "uid": 167453165686358016,
            "ttype": 7,
            "quantity": 1000000,
            "ctime": 1554780828974,
            "status":0
        }
    ],
    "meta": { 
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    }
  }¡
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述        | 取值范围    |
| -------------- | ------- | ------ | ---------- | ---------- |
| id             | true    | long   | 记录 ID     |            |
| ttype           | true    | string | 类型        | 类型参见下表 |
| quantity         | true    | long   | 数量 *10000        |             
| status         | true    | string | 状态 | 目前无区分都是已完成 
| txid | true    | string | 交易 ID     |            |
| ctime          | true    | long   | 发起时间     |            |

#### 类型定义:

| TTYPE  | 描述     | 备注 |
| -----  | ------- | --- |
| 1 | 购买
| 2 |出售
| 3 |转出
| 4 |转入
| 5 |转入承兑 | 承兑商仅可见
| 6 |承兑转出 |承兑商仅可见
| 7 |应用收入
| 8 |应用支出
| 9 |USDT抵押|承兑商仅可见
| 10 |USDT赎回|承兑商仅可见
| 11| 分润   


## 获取财务记录

### HTTP 请求

- GET `/v1/eos/records/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | --------
| id      | true    | int    | NA    | 记录 id

> Response:

```json
{  
  "data": {
    "id": "28290050-b655-4709-b004-dd1be04974e8",
    "type": "transfer-in",
    "wallet": "13999999999",
    "wallet2": "13999888888",
    "amount": "0.05",
    "fee": "0.01",
    "memo": "hello there",
    "txid": "2f2419ed0be5bd7408aa3d7f6e8800cdc481023f31673edc54b03a924040c2bf",
    "block_num": "45725844",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "status": "created",
  }
}
```

### 响应数据
返回的主数据对象是一个对应财务记录对象。
