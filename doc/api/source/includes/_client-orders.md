# 客户端 - OTC orders 交易订单

## 查询所有订单

查询已提交但是仍未成交或被撤销的订单。

### HTTP 请求

- GET `/v1/orders`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值  | 描述 
| -------- | ------- | ------ | ------ | -----------
| side     | false   | string | both   | 0全部 1购买 2出售
| status   | false   | string | 所有状态 | 单个 or 全部
| appeal_status   | false   | string | 所有申述状态 | 单个 or 全部
| page     | false   | int    | NA     | 当前显示分页号
| limit    | false   | int    | 10     | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 167823331414769664,
        "uid": 167453165686358016,
        "uip": "127.0.0.1",
        "euid": 166854124489408512,
        "side": 1,
        "amount": 431413,
        "price": "6.9539",
        "funds": 30000,
        "pay_id": 167453200696213504,
        "pay_type": 2,
        "pay_name": "支付宝",
        "pay_account": "taobao.com",
        "ctime": 1554777000216,
        "status": 1,
        "epay_id": 166855077401722880,
        "epay_type": 2,
        "epay_name": "支付宝",
        "epay_account": "ali",
		"appeal_status":1,
        "qr_code":"url",
        "u_mobile": "1312341112",
        "u_qr_code": "",
        "eu_mobile": "1312341111",
        "eu_qr_code": "",
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

### 响应数据

| 字段名称         | 是否必须 | 类型   | 描述        | 取值范围     |
| --------------- | ------- | ------ | ---------- | ----------- |
| id              | true    | long   | 订单ID     |             |
| pay_id          | true    | long   | 付款方式ID  |            |
| pay_type        | true    | long   | 付款类型    |            |
| pay_account     | true    | string | 付款账号    |            |
| pay_bank        | false   | string | 付款银行    |            |
| pay_bank_branch | false   | string | 付款银行    |            |
| amount          | true    | string | 订单数量    |            |
| price           | true    | string | 订单价格    |             |
| funds           | true    | string | 成交总金额  |             |
| fee             | true    | string | 成交手续费  |             |
| side            | true    | int | 订单方向    | 1：买, 2：卖 |
| status          | true    | int | 订单状态    | 见下表       |
| ctime           | true    | long   | 订单创建时间 |             |
| utime           | true    | long   | 订单更新时间 |             |
| ftime           | false   | long   | 订单终结时间 |             |
| epay_id          | true    | long   | 承兑商付款方式ID  |            |
| epay_type        | true    | long   | 承兑商付款类型    |            |
| epay_account     | true    | string | 承兑商付款账号    |            |
| epay_bank        | false   | string | 承兑商付款银行    |            |
| epay_bank_branch | false   | string | 承兑商付款银行    |            |
| appeal_status   | false   | int     | 申述状态          |            |
| qr_code         | false   | string  | 申述客服微信二维码|            |

#### status 状态定义:

|ID | 类型         | 描述           |
| -----------| ----------- | -------------- |
|1| created     | 未付款          |
|2| unconfirmed | 已付款, 未确认   |
|3| confirmed   | 已确认          |
|4| canceled    | 已取消          |           |
|5|    |
|6| expired     | 已过期 (自动取消)|
|7| transfering | 转账中          |
|8| finished    | 已完成          |

#### appeal_status 状态定义:

|ID | 类型         | 描述           |
| -----------| ----------- | -------------- |
|1| pending  | 等待处理          |
|2| processing | 正在处理   |
|3| resolved   | 已解决          |


## 获取订单详情

此接口返回指定订单的最新状态和详情。

### HTTP 请求

- GET `/v1/orders/{order-id}`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 描述
| -------- | ------- | ------ | ---------
| order-id | true    | string | 订单ID，填在path中

> Response:

```json
{  
  "data": 
  {
    "id": 59378,
    "pay_id": 12342353,
    "pay_type": 1, // 付款类型
    "pay_name": "张三", // 付款姓名
    "pay_account": "13777777777", // 付款账号
    "pay_bank": "",
    "pay_bank_branch": "",
    "amount": "10.00",
    "price": "6.74",
    "funds": "67.40",
    "fee": "0.0202000000",
    "side": "buy",
    "status": 2,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ftime": 1494901400468,
    "epay_id": 166855077401722880,
    "epay_type": 2,
    "epay_name": "支付宝",
    "epay_account": "ali",
	  "appeal_status":1,
	  "appeal_time":1494901162595,
	  "u_mobile": "13850196151",
    "u_qr_code": "http://test-wallet.oss-cn-hangzhou.aliyuncs.com/payment_168259378623807488_1554901038",
    "eu_mobile": "13850196155",
    "eu_qr_code": "",
    "appeal_id": 1,
    "admin_name": "",
    "admin_wechat": "",
    "admin_qr": ""
  }
}
```

### 响应数据

| 字段名称         | 是否必须 | 类型   | 描述        | 取值范围     |
| --------------- | ------- | ------ | ---------- | ----------- |
| id              | true    | long   | 订单ID     |             |
| pay_id          | true    | long   | 付款方式ID  |            |
| pay_type        | true    | long   | 付款类型    |            |
| pay_account     | true    | string | 付款账号    |            |
| pay_bank        | false   | string | 付款银行    |            |
| pay_bank_branch | false   | string | 付款银行    |            |
| amount          | true    | string | 订单数量    |            |
| price           | true    | string | 订单价格    |             |
| funds           | true    | string | 成交总金额  |             |
| fee             | true    | string | 成交手续费  |             |
| side            | true    | int | 订单方向    | 1：买, 2：卖 |
| status          | true    | int | 订单状态    | 见下表       |
| ctime           | true    | long   | 订单创建时间 |             |
| utime           | true    | long   | 订单更新时间 |             |
| ftime           | false   | long   | 订单终结时间 |             |
| epay_id          | true    | long   | 承兑商付款方式ID  |            |
| epay_type        | true    | long   | 承兑商付款类型    |            |
| epay_account     | true    | string | 承兑商付款账号    |            |
| epay_bank        | false   | string | 承兑商付款银行    |            |
| epay_bank_branch | false   | string | 承兑商付款银行    |            |
| appeal_status   | false   | int     | 申述状态          |            |
| qr_code         | false   | string  | 申述客服微信二维码|            |
| u_mobile        | false   | string  | uid对应手机号|            |
| u_qr_code         | false   | string  | uid对应支付二维码|            |
| eu_mobile         | false   | string  | euid对应手机号|            |
| eu_qr_code     | false   | string  | euid对应支付二维码|            |
| appeal_id      | false   | int  | 申述ID，处于申诉状态才有数据 |        |
| admin_name      | false   | string  | 管理员昵称 |            |
| admin_wechat     | false   | string  | 管理员微信 |            |
| admin_qr         | false   | string  | 管理员二维码 |            |

## 查询所有订单(承兑商)

查询已提交但是仍未成交或被撤销的订单。

### HTTP 请求

- GET `/v1/orders/exchanger`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值  | 描述 
| -------- | ------- | ------ | ------ | -----------
| side     | false   | string | both   | 0全部 1购买 2出售
| status   | false   | int    | 所有状态 | 单个 or 全部
| pay_type | false   | int    | 支付方式 | 0全部 1微信 2支付宝 4银行卡
| date     | false   | int    | 日期    | 例：20190102
| page     | false   | int    | NA     | 当前显示分页号
| limit    | false   | int    | 10     | 每页显示条数


> Response:

```
{
    "code": 200,
     "data": {
        "list": [
            {
                "id": 178865868078317568,
                "uid": 178839351583571968,
                "uip": "127.0.0.1",
                "euid": 178763452930588672,
                "side": 1,
                "amount": 300000,
                "price": "6.8887",
                "funds": 20666,
                "pay_id": 178865841746477056,
                "pay_type": 2,
                "pay_name": "支付宝",
                "pay_account": "taobao.com",
                "ctime": 1557409746117,
                "status": 3,
                "epay_id": 178763684783325184,
                "epay_type": 2,
                "epay_name": "支付宝",
                "epay_account": "taobao.com",
                "date": 20190508
            }
        ],
        "meta": {
            "total": 1,
            "page": 1,
            "limit": 10,
            "total_page": 1,
            "offset": 0
        },
        "total": [
            {
                "date": 20190508,
                "amount": 300000,
                "funds": 20666
            }
        ]
     }
}
```

## 创建申诉

### HTTP 请求

- POST `/v1/orders/{order-id}/appeal`

```json
{
  "type": 1,
  "order_id": "123456",
  "context": "具体原因"
  "wechat": "123456789",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| type        | true    | int    |        | 申诉类型
| order_id    | true    | string |        | 订单id
| wechat      | true    | string |        | 微信号
| context     | false   | text   |        | 申诉原因

> Response:

```json
{  
  "data": {
    "id": "2",
	"type": 1,
	"user_id": "181676179428737024",
	"admin_id": 1,
	"order_id": "2",
	"context": "123456",
	"contact_wechat": "winpaykefu1",
	"qr_code": "",
	"status": 1,
	"ctime": 1560137567020,
	"utime": 1560137567020,
	"mobile": "1234567890"
	"wechat": "123456789"
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| ---------      | ------- | ------ | ---------- | ------- |
| id             | true    | long   | 申诉 ID    |         |
| type           | true    | int    | 申诉类型    | 见下表    |
| user_id        | false   | string | 申述用户id    |         |
| order_id       | false   | string | 申述订单id    |         |
| admin_id       | false   | int    | 处理人id    |         |
| context        | text    | text   | 申诉原因     |         |
| status         | true    | int    | 申诉状态     | 1, 2, 3 |
| contact_wechat | true    |string  | 客服微信    |         |
| qr_code 		 | true    |string  | 客服微信二维码url    |         |
| ctime          | false   | long   | 申诉创建时间  |         |
| utime          | false   | long   | 申诉更新时间  |         |
| mobile         | false   | string | 申诉人手机号  |         |
| wechat         | false   | string | 申诉人微信号  |         |

- 申诉类型 type 定义：

| 类型              | 描述       |
| ----------------- | --------- |
| 1            | 买家未付款 |
| 2            | 卖家未确认 |
| 3            | 长时间无回应 |
| 4            | 涉嫌诈骗   |
| 5            | 涉嫌洗钱   |
| 6            | 其它      |

- 申诉状态 status 定义：

| 类型          | 描述  |
| ------------ | ----- |
| 1      | 等待中 |
| 2      | 处理中 |
| 3      | 已处理 |

## 获取申述
### HTTP 请求

- GET `/v1/orders/{order-id}/appeal`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述
| --------- | ------- | ------ | ----------
| order-id  | true    | string | 订单ID

> Response:

```json
{  
  "data": {
    "id": "2",
	"type": 1,
	"user_id": "181676179428737024",
	"admin_id": 1,
	"order_id": "2",
	"context": "123456",
	"contact_wechat": "winpaykefu1",
	"qr_code": "",
	"status": 1,
	"ctime": 1560137567020,
	"utime": 1560137567020,
	"mobile": "1234567890"
	"wechat": "123456789"
  }
}
```
### 响应数据

返回的主数据对象是一个申述对象。


## 解决申述
### HTTP 请求

- PUT `/v1/orders/{order-id}/appeal`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述
| --------- | ------- | ------ | ----------
| order-id  | true    | string | 订单ID，填在path中

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "type": 1,
    "admin_id": 234567,
    "context": "具体原因",
    "status": 3,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

返回的主数据对象是一个申述对象。


## 获取订单聊天

### HTTP 请求

- GET `/v1/orders/{order-id}/messages`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| order-id | true    | int    | NA    | 订单 id

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "5454937",
        "uid": "0",// 系统消息时 uid 为 0
        "type": "system",
        "content": "created",
        "is_read": 0,
        "ctime": 1530604762277
      },
      {
        "id": "54549372",
        "uid": "1234567",// 用户id
        "type": "text",
        "content": "你好，请尽快打款",
        "is_read": 0,
        "ctime": 1530604762277
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

### 响应数据

| 字段名称         | 是否必须 | 类型   | 描述        | 取值范围       |
| --------------- | ------- | ------ | ---------- | ------------- |
| id              | true    | long   | 订单ID      |               |
| uid             | true    | long   | 用户ID      |               |
| type            | true    | string | 订单类型     | 见下表        |
| content         | true    | text   | 消息内容     | 见下表        |
| is_read         | true    | int    | 是否已读     | 0-未读, 1-已读 |
| ctime           | true    | long   | 订单创建时间 |               |


#### type 类型定义:

| 类型   | 描述   |
| ------ | ----- |
| system | 系统  |
| text   | 消息  |

## 获取订单聊天系统消息

### HTTP 请求

- GET `/v1/orders/common_messages`

### 请求参数
此接口不接受任何参数。

> Responds:

```json
  "data": {
    "created": ["您已成功下单，请及时付款。", "已成功下单，请等待买家付款。"],
    "unconfirmed": ["你已付款，请等待卖家确认收款。", "买家已付款，请及时查收并确认收款。"],
    "confirmed": ["卖家已确认收款，系统正在转账代币到您的钱包。", "您已确认收款，系统正在转账代币到买家的钱包。"],
    "finished": ["转账完成，您已收到您购买的代币。", "转账完成，买家已收到您出售的代币。"],
    "buyer_canceled": ["您已取消订单，请不要再付款给卖家。", "买家取消订单，如收到买家付款，请及时退还。"],
    "seller_canceled": ["卖家取消订单，请不要再付款给卖家。", "您已取消订单，如收到买家付款，请及时退还。"],
    "admin_canceled": ["客服取消订单，请不要再付款给卖家。", "客服取消订单，如收到买家付款，请及时退还。"],
    "pay_expired": ["您的订单因为超时已被系统取消，如有疑问，请联系客服。", "买家付款超过时间限制，订单已被系统取消。"],
    "confirm_expired": ["卖家确认收款时间已过期，可以通过申诉联系客服。", "您的确认收款时间已过期，请尽快确认。"],
    "buyer_appealed": ["您已成功提交申诉，请联系客服处理。", "买家申诉，请配合客服沟通协调。"],
    "seller_appealed": ["卖家申诉，请配合客服沟通协调。", "您已成功提交申诉，请联系客服处理。"],
    "buyer_appeal_resolved": ["您已取消申诉，请继续完成订单。", "买家已取消申诉，您可以继续完成订单。"],
    "seller_appeal_resolved": ["卖家已取消申诉，您可以继续完成订单。", "您已取消申诉，请继续完成订单。"],
  }
```

### 响应数据
返回系统消息内容映射对象。

## 获取订单聊天

### HTTP 请求

- POST `/v1/orders/add_msg`

```json
{
  "order_id": 123456,
  "uid": 123,
  "msg_type": "text",
  "content": "聊天内容"
}
```
### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| order_id | true    | int    | NA    | 订单 id
| uid | true    | int    | NA    | Uid
| msg_type | true    | string    | NA    | text 用户消息  system 系统消息
| content | true    | string    | NA    | 聊天内容

> Response:

```json
{  
  "code": 200,
  "data": {
    "msg":{
        "id": "5454937",
        "order_id": 123456,
        "uid": 123,
        "type": "system",
        "content": "聊天内容",
        "is_read": 0,
        "ctime": 1530604762277
      }
  }
}
```

### 响应数据

| 字段名称         | 是否必须 | 类型   | 描述        | 取值范围       |
| --------------- | ------- | ------ | ---------- | ------------- |
| id              | true    | long   | 订单ID      |               |
| order_id        | true    | long   | 订单ID      |               |
| uid             | true    | long   | 用户ID      |               |
| type            | true    | string | 订单类型     | 见下表        |
| content         | true    | text   | 消息内容     |         |
| is_read         | true    | int    | 是否已读     | 0-未读, 1-已读 |
| ctime           | true    | long   | 订单创建时间 |               |


#### type 类型定义:

| 类型   | 描述   |
| ------ | ----- |
| system | 系统  |
| text   | 消息  |
