# 服务端 - 域名管理

## 获取所有域名

### HTTP 请求

- GET `/v1/admin/endpoint`

### 请求参数


> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 1,
        "endpoint`": "https://www.qdd.com",
        "ctime": 1494901162595,
        "utime": 1494901162595,
      },
      {
        "id": 2,
        "endpoint`": "https://www.qdd.com",
        "ctime": 1494901162595,
        "utime": 1494901162595,
      }
    ]
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围|
| --------- | -------   | ------ | ---------- | ------- |
| id        | true      | int    | 域名id     |         |
| endpoint  | true      | string | 域名       |         |
| ctime     | false     | long   | 创建时间   |         |
| utime     | false     | long   | 更新时间   |         |



## 创建域名

### HTTP 请求

- POST `/v1/admin/endpoint`

```json
{
  "endpoint`": "https://www.qdd.com",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------   | -------  | ------ | ------ | -----------
| endpoint   | true     | string | 域名   |         

> Response:


### 响应数据
返回的操作错误码。


## 更新域名

### HTTP 请求

- PUT `/v1/admin/endpoint`

```json
{
  "id": 1,
  "endpoint`": "https://www.qdd.com"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------   | -------  | ------ | ------ | -----------
| id         | true     | int    | 域名id |   
| endpoint   | true     | string | 域名   |   

> Response:

### 响应数据
返回的操作错误码。


## 删除域名

### HTTP 请求

- DELETE `/v1/admin/endpoint/{id}`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------   | -------  | ------ | ------ | -----------
| id         | true     | int    | 域名id |   

> Response:

```json
{  
  "data": {
    "id": "1"
  }
}
```

### 响应数据
返回的操作错误码。
