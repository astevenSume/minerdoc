# 服务端 - 一级代理管理
## 获取所有一级代理

### HTTP 请求

- GET `/v1/admin/topagent`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| mobile   | false   | string | NA    | 根据手机号筛选
| status   | false   | int    | NA    | 根据状态筛选
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
		"national_code":"86",
        "mobile": "13701090888",
        "status": 1,
        "ctime": 1494901162595,
        "utime": 1494901162595,
      },
      {
        "id": 123456789,
		"national_code":"86",
        "mobile": "13701090888",
        "status": 1,
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

## 获取一级代理

### HTTP 请求

- GET `/v1/admin/topagent?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 一级代理 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
	"national_code":"86",
    "mobile": "13701090888",
    "status": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述         | 取值范围 |
| ------------- | ------- | ------ | ----------    | ------- |
| id            | true    | int    | ID            |         |
| national_code | false   | string | 国家码(先不用)|         |
| mobile        | true    | string | 联系手机号    |         |
| status        | true    | int    | 一级代理状态  | 见下表   |
| ctime         | false   | long   | 创建时间 |         |
| utime         | false   | long   | 更新时间 |         |

- 一级代理状态 status 定义：

| 状态      | 描述   |
| --------- | -----  |
| 1         | 未注册 |
| 2         | 已注册 |



## 创建一级代理

### HTTP 请求

- POST `/v1/admin/topagent`

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ----- | -----------
| national_code | false   | string | NA    | 国家码
| mobile        | true    | string | NA    | 手机号

> Response:

```json
{  
  "data": {
    "id": 123456789,
	"national_code":"86",
    "mobile": "13701090888",
    "status": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据

返回的主数据对象。

## 更新一级代理

### HTTP 请求

- POST `/v1/admin/topagent`

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ----- | -----------
| id            | true    | int    | NA    | 一级代理 id
| national_code | false   | string | NA    | 国家码
| mobile        | true    | string | NA    | 手机号

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应一级代理id的字符串。


## 删除一级代理

### HTTP 请求

- DELETE `/v1/admin/topagent?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 一级代理id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应一级代理id的字符串。
