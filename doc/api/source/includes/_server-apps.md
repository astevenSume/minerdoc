# 服务端 - 应用管理
## 获取所有应用

### HTTP 请求

- GET `/v1/admin/apps`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| type      | false   | int    | NA    | 筛选类型
| featured  | false   | int    | NA    | 筛选推荐
| status    | false   | int    | NA    | 应用状态
| channel_id| false   | int    | NA    | 渠道

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "name": "租赁市场",
        "desc": "去中心化CPU租赁市场",
        "url": "https://baidu.com/app/1",
		"icon_url": "https://baidu.com/app/1",
        "type_id": 1,
        "channel_id": 1,
        "app_id" : "327",
        "featured": 1,
        "status": 1,
		"orientation":1,
		"position":1,
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": "123456790",
        "name": "糖果盒",
        "desc": "免费领取EOS糖果",
        "url": "https://baidu.com/app/2",
		"icon_url": "https://baidu.com/app/1",
        "type_id": 2,
        "channel_id": 1,
        "app_id" : "328",
        "featured": 1,
        "status": 1,
		"orientation":1,
		"position":2,
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

## 获取应用

### HTTP 请求

- GET `/v1/admin/apps?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 应用 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "name": "租赁市场",
    "desc": "去中心化CPU租赁市场",
    "url": "https://baidu.com/app/1",
	"icon_url": "https://baidu.com/app/1",
    "type_id": 1,
    "channel_id": 1,
    "app_id" : "327",
    "featured": 1,
    "status": 1,
	"orientation":1,
	"position":2,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称    | 是否必须 | 类型    | 描述       | 取值范围         |
| --------- | ------- | ------ | ---------- | -------------- |
| id        | true    | long   | 应用 ID    |                 |
| name      | true    | string | 应用名称    |                 |
| desc      | true    | string | 应用描述     |                |
| url       | true    | string | 应用地址     |                |
| icon_url  | true    | string | 应用图标地址 |                |
| featured  | true    | int    | 是否推荐     | 1-不推荐, 2-推荐 |
| type      | true    | int    | 应用分类ID   |                |
| channel_id| true    | int    | 渠道标识     |                |
| app_id    | true    | string    | 渠道应用标识  |                |
| status      | true    | int    | 应用状态     |                |
| orientation | true    | int    | 应用朝向     |                |
| position    | true    | int    | 应用位置     |                |
| ctime       | false   | long   | 应用创建时间  |                |
| utime       | false   | long   | 应用更新时间  |                |
| dtime       | false   | long   | 应用被删时间  |                |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------- |
| 1         | 等待上线  |
| 2         | 已上线   |
| 3         | 计划上线 |

- orientation 定义

| 状态       | 定义    |
| ----------| ------- |
| 1         | 横屏    |
| 2         | 竖屏    |


## 创建应用

### HTTP 请求

- POST `/v1/admin/apps`

```json
{
  "name": "租赁市场",
  "desc": "去中心化CPU租赁市场",
  "url": "https://baidu.com/app/1",
  "icon_url": "https://baidu.com/app/1",
  "type_id": 1,
  "channel_id": 1,
  "app_id" : "327",
  "featured": 1,
  "orientation":1,
  "position":1
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| name       | true    | string |        | 应用名称
| desc       | true    | string |        | 应用描述 
| url        | true    | string |        | 应用地址 
| icon_url   | true    | string |        | 应用图标地址
| type_id    | true    | int    |        | 应用类型
| channel_id | true    | int    |        | 渠道标识   
| app_id     | true    | string    |        | 渠道应用标识
| featured   | false   | int    | 1      | 是否推荐
| orientation| true	   | int    | 1      | 朝向
| position   | true	   | int    | 1      | 位置

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "name": "租赁市场",
    "desc": "去中心化CPU租赁市场",
    "url": "https://baidu.com/app/1",
	"icon_url": "https://baidu.com/app/1",
    "type_id": 1,
    "channel_id": 1,
    "app_id" : "327",
    "featured": 1,
	"orientation":1,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
	"position":1
  }
}
```

### 响应数据
返回的主数据对象是一个对应应用完整对象。

## 更新应用

### HTTP 请求

- PUT `/v1/admin/apps/{id}`

```json
{
  "id":1,
  "name": "租赁市场",
  "desc": "去中心化CPU租赁市场",
  "url": "https://baidu.com/app/1",
  "icon_url": "https://baidu.com/app/1",
  "type_id": 1,
  "channel_id": 1,
  "game_id" : 327,
  "featured": 1,
  "orientation":1,
  "position":1
  
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| name      | true    | string |        | 应用名称
| desc      | true    | string |        | 应用描述 
| url       | true    | string |        | 应用地址
| icon_url  | true    | string |        | 应用图标地址
| type_id   | true    | string |        | 应用类型
| channel_id| true    | int    |        | 渠道标识   
| app_id    | true    | string    |        | 渠道应用标识
| featured  | false   | int    | 1      | 是否推荐
| orientation | false | int    | 1      | 朝向
| position  | true   | int    | 1      | 位置

> Response:

```json
{  
  "data": {
    "id": 1,
    "name": "租赁市场",
    "desc": "去中心化CPU租赁市场",
    "url": "https://baidu.com/app/1",
	"icon_url": "https://baidu.com/app/1",
    "type_id": 1,
    "channel_id": 1,
    "app_id" : "327",
    "featured": 1,
	"orientation":1,
    "status": "published",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
	"position":1
  }
}
```

### 响应数据
返回的主数据对象是一个对应应用完整对象。

## 推荐应用

### HTTP 请求

- POST `/v1/admin/apps/{id}/feature`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 应用 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用id的字符串。

## 取消推荐应用

### HTTP 请求

- POST `/v1/admin/apps/{id}/unfeature`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 应用 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用id的字符串。


## 上线应用

### HTTP 请求

- POST `/v1/admin/apps/{id}/publish`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 应用 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用id的字符串。

## 取消上线应用

### HTTP 请求

- POST `/v1/admin/apps/{id}/unpublish`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 应用 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用id的字符串。

## 删除应用

### HTTP 请求

- DELETE `/v1/admin/apps/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 应用 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应应用id的字符串。

