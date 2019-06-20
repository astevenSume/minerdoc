# 服务端 - 指导价数据

## 获取所有价格

### HTTP 请求

- GET `/v1/admin/prices`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| market   | false   | int    | NA    | 筛选市场 
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "market": 1,
        "price": "6.74",
        "ctime": 1494901162595,
      },
      {
        "id": "123456790",
        "market": 1,
        "price": "6.74",
        "ctime": 1494901162595,
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

## 获取价格

### HTTP 请求

- GET `/v1/admin/prices/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 价格 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "market": 1,
    "price": "6.74",
    "ctime": 1494901162595
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ----------- | ------- |
| id        | true    | long   | 价格 ID      |         |
| market    | true    | string | 来源市场     | 见下表   |
| price     | true    | string | 当前市价     |         |
| ctime     | false   | long   | 价格创建时间  |         |

- Market 市场定义：

| 市场    | 描述  |
| ------- | ---- |
| 0       | OKEX |
| 1       | 火币 |
| 2       | 币安  |


## 获取当前指导价

### HTTP 请求

- GET `/v1/admin/curprice/`

### 请求参数



> Response:

```json
{  
  "data": {
    "price": "6.92"
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ----------- | ------- |
| price     | true    | string | 当前市价     |         |