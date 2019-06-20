# 服务端 - 版本管理
## 获取所有版本

### HTTP 请求

- GET `/v1/admin/versions`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| system     | false   | int    | NA    | 平台类型: 1:安卓平台, 2:ios平台
| status     | false   | int    | NA    | 版本状态  1:已删除, 2:已发布, 3:等待发布
| page       | false   | int    | NA    | 当前显示分页号
| per_page   | false   | int    | 10    | 每页显示条数


- System 平台定义

| 状态       | 定义    |
| ----------| ------  |  
| 1         | 安卓平台
| 2         | ios平台   

- Status 状态定义

| 状态       | 定义    |
| ----------| ------  |  
| 3         | 等待发布 
| 2         | 已发布   
| 1         | 已删除   


> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "version": "1.0.0",
        "version_num": 1,
        "changelog": "更新日志",
        "download": "https://baidu.com/app.apk",
        "system": 1,
        "status": 2,
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": "123456790",
        "version": "1.0.0",
        "version_num": 2,
        "changelog": "更新日志",
        "download": "https://baidu.com/app.ipa",
        "system": 1,
        "status": 3,
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

## 获取版本

### HTTP 请求

- GET `/v1/admin/versions/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 版本 id

> Response:

```json
{  
  "data": {
    "id": 123445464,
    "version": "1.0.0",
    "version_num": 1,
    "changelog": "更新日志",
    "download": "https://baidu.com/app.apk",
    "system": 1,
    "status": 2,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| id           | true    | long   | 版本 ID     |         |
| version      | true    | string | 版本号       |         |
| version_num  | true    | int    | 版本更新号    |         |
| changelog     | true    | string | 版本更新日志  |         |
| download     | true    | string | 版本下载链接  |         |
| system       | true    | int    | 平台类型      |         |
| status       | true    | int    | 状态         |         |
| ctime        | false   | long   | 版本创建时间  |         |
| utime        | false   | long   | 版本更新时间  |         |
| dtime        | false   | long   | 版本被删时间  |         |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------  |  
| 3         | 等待发布 
| 2         | 已发布   
| 1         | 已删除     

- System 平台定义

| 状态       | 定义    |
| ----------| ------  |  
| 1         | 安卓平台
| 2         | ios平台   

## 创建版本

### HTTP 请求

- POST `/v1/admin/versions`

```json
{
  "version": "1.0.0",
  "changelog": "更新日志",
  "download": "https://baidu.com/app.apk",
  "version_num": 1,
  "system": 1,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | --------
| version   | true    | string |       | 版本号
| version_num | true  | int    |       | 版本更新号    |         
| changelog  | true    | string |       | 版本更新日志
| download  | true    | string |       | 版本下载链接
| system    | true    | int    |       | 平台类型: 1:安卓平台, 2:ios平台

> Response:

```json
{  
  "data": {
    "id": 1231231,
    "version": "1.0.0",
    "version_num": 1,
    "changelog": "更新日志",
    "download": "https://baidu.com/app.apk",
    "system": 1,
    "status": 3,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应版本完整对象。

## 更新版本

### HTTP 请求

- PUT `/v1/admin/versions/{id}`

```json
{
  "version": "1.0.0",
  "version_num": 1,
  "changelog": "更新日志",
  "download": "https://baidu.com/app.apk",
  "system": 1,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | --------
| version   | true    | string |       | 版本号
| version_num | true  | int    |       | 版本更新号     
| changelog  | true    | string |       | 版本更新日志
| download  | true    | string |       | 版本下载链接
| system    | true    | string |       | 平台类型: android, ios

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "version": "1.0.0",
    "version_num": 1,
    "changelog": "更新日志",
    "download": "https://baidu.com/app.apk",
    "system": 1,
    "status": 3,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0
  }
}
```

### 响应数据
返回的主数据对象是一个对应版本完整对象。

## 上架版本

### HTTP 请求

- POST `/v1/admin/versions/{id}/publish`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 版本 id

> Response:

```json
{  
  "data": {
    "id": 123123123
  }
}
```

### 响应数据

返回的主数据对象是一个对应版本id的字符串。

## 下架版本

### HTTP 请求

- POST `/v1/admin/versions/{id}/unpublish`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 版本 id

> Response:

```json
{  
  "data": {
    "id": 1231232131
  }
}
```

### 响应数据

返回的主数据对象是一个对应版本id的字符串。

## 删除版本

### HTTP 请求

- DELETE `/v1/admin/versions/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 版本 id

> Response:

```json
{  
  "data": {
    "id": 12313123123
  }
}
```

### 响应数据

返回的主数据对象是一个对应版本id的字符串。