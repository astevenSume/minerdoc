# 客户端 - OTC sell用户出售Token
## 出售Token-下单（用户） （需要支付密码&二次验证）

发送一个新订单到平台以进行撮合。  

### HTTP 请求

- POST `/v1/sell`

```json
{
	"quantity":1000000,
	"pay_id":165449135284027392
}
```

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| quantity    | true    | int    | NA    | 购买金额（RMB-分）
| pay_id   | true    | int    | NA    | 用户的收款方式ID
| token     | true    | string | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码，开启二次认证时为必填字段 | action: change-payment-password  |

> Response:

```json
{  
  "data": {
    "id": "5454937",
    "pay_id": 12342353,
    "pay_type": 1, // 付款类型
    "pay_name": "张三", // 付款姓名
    "pay_account": "13777777777", // 付款账号
    "pay_bank": "",
    "pay_bank_branch": "",
    "amount": "10.0000",
    "price": "4.73",
    "funds": "47.30",
    "fee": "0.05",
    "side": "sell",
    "status": "pending",
    "ctime": 1530604762277,
    "utime": 1530604762277,
    "ftime": 0,
  }
}
```

> Response:

```json
{  
  "code": 200
}
```

## 出售Token-确认支付 （承兑商）

### HTTP 请求

- POST `/v1/sell/{order_id}/pay`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| pay_id   | true    | int    | NA    |  承兑商的付款方式ID


> Response:

```json
{  
  "code": 200
}
```

## 买入Token-撤销订单（承兑商）

### HTTP 请求

- POST `/v1/sell/{order_id}/cancel`

> Response:

```json
{  
  "code": 200
}
```

## 确认收款（用户）（需要支付密码&二次验证）

### HTTP 请求

- POST `/v1/sell/{order_id}/confirm`

```json
{  
  "token": "518358864332464",
  "verify_code": "123456"
}
```
### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| token     | true    | string      | 支付密码验证返回的token |        |
| verify_code | false/true | string | 短信验证码，开启二次认证时为必填字段 | action: change-payment-password  |

> Response:

```json
{  
  "code": 200
}
```



