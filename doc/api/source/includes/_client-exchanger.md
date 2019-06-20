# 客户端 - 承兑商

## 申请成为承兑商
### HTTP 请求

- POST `/v1/exchange/apply`

```json
{
  "mobile": "13777777777",
  "wechat": "13777777777",
  "telegram": "13777777777"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| mobile      | true    | string | NA    | 手机号
| wechat      | false   | string | NA    | 微信号
| telegram    | false   | string | NA    | telegram号

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "uid": 234567123123,
    "status": "pending",
    "ctime": 1494901162595
  }
}
```

## 承兑商资产信息
### HTTP 请求

- GET `/v1/exchange/info`

> Response:

```json
{  
  "data": {
        "uid": 165710248248606720,
        "account": "4pypgr2pjsdh",
        "status": 1,
        "available": 570822,
        "trade": 429178,
        "sell_able": true,
        "sell_rmb_day": 12300,
        "sell_rmb_lower_limit": 300000,
        "buy_able": true,
        "buy_rmb_day": 100,
        "buy_rmb_lower_limit": 5000000,
        "buy_pay_type": 7,
        "ctime": 1554273213746,
        "num_sell_order": 0,
        "num_buy_order": 1
  }
}
```


## 划转-用户账户转入OTC账户
### HTTP 请求

- POST `/v1/exchange/tranferInto`

```json
{
  "quantity": 1234567,
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| quantity    | true    | int |     | 代币数量 * 精度10000后的int

> Response:

```json
{  
  "code": 200
}
```

## 划转-OTC账户转入用户账户
### HTTP 请求

- POST `/v1/exchange/tranferOut`

```json
{
  "quantity": 1234567
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| quantity    | true    | int  |    | 代币数量 * 精度10000后的int

> Response:

```json
{  
  "code": 200
}
```

## 承兑商 开启出售Token
### HTTP请求
- POST /v1/buy/start

```json
{
	"able":true,
	"lower_limit": 10000,
	"day_limit": 300000
}
```
### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| able    | true    | bool |    | true-开启 false-关闭
| lower_limit    | true    | int |    | 最低购买金额（RMB-分）
| day_limit    | true    | int |    | 每日限制购买金额（RMB-分）

> Response:

```json
{  
  "code": 200
}
```

## 承兑商 开启收购Token
### HTTP请求
- POST /v1/sell/start

```json
{
	"able":true,
	"lower_limit": 10000,
	"day_limit": 300000,
	"pay_type":[1,2,4]
}
```
### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| able    | true    | bool |    | true-开启 false-关闭
| lower_limit    | true    | int |    | 最低出售金额（RMB-分）
| day_limit    | true    | int |    | 每日限制出售金额（RMB-分）
| pay_type | true | []int | |承兑商支持的付款方式

> Response:

```json
{  
  "code": 200
}
```
