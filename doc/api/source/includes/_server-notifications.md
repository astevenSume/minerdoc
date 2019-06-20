# 服务端 - 系统通知
## 获取所有系统通知

### HTTP 请求

- GET `/v1/admin/notifications`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| status   | false   | int    | NA    | 系统通知状态
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
        "content": "这是一条系统通知",
		"status":1,
        "admin_id": "1234567890",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": 123456790,
        "content": "这是另一条系统通知",
		"status":1,
        "admin_id": "1234567890",
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

## 获取系统通知

### HTTP 请求

- GET `/v1/admin/notifications?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 通知 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "content": "这是一条系统通知",
	"status":1,
    "admin_id": "1234567890",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | int    | 通知 ID    |         |
| content   | true    | string | 通知内容    |         |
| status    | true    | int    | 通知状态    | 见下表定义 |
| admin_id  | true    | string | 发布人ID    |         |
| ctime     | false   | long   | 通知创建时间  |         |
| utime     | false   | long   | 通知更新时间  |         |
| dtime     | false   | long   | 通知被删时间  |         |

-系统通知状态 status 定义：
| 状态      | 描述   |
| --------- | -----  |
| 1         | 未发布 |
| 2         | 已发布 |

## 创建系统通知

### HTTP 请求

- POST `/v1/admin/notifications`

```json
{
  "content": "这是一条系统通知"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| content   | true    | string |        | 通知内容

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "content": "这是一条系统通知",
	"status":1,
    "admin_id": "1234567890",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应通知完整对象。

## 更新系统通知

### HTTP 请求

- PUT `/v1/admin/notifications`

```json
{
  "id":1,
  "content": "这是一条系统通知",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| id        | true    | int    |        | 通知ID
| content   | true    | string |        | 通知内容

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "content": "这是一条系统通知",
	"status":1,
    "admin_id": "1234567890",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应通知完整对象。

## 删除系统通知

### HTTP 请求

- DELETE `/v1/admin/notifications?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 通知 id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应通知id。

## 发布系统通知

### HTTP 请求

- POST `/v1/admin/notifications/publish?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 通知 id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应通知id。