# 服务端 - 申诉管理
## 获取所有申诉

### HTTP 请求

- GET `/v1/admin/appeals`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| type     | false   | string | NA    | 筛选类型
| status   | false   | int    | NA    | 筛选状态
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "5",
        "type": 1,
        "user_id": "1",
        "admin_id": 1,
        "order_id": "2",
        "context": "123456",
        "status": 1,
        "ctime": 1560245978659,
        "utime": 1560245978659,
        "mobile": "18850196150",
        "wechat": "123456799"
      },
      {
        "id": "123456790",
        "type": 1,
        "user_id": "123456",
        "admin_id": 345678,
        "order_id": "123456",
        "context": "具体原因",
        "status": 1,
        "ctime": 1494901162595,
        "utime": 1494901162595,
		"mobile": "18850196150",
        "wechat": "123456799"
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

## 获取申诉

### HTTP 请求

- GET `/v1/admin/appeals/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 申诉 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "type": 1,
    "user_id": "123456",
    "admin_id": 345678,
    "order_id": "123456",
    "context": "具体原因",
    "status": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595,
	"mobile": "18850196150",
    "wechat": "123456799"
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 申诉 ID    |         |
| type      | true    | int | 申诉类型    | 见下表    |
| user_id   | false   | long   | 发起人id    |         |
| admin_id  | false   | int   | 处理人id    |         |
| order_id  | false   | long   | 订单id      |         |
| context    | text   | text   | 申诉原因     |         |
| status    | true    | int | 申诉状态     | 1, 2, 3 |
| ctime     | false   | long   | 申诉创建时间  |         |
| utime     | false   | long   | 申诉更新时间  |         |
| mobile    | false   | string | 申诉人手机号  |         |
| wechat     | false   | string | 申诉人微信号  |         |

- 申诉类型定义：
| 类型             | 描述       |
| ---------------- | --------- |
| 1          | 买家未付款 |
| 2          | 卖家未确认 |
| 3          | 长时间无回应 |
| 4          | 涉嫌诈骗   |
| 5          | 涉嫌洗钱   |
| 6          | 其它      |

- 申诉状态定义：
| 状态        | 描述     |
| ---------- | -------- |
| 1    | 等待处理 |
| 2    | 处理中   |
| 3    | 已解决   |

## 创建申诉

### HTTP 请求

- POST `/v1/admin/appeals`

```json
{
  "type": 1,
  "user_id": "123456",
  "admin_id": 345678,
  "order_id": "123456",
  "context": "具体原因"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| type        | true    | int    |         | 申诉类型
| user_id     | true    | string |         | 发起人id
| admin_id    | true    | int    |         | 处理人id
| order_id    | true    | string |         | 订单id
| context     | false   | text   |         | 申诉原因

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "type": 1,
    "user_id": "123456",
    "admin_id": 345678,
    "order_id": "123456",
    "context": "具体原因",
	"contact_wechat": "xxxx", 
    "status": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应申诉完整对象。
contact_wechat微信二维码
## 更新申诉

### HTTP 请求

- PUT `/v1/admin/appeals/{id}`

```json
{
  "type": "no_confirm",
  "user_id": "123456",
  "admin_id": 345678,
  "order_id": "123456",
  "context": "具体原因",
  "status": 1,
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| type        | true    | int    |        | 申诉类型
| user_id     | true    | string |        | 发起人id
| admin_id    | true    | int    |        | 处理人id
| order_id    | true    | string |        | 订单id
| context     | text    | string |        | 申诉原因
| status      | true    | int    |        | 申诉状态

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "type": 1,
    "user_id": "123456",
    "admin_id": 345678,
    "order_id": "123456",
    "context": "具体原因",
    "status": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应申诉完整对象。
