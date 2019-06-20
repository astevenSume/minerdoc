# 服务端 - 操作日志
## 获取所有操作日志

### HTTP 请求

- GET `/v1/admin/operations`

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述
| ------------ | --------| -------| ----- | -----------
| admin_id     | false   | string | NA    | 操作管理员id
| method       | false   | string | NA    | 请求http方法
| route        | false   | text   | NA    | 请求路由
| action       | false   | text   | NA    | 操作动作
| input        | false   | text   | NA    | 操作请求参数
| user_agent   | false   | text   | NA    | 操作浏览器信息
| ips          | false   | text   | NA    | 操作IP
| response_code| false   | text   | NA    | 操作状态码
| per_page     | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "admin_id": "1234",
        "method": "GET",
        "route": "list_record",
        "action": "操作记录列表",
        "input": "请求参数",
        "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36",
        "ips": "120.36.249.215",
        "response_code": "200",
        "ctime": 1494901162595
      },
      {
        "id": "123456789",
        "admin_id": "1234",
        "method": "POST",
        "route": "add_admin",
        "action": "操作添加管理员",
        "input": "请求参数",
        "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36",
        "ips": "120.36.249.215",
        "response_code": "304",
        "ctime": 1494901162595
      },
    ],
    "meta": {
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    }
  }
}
```

## 获取操作日志

### HTTP 请求

- GET `/v1/admin/operations/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 操作日志 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "admin_id": "1234",
    "method": "POST",
    "route": "add_admin",
    "action": "操作添加管理员",
    "input": "请求参数",
    "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36",
    "ips": "120.36.249.215",
    "response_code": "304",
    "ctime": 1494901162595
  }
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述        | 取值范围     |
| -------------- | ------- | ------ | ---------- | ----------- |
| id             | true    | long   | 操作日志 ID |             |
| admin_id       | false   | string | NA         | 操作管理员id |
| method         | false   | string | NA         | 请求http方法 |
| route          | false   | string | NA         | 请求路由     |
| action         | false   | text   | NA         | 操作动作     |
| input          | false   | text   | NA         | 操作请求参数  |
| user_agent     | false   | text   | NA         | 操作浏览器信息 |
| ips            | false   | text   | NA         | 操作IP        |
| response_code  | false   | text   | NA         | 返回状态码    |
| ctime          | false   | long   | NA         | 操作创建时间  |

## 创建操作日志

### HTTP 请求

- POST `/v1/admin/operations`

```json
{
  "admin_id": "1234",
  "method": "POST",
  "route": "add_admin",
  "action": "操作添加管理员",
  "input": "请求参数",
  "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36",
  "ips": "120.36.249.215",
  "response_code": "304",
  "ctime": 1494901162595
}
```

### 请求参数

| 参数名称       | 是否必须 | 类型   | 默认值 | 描述
| ------------- | --------| -------| ----- | -----------
| admin_id      | true    | string |       | 操作管理员id
| action        | true    | string |       | 操作动作名
| route         | true    | string |       | 请求路由（url地址)
| method        | true    | string |       | 请求http方法
| input         | true    | string |       | 请求数据参数
| user_agent    | true    | string |       | 请求UserAgent
| ips           | true    | string |       | 来源ip
| response_code | true    | string |       | 响应状态码

> Response:

```json
{
  "data": {
    "id": "123456789",
    "admin_id": "1234",
    "method": "POST",
    "route": "manage_admin",
    "action": "操作添加管理员",
    "input": "请求参数",
    "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36",
    "ips": "120.36.249.215",
    "response_code": "304",
    "ctime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应操作日志完整对象。
