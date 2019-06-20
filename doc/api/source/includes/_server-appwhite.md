# 服务端 - 应用白名单管理

## 获取所有应用白名单

### HTTP 请求

- GET `/v1/admin/appwhite`

### 请求参数
| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| channel_id| false   | int    | NA    | 渠道
| page      | false   | int    | NA    | 当前显示分页号
| limit     | false   | int    | 10    | 每页显示条数

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 2,
                "channel_id": 1,
                "app_id": "1",
                "ctime": 1558439650906
            }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 1
        }
    }
}
```

## 获取应用白名单

### HTTP 请求

- GET `/v1/admin/appwhite?id=2`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 应用渠道 id

> Response:

```json
{  
  "data": {
    "id": 2,
    "channel_id": 1,
    "app_id": "1",
    "ctime": 1558439650906
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述                | 取值范围 |
| ------------- | ------- | ------ | -------------------- | ------- |
| id            | true    | int   |  白名单ID         |         |
| channel_id    | true    | string | 应用渠道 ID | 1,2,3        |
| app_id        | true    | string | 应用id         |         |
| ctime         | false   | long   | 白名单创建时间     |         |

## 创建应用白名单

### HTTP 请求

- POST `/v1/admin/appwhite`

```json
{
   "channel_id": 1,
   "app_id": "1",
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ------ | -----------
| channel_id    | true    | string | 应用渠道 ID | 1,2,3        |
| app_id        | true    | string | 应用id         |         | 

> Response:

```json
{  
  "data": {
    "id": 2,
    "channel_id": 1,
    "app_id": "1",
    "ctime": 1558439650906
  }
}
```

### 响应数据
返回的主数据对象是一个对应应用白名单完整对象。


## 删除应用白名单

### HTTP 请求

- DELETE `/v1/admin/appwhite?id=1`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 应用白名单 id

> Response:

```json
{  
  "data": {
    "id": 1
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用白名单id。