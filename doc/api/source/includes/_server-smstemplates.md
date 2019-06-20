# 服务端 - 短信模板管理
## 获取所有短信模板

### HTTP 请求

- GET `/v1/admin/smstemplates`

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
        "name": "登录模板",
        "type": "login",
        "template": "{{name}} 您好，欢迎登录{{platform}}平台。您可以通过验证码：{{code}} 进行登录。【{{platform}}】",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": "123456790",
        "name": "两步支付验证模板",
        "type": "2-step",
        "template": "{{name}} 您好，您正在请求支付验证。验证码为：{{code}}。如不是您本人操作请检查您的账户。【{{platform}}】",
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

## 获取短信模板

### HTTP 请求

- GET `/v1/admin/smstemplates/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 短信模板 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "name": "登录模板",
    "type": "login",
    "template": "{{name}} 您好，欢迎登录{{platform}}平台。您可以通过验证码：{{code}} 进行登录。【{{platform}}】",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述           | 取值范围 |
| --------- | ------- | ------ | ------------- | ------- |
| id        | true    | long   | 短信模板 ID    |         |
| name      | true    | string | 短信模板名称    |         |
| type      | true    | string | 短信模板动作    |         |
| template  | true    | string | 短信模板内容    |         |
| ctime     | false   | long   | 短信模板创建时间 |         |
| utime     | false   | long   | 短信模板更新时间 |         |
| dtime     | false   | long   | 短信模板被删时间 |         |

## 创建短信模板

### HTTP 请求

- POST `/v1/admin/smstemplates`

```json
{
  "name": "登录模板",
  "type": "login",
  "template": "{{name}} 您好，欢迎登录{{platform}}平台。您可以通过验证码：{{code}} 进行登录。【{{platform}}】",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| name        | true    | string |        | 短信模板名称
| type        | true    | string |        | 短信模板动作
| template    | true    | string |        | 短信模板内容 

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "name": "登录模板",
    "type": "login",
    "template": "{{name}} 您好，欢迎登录{{platform}}平台。您可以通过验证码：{{code}} 进行登录。【{{platform}}】",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应短信模板完整对象。

## 更新短信模板

### HTTP 请求

- PUT `/v1/admin/smstemplates/{id}`

```json
{
  "name": "登录模板",
  "template": "{{name}} 您好，欢迎登录{{platform}}平台。您可以通过验证码：{{code}} 进行登录。【{{platform}}】",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| name        | true    | string |        | 短信模板名称
| type        | true    | string |        | 短信模板动作
| template    | true    | string |        | 短信模板内容 

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "name": "登录模板",
    "type": "login",
    "template": "{{name}} 您好，欢迎登录{{platform}}平台。您可以通过验证码：{{code}} 进行登录。【{{platform}}】",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0
  }
}
```

### 响应数据
返回的主数据对象是一个对应短信模板完整对象。

## 删除短信模板

### HTTP 请求

- DELETE `/v1/admin/smstemplates/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 短信模板 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应短信模板id的字符串。