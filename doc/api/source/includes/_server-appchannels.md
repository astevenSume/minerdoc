# 服务端 - 应用渠道管理

## 获取所有应用渠道

### HTTP 请求

- GET `/v1/admin/appchannels`

### 请求参数


> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
		"is_third_hall":1,
        "name": "金龙",
        "desc": "金龙应用平台",
        "exchange_rate":100,
        "precision":2,
		"profit_rate":100,
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": 123456790,
		"is_third_hall":2,
        "name": "无双",
        "desc": "无双应用",
        "exchange_rate":100,
        "precision":2,
		"profit_rate":100,
        "ctime": 1494901162595,
        "utime": 1494901162595
      }
    ]
  }
}
```

## 获取应用渠道

### HTTP 请求

- GET `/v1/admin/appchannels?id=`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 应用渠道 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
	"is_third_hall":true,
    "name": "金龙",
    "desc": "金龙应用平台",
    "exchange_rate":100,
    "precision":2,
	"profit_rate":100,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述                | 取值范围 |
| ------------- | ------- | ------ | -------------------- | ------- |
| id            | true    | int   | 应用渠道 ID           |  见下表 |
| is_third_hall | true    | string | 渠道方是否有应用大厅 | 2:没有 1：有        |
| name          | true    | string | 应用渠道名称         |         |
| desc          | true    | string | 应用渠道描述         |         |
| exchange_rate      | true    | int | 兑换比率    |         |
| precision      | true    | int | 精度    |         |
| profit_rate      | true    | int | 利润率(万分比)    |         |
| ctime         | false   | long   | 应用渠道创建时间     |         |
| utime         | false   | long   | 应用渠道更新时间     |         |

#### id 定义:

|ID  | 描述       
|----| ----------- 
|1   | 开元         
|2   | AG 
|3   | 彩票   


## 创建应用渠道

### HTTP 请求

- POST `/v1/admin/appchannels`

```json
{
  "id": 123456789,
  "is_third_hall":2,
  "precision":100,
  "exchange_rate":100,
  "profit_rate":100,
  "name": "金龙",
  "desc": "金龙应用平台",
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ------ | -----------
| id            | true    | int    | NA     | 应用渠道 id
| is_third_hall | true    | int    |        | 渠道方是否有应用大厅
| name          | true    | string |        | 应用渠道名称
| desc          | true    | string |        | 应用渠道描述 
| exchange_rate | true    | int    |        |兑换比率|
| precision     | true    | int    |        |精度| 
| profit_rate   | true    | int    |        |利润率| 

> Response:

```json
{  
  "data": {
    "id": 123456789,
	"is_third_hall":2,
    "name": "金龙",
    "desc": "金龙应用平台",
    "exchange_rate":100,
    "precision":2,
	"profit_rate":100,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应应用渠道完整对象。

## 更新应用渠道

### HTTP 请求

- PUT `/v1/admin/appchannels`

```json
{
  "id":1,
  "is_third_hall":2,
  "name": "金龙",
  "desc": "金龙应用平台",
  "exchange_rate":100,
  "profit_rate":100,
  "precision":2
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ------ | -----------
| id            | true    | int    | NA     | 应用渠道 id
| is_third_hall | true    | int    |        | 渠道方是否有应用大厅
| name          | true    | string |        | 应用渠道名称
| desc          | true    | string |        | 应用渠道描述 
| exchange_rate | true    | int    |        |兑换比率|
| precision     | true    | int    |        |精度| 
| profit_rate   | true    | int    |        |利润率| 


> Response:

```json
{  
  "data": {
    "id": 123456789,
	"is_third_hall":2,
    "name": "金龙",
    "desc": "金龙应用平台",
    "exchange_rate":100,
    "precision":2,
	"profit_rate":100,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应应用渠道完整对象。

## 删除应用渠道

### HTTP 请求

- DELETE `/v1/admin/appchannels?id=`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 应用渠道 id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用渠道id。