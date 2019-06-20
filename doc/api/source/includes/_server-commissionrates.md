# 服务端 - 返佣等级管理
## 获取所有返佣等级

### HTTP 请求

- GET `/v1/admin/commissionrates`

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
        "id": "1",
        "min": "0",
        "max": "1",
        "commission": "50",
        "ctime": 1494901162595,
        "utime": 1494901162595,
      },
      {
        "id": "2",
        "min": "1",
        "max": "10",
        "commission": "60",
        "ctime": 1494901162595,
        "utime": 1494901162595,
      },
      {
        "id": "3",
        "min": "15",
        "max": "50",
        "commission": "80",
        "ctime": 1494901162595,
        "utime": 1494901162595,
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

## 获取返佣等级

### HTTP 请求

- GET `/v1/admin/commissionrates/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 返佣等级 id

> Response:

```json
{  
  "data": {
    "id": "1",
    "min": "0",
    "max": "1",
    "commission": "50",
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 返佣等级 ID    |         |
| min       | true    | string | 业绩开始金额 单位万 |         |
| max       | true    | string | 业绩结束金额 单位万 |         |
| commission| true    | string | 每万业绩佣金    |         |
| ctime     | false   | long   | 返佣等级创建时间 |         |
| utime     | false   | long   | 返佣等级更新时间 |         |

## 创建返佣等级

### HTTP 请求

- POST `/v1/admin/commissionrates`

```json
{
  "min": "0",
  "max": "1",
  "commission": "50",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型    | 默认值 | 描述 
| -------- | ------- | ------ | ------ | -----------
| min      | true    | string |        | 业绩开始金额 单位万 
| max      | true    | string |        | 业绩结束金额 单位万 

> Response:

```json
{  
  "data": {
    "id": "1",
    "min": "0",
    "max": "1",
    "commission": "50",
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据
返回的主数据对象是一个对应返佣等级完整对象。

## 更新返佣等级

### HTTP 请求

- PUT `/v1/admin/commissionrates/{id}`

```json
{
  "min": "0",
  "max": "1",
  "commission": "50",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型    | 默认值 | 描述 
| -------- | ------- | ------ | ------ | -----------
| min      | true    | string |        | 业绩开始金额 单位万 
| max      | true    | string |        | 业绩结束金额 单位万 

> Response:

```json
{  
  "data": {
    "id": "1",
    "min": "0",
    "max": "1",
    "commission": "50",
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据
返回的主数据对象是一个对应返佣等级完整对象。

## 删除返佣等级

### HTTP 请求

- DELETE `/v1/admin/commissionrates/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型    | 默认值 | 描述 
| ------ | ------- | ------ | ----- | -----------
| id     | true    | long   | NA    | 返佣等级 id

> Response:

```json
{  
  "data": {
    "id": "1"
  }
}
```

### 响应数据

返回的主数据对象是一个对应返佣等级id的字符串。
