# 客户端 - 收付款方式

## 获取所有收付款方式

此接口返回用户所有的收付款方式。

### HTTP 请求

- GET `/v1/payment-methods`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| type      | false    | int | 0    | 收付款方式 1-微信 2-支付宝 4-银行卡

> Response

```json
{  
  "data": {
    "list": [
      {
        "id": 123457,
        "type": 1, // 支付宝
        "name": "张三", // 姓名
        "account": "13777777777", // 支付宝账号
        "extra0" : "qrcode url",//收款二维码字符串
        "ord": 1, // 排序
        "status": 0, // 0-禁用 1-可用
        "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
        "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
        "times_per_day_limit": 5,//单日收款笔数
        "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
        "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
        "money_today" : 10000, //本日已收款额度，单位：分，uint64
        "times_today" : 2, //本日已收款次数
        "money_sum" : 5000000,//累计已收款，单位：分，uint64
      },
      {
        "id": 123458,
        "type": 2, // 微信支付
        "name": "张三", // 微信昵称
        "account": "13777777777", // 微信号
        "extra0" : "qrcode url",//收款二维码字符串
        "ord": 2, // 排序
        "status": 0, // 0-禁用 1-可用
        "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
        "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
        "times_per_day_limit": 5,//单日收款笔数
        "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
        "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
        "money_today" : 10000, //本日已收款额度，单位：分，uint64
        "times_today" : 2, //本日已收款次数
        "money_sum" : 5000000,//累计已收款，单位：分，uint64
      },
      {
        "id": 123456,
        "type": 4, // 银行卡
        "name": "张三", // 姓名
        "account": "5522451820999999", // 银行卡号
        "extra0": "中国建设银行", // 开户银行 
        "extra1": "福建支行", // 开户支行
        "ord": 3, // 排序
        "status": 0, // 0-禁用 1-可用
        "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
        "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
        "times_per_day_limit": 5,//单日收款笔数
        "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
        "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
        "money_today" : 10000, //本日已收款额度，单位：分，uint64
        "times_today" : 2, //本日已收款次数
        "money_sum" : 5000000,//累计已收款，单位：分，uint64
      }
    ]
  }
}
```

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| type     | true    | int    | NA    | 类型，包括 1-微信 2-支付宝 4-银行卡

## 获取收付款方式

### HTTP 请求

- GET `/v1/payment-methods/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | uint64 | NA    | 收付款方式 id

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457,
    "type": 1, // 支付宝
    "name": "张三", // 姓名
    "account": "13777777777", // 支付宝账号
    "extra0" : "qrcode url",//收款二维码字符串
    "ord": 1, // 排序
    "status": 0, // 0-禁用 1-可用
    "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
    "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
    "times_per_day_limit": 5,//单日收款笔数
    "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
    "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
    "money_today" : 10000, // 本日已收款额度，单位：分，uint64
    "times_today" : 2, //本日已收款次数
    "money_sum" : 5000000,//累计已收款，单位：分，uint64
  }
}
```

### 响应数据

返回的主数据对象是获取的收付款方式对象。

## 添加收付款方式
（需要支付密码&二次验证）
### HTTP 请求

- POST `/v1/payment-methods`

```json
{
  "type": 1, // 支付宝
  "name": "张三", // 姓名
  "account": "13777777777", // 支付宝账号
  "qrcode" : "qrcode url",//收款二维码字符串
  "ord": 1, // 排序
  "verify_code":"1234" // 短信
 }
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | -------- | -----  | ----- | -----------
| type         | true    | int    | NA    | 类型，包括 1-微信 2-支付宝 4-银行卡
| name         | true    | string | NA    | 支付宝姓名，微信昵称，银行卡姓名
| account      | true    | string | NA    | 支付宝账号，微信账号，银行卡号
| bank         | false   | string | NA    | 开户银行 （只有在银行卡类型下，才是必选）
| bank_branch  | false   | string | NA    | 开户支行
| qr_code      | false   | string | NA    | 二维码
| verify_code  | false   | string | NA    | 短信验证码

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457,
    "name": "张三", // 姓名
    "account": "5522451820999999", // 银行卡号
    "extra0": "中国建设银行", // 开户银行 
    "extra1": "福建支行", // 开户支行
    "ord": 1, // 排序
    "status": 0, // 0-禁用 1-可用
  }
}
```

### 响应数据

返回的主数据对象是新添加的收付款方式对象。

## 编辑收付款方式
（需要支付密码&二次验证）
### HTTP 请求

- PUT `/v1/payment-methods/{id}`

```json
{
  "id": 123457,
  "type": 3,
  "name": "张三", 
  "account": "5522451820999999",
  "extra0": "中国建设银行", 
  "extra1": "福建支行",
  "ord": 1,
  "low_money_per_tx_limit": 1000,
  "high_money_per_tx_limit": 10000000,
  "times_per_day_limit": 5,
  "money_per_day_limit": 50000,
  "money_sum_limit": 50000000,
}
```

### 请求参数

| 参数名称                 | 是否必须 | 类型   | 默认值 | 描述 
| ----------------------- | ------- | ------ | ----- | -----------
| id                      | true    | uint64 | NA    | 收付款方式 id
| type                    | true    | string | NA    | 类型，1-微信 2-支付宝 4-银行卡
| name                    | true    | string | NA    | 支付宝姓名，微信昵称，银行卡姓名
| account                 | true    | string | NA    | 支付宝账号，微信账号，银行卡号
| bank                    | false   | string | NA    | 开户银行 （只有在银行卡类型下，才是必选）
| bank_branch             | false   | string | NA    | 开户支行
| qr_code                 | false   | string | NA    | 收款二维码
| low_money_per_tx_limit  | false   | uint64 | NA    | 单笔最低收款额, 单位：分
| high_money_per_tx_limit | false   | uint64 | NA    | 单笔最高收款额, 单位：分
| times_per_day_limit     | false   | int    | NA    | 单日收款笔数
| money_per_day_limit     | false   | uint64 | NA    | 单日收款限额，单位：分
| money_sum_limit         | false   | uint64 | NA    | 累计收款限额，单位：分
| token     | true    | string | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码，开启二次认证时为必填字段 | action: change-payment-password  |

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457,
    "type": 3,
    "name": "张三", 
    "account": "5522451820999999",
    "extra0": "中国建设银行", 
    "extra1": "福建支行",
    "ord": 1,
    "low_money_per_tx_limit": 1000,
    "high_money_per_tx_limit": 10000000,
    "times_per_day_limit": 5,
    "money_per_day_limit": 50000,
    "money_sum_limit": 50000000,
  }
}
```

### 响应数据

返回的主数据对象是编辑后的收付款方式对象。

## 启用收付款方式
### HTTP 请求

- POST `/v1/payment-methods/{id}/activate`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | uint64 | NA    | 收付款方式 id

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457
  }
}
```

### 响应数据

返回的主数据对象是的被启用的收付款方式对象id。

## 禁用收付款方式
### HTTP 请求

- POST `/v1/payment-methods/{id}/deactivate`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | uint64 | NA    | 收付款方式 id

> Response:

```json
{ 
  "code": 0,//错误码 
  "data": {
    "id": 123457
  }
}
```

### 响应数据

返回的主数据对象是的被启用的收付款方式对象id。

## 删除收付款方式
（需要支付密码&二次验证）
### HTTP 请求

- DELETE `/v1/payment-methods/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | uint64 | NA    | 收付款方式 id

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457
  }
}
```

### 响应数据

返回的主数据对象是的删除的收付款方式对象id。

## 收付款方式重排序
### HTTP 请求

- POST `/v1/payment-methods/ord`

```json
{
  "data":[
  {
    "id": 123457,
    "ord": 1
  },
  {
    "id": 123458,
    "ord": 2
  }]
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | uint64 | NA    | 收付款方式 id
| ord     | true    | uint32 | NA    | 收付款方式序列号

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457
  }
}
```

### 响应数据

返回的主数据对象是的删除的收付款方式对象id。

