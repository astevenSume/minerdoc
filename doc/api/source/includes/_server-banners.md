# 服务端 - 广告管理
## 获取所有广告

### HTTP 请求

- GET `/v1/admin/banners`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| status   | false   | string | NA    | 广告状态
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "subject": "送iphone活动",
        "image": "https://baidu.com/huodong/1.png",
        "url": "https://baidu.com/huodong/1.html",
        "status": "published",
        "stime": 1494901162595,
        "etime": 1494901162595,
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456790",
        "subject": "澳门行活动",
        "image": "https://baidu.com/huodong/2.png",
        "url": "https://baidu.com/huodong/2.html",
        "status": "pending",
        "stime": 1494901162595,
        "etime": 1494901162595,
        "ctime": 1494901162595,
        "utime": 1494901162595
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

## 获取广告

### HTTP 请求

- GET `/v1/admin/banners/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 广告 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "subject": "送iphone活动",
    "image": "https://baidu.com/huodong/1.png",
    "url": "https://baidu.com/huodong/1.html",
    "status": "published",
    "stime": 1494901162595,
    "etime": 1494901162595,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 广告 ID    |         |
| subject   | true    | string | 广告主题    |         |
| image     | true    | string | 广告图片地址  |         |
| url       | true    | string | 广告跳转链接  |         |
| status    | true    | string | 广告状态     |         |
| stime     | false   | long   | 广告开始时间  |         |
| etime     | false   | long   | 广告结束时间  |         |
| ctime     | false   | long   | 广告创建时间  |         |
| utime     | false   | long   | 广告更新时间  |         |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------- |
| pending   | 等待发布 |
| published | 已发布   |
| expired   | 已过期(后面再实现) |

## 创建广告

### HTTP 请求

- POST `/v1/admin/banners`

```json
{
  "subject": "送iphone活动",
  "image": "https://baidu.com/huodong/1.png",
  "url": "https://baidu.com/huodong/1.html",
  "stime": 1494901162595,
  "etime": 1494901162595,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| subject   | true    | string |        | 广告主题
| image     | true    | string |        | 广告图片地址
| url       | true    | string |        | 广告跳转链接
| stime     | false   | long   |        | 广告开始时间
| etime     | false   | long   |        | 广告结束时间

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "subject": "送iphone活动",
    "image": "https://baidu.com/huodong/1.png",
    "url": "https://baidu.com/huodong/1.html",
    "status": "pending",
    "stime": 1494901162595,
    "etime": 1494901162595,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

新创建的广告 status 默认为 pending。

### 响应数据
返回的主数据对象是一个对应广告完整对象。

## 更新广告

### HTTP 请求

- PUT `/v1/admin/banners/{id}`

```json
{
  "subject": "送iphone活动",
  "image": "https://baidu.com/huodong/1.png",
  "url": "https://baidu.com/huodong/1.html",
  "stime": 1494901162595,
  "etime": 1494901162595,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| subject   | true    | string |        | 广告主题
| image     | true    | string |        | 广告图片地址
| url       | false   | string |        | 广告跳转链接
| stime     | false   | long   |        | 广告开始时间
| etime     | false   | long   |        | 广告结束时间

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "subject": "送iphone活动",
    "image": "https://baidu.com/huodong/1.png",
    "url": "https://baidu.com/huodong/1.html",
    "status": "published",
    "stime": 1494901162595,
    "etime": 1494901162595,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应广告完整对象。


## 发布广告

### HTTP 请求

- POST `/v1/admin/banners/{id}/publish`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 广告 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应广告id的字符串。

## 取消发布广告

### HTTP 请求

- POST `/v1/admin/banners/{id}/unpublish`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 广告 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

## 删除广告

### HTTP 请求

- DELETE `/v1/admin/banners/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 广告 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应广告id的字符串。