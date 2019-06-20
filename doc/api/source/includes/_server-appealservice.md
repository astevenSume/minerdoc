# 服务端 - 申述客服管理

## 获取所有申述客服

### HTTP 请求

- GET `/v1/admin/appealservice`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| status   | false   | int    | NA    | 客服状态
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
        "admin_id": 1,
		"admin_nick":"admin",
		"qr_code": "url",
        "wechat": "123",
        "status": 1
      },
      {
        "id": 123456789,
        "admin_id": 1,
		"admin_nick":"admin",
		"qr_code": "url",
        "wechat": "123",
        "status": 1
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

## 获取申述客服

### HTTP 请求

- GET `/v1/admin/appealservice/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 客服 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "admin_id": 1,
	"admin_nick":"admin",
	"qr_code": "url",
    "wechat": "123",
    "status": 1
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | int    | 客服 ID    |         |
| admin_id  | true    | int    | 管理员ID   |         |
| admin_nick| true    | string | 管理员昵称 |         |
| wechat    | true    | string | 客服微信   |         |
| qr_code   | true    | string | 客服微信二维码url |         |
| status    | true    | int    | 客服状态   |         |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------- |
| 1         | 启用 |
| 2         | 禁用   |

## 创建申述客服

### HTTP 请求

- POST `/v1/admin/appealservice`

```json
{
  "admin_id": 1,
  "wechat": "123"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| admin_id  | true    | int    |        | 管理员ID
| wechat    | true    | string |        | 客服微信
| qr_code   | true    | string |        | 客服微信二维码url
> Response:

 status 默认为 启用

### 响应数据
返回错误码。


## 更新申述客服

### HTTP 请求

- PUT `/v1/admin/appealservice`

```json
{
  "id": 1,
  "wechat": "123"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| id        | true    | int    |        | 客服ID
| wechat    | true    | string |        | 客服微信
| qr_code   | false   | string |        | 客服微信二维码url

> Response:


### 响应数据
返回错误码。



## 删除申述客服

### HTTP 请求

- DELETE `/v1/admin/appealservice/id=1`


### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| id        | true    | int    |        | 客服ID

> Response:


### 响应数据
返回错误码。


## 禁用申述客服

### HTTP 请求

- POST `/v1/admin/appealservice/suspend/id=1`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 客服 id

> Response:


### 响应数据

返回错误码。

## 启用申述客服

### HTTP 请求

- POST `/v1/admin/appealservice/restore?id=1`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 客服 id

> Response:


### 响应数据

返回错误码。


## 获取所有客服申述处理记录

### HTTP 请求

- GET `/v1/admin/appealservice/record`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| appeal_id| false   | string   | NA    | 申述ID
| order_id | false   | string   | NA    | 申述订单ID
| admin_id | false   | int    | NA      | 申述客服ID
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
		"appeal_id":"1",
		"admin_id": 1,
		"order_id": "1",
        "action": 1,
        "ctime": 1
      },
      {
        "id": "123456789",
		"appeal_id":"1",
		"admin_id": 1,
		"order_id": "1",
        "action": 1,
        "ctime": 1
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

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | int    | 记录 ID    |         |
| admin_id  | true    | int    | 管理员ID   |         |
| appeal_id | true    | string | 申述ID     |         |
| order_id  | true    | string | 订单ID     |         |
| action    | true    | int    | 客服操作动作|         |
| ctime     | true    | long   | 操作时间   |         |

- action 状态定义

| 状态       | 定义    |
| ---------- | ------- |
| 1          | 解决订单 |
| 2          | 取消订单 |
| 3          | 确认买家已付款 |
| 4          | 确认放币 |
| 5          | 冻结卖家 |
| 6          | 解冻卖家 |
| 7          | 禁止卖家 |
| 8          | 激活卖家 |
| 9          | 禁止买家 |
| 10         | 激活买家 |

