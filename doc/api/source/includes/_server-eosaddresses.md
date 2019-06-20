# 服务端 - EOS Address 地址
## 获取所有地址

### HTTP 请求

- GET `/v1/admin/eosaddress`

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
        "address": "addressoneos",
        "user_id": "123456",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": "123456790",
        "address": "addresss12345",
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

- GET `/v1/admin/eosaddress/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 地址 ID

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "address": "addressoneos",
    "user_id": "123456",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 地址 ID    |         |
| address   | true    | long   | eos 地址   |         |
| user_id   | true    | long   | 所属用户    |         |
| ctime     | false   | long   | 地址创建时间  |         |
| utime     | false   | long   | 地址更新时间  |         |
| dtime     | false   | long   | 地址被删时间  |         |

## 创建地址

### HTTP 请求

- POST `/v1/admin/eosaddress`

```json
{
  "address": "addressoneos",
  "user_id": "123456",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| address     | true    | long   |         | 地址
| user_id     | true    | long   |         | 用户id 

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "address": "addressoneos",
    "user_id": "123456",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应eos地址完整对象。

## 删除地址

### HTTP 请求

- DELETE `/v1/admin/eosaddress/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | long    | true   | NA    | 地址 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应eos地址id的字符串。