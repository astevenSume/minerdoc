# 服务端 - 管理员管理

## 获取所有管理员

### HTTP 请求

- GET `/v1/admin/admins`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| role_id   | false   | int    | NA    | 根据角色筛选
| status    | false   | int    | NA    | 根据状态筛选
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
        "name": "张三",
        "email": "zhangsan@gmail.com",
        "status": 1,
        "roles": [{
          "id": 1,
          "name": "超级管理员"
        }],
        "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "ltime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": 123456790,
        "name": "李四",
        "email": "lisi@gmail.com",
        "status": 1,
        "roles": [{
          "id": 2,
          "name": "普通管理员"
        }],
        "whitelist_ips": "0.0.0.0",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "ltime": 1494901162595,
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

## 获取管理员

### HTTP 请求

- GET `/v1/admin/admins/{id}`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 管理员 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "name": "张三",
    "email": "lisi@gmail.com",
    "status": 1,
    "roles": [{
      "id": 1,
      "name": "超级管理员"
    }],
    "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595,
    "dtime": 0
  }
}
```

### 响应数据

| 字段名称       | 是否必须 | 类型   | 描述          | 取值范围 |
| ------------- | ------- | ------ | ------------ | ------- |
| id            | true    | int    | 管理员 ID     |         |
| name          | true    | string | 管理员管理员名 |         |
| email         | true    | string | 邮箱          |         |
| role_id       | true    | int    | 角色id        |         |
| status        | true    | int    | 管理员状态     | 1, 2, 3 |
| whitelist_ips | true    | string | ip白名单       |         |
| ctime         | false   | long   | 管理员创建时间  |         |
| utime         | false   | long   | 管理员更新时间  |         |
| ltime         | false   | long   | 管理员登陆时间  |         |
| dtime         | false   | long   | 管理员被删时间  |         |

- 管理员状态 status 定义：
| 状态      | 描述  |
| --------- | ---- |
| 1    		| 激活 |
| 2    		| 禁用 |
| 3    		| 删除 |

## 创建管理员

### HTTP 请求

- POST `/v1/admin/admins`

```json
{
  "name": "张三",
  "email": "zhangsan@gmail.com",
  "role_ids": [1],
  "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | --------- | -------- | ------- | -----------
| name       | true    | string | NA    | 管理员姓名
| email      | true    | string | NA    | 邮箱
| role_id    | true    | int    | NA    | 角色 id

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "name": "张三",
    "email": "zhangsan@gmail.com",
    "status": 1,
    "roles": [{
      "id": 1,
      "name": "超级管理员"
    }],
    "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595,
    "dtime": 0
  }
}
```

### 响应数据
返回的主数据对象是一个对应管理员完整对象。

## 更新管理员

### HTTP 请求

- PUT `/v1/admin/admins/{id}`

```json
{
  "name": "张三",
  "email": "zhangsan@gmail.com",
  "role_ids": [1],
  "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值   | 描述 
| ------------ | ------- | ------ | ------- | -----------
| id           | true    | int    | NA      | 管理员 id
| name         | false   | string | NA      | 管理员姓名
| email        | false   | string | NA      | 管理员邮箱
| role_id      | false   | int    | NA      | 角色 id
| status       | false   | int    | NA      | 管理员状态
| whitelist_ips| false   | string | 0.0.0.0 | ip白名单

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "name": "张三",
    "email": "zhangsan@gmail.com",
    "status": 1,
    "roles": [{
      "id": 1,
      "name": "超级管理员"
    }],
    "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595,
    "dtime": 0
  }
}
```

### 响应数据
返回的主数据对象是一个对应管理员完整对象。

## 禁用管理员

### HTTP 请求

- POST `/v1/admin/admins/{id}/suspend`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 管理员 id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应管理员id的字符串。

## 启用管理员

### HTTP 请求

- POST `/v1/admin/admins/{id}/restore`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 管理员 id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应管理员id的字符串。

## 删除管理员

### HTTP 请求

- DELETE `/v1/admin/admins/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 管理员 id

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应管理员id的字符串。


## 批量添加管理员 (不需要)

### HTTP 请求

- POST `/v1/admins-bulk`

```json
{  
  "admins": [
    {
      "name": "张三",
      "email": "zhangsan@gmail.com",
      "role_ids": [1],
      "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
    },
    {
      ...
    },
  ]
}
```

> Response:

```json
{  
  "data": {
    "admins": [
      {
        "id": 123456789,
        "name": "张三",
        "email": "zhangsan@gmail.com",
        "status": 1,
        "roles": [{
          "id": 1,
          "name": "超级管理员"
        }],
        "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "ltime": 1494901162595,
        "dtime": 0,
      },
      {
        ...
      },
    ]
  }
}
```

### 响应数据

返回的主数据对象是新添加的管理员对象数组.

## 批量编辑管理员 (不需要)

### HTTP 请求

- PUT `/v1/admins-bulk`

```json
{  
  "admins": [
    {
      "id": 123456789,
      "name": "张三",
      ...
    },
    {
      ...
    },
  ]
}
```

> Response:

```json
{  
  "data": {
    "admins": [
      {
        "id": 123456789,
        "name": "张三",
        "email": "zhangsan@gmail.com",
        "status": 1,
        "roles": [{
          "id": 1,
          "name": "超级管理员"
        }],
        "whitelist_ips": "192.168.1.1-192.168.1.255,123.90.1.31",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "ltime": 1494901162595,
        "dtime": 0,
      },
      {
        ...
      },
    ]
  }
}
```

### 响应数据

返回的主数据对象是编辑后的管理员对象数组.

## 批量删除管理员 (不需要)

### HTTP 请求

- DELETE `/v1/admins-bulk`

```json
{  
  "ids": [123456789, ...]
}
```

> Response:

```json
{  
  "data": {
    "ids": [123456789, ...]
  }
}
```

### 响应数据

返回的主数据对象是删除的管理员id数组.

## 获取管理员所有操作日志

### HTTP 请求

- GET `/v1/admin/admins/{id}/operations`

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述
| ------------ | --------| -------| ----- | -----------
| id           | false   | string | NA    | 操作管理员id
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

### 响应数据
返回当前管理员操作日志列表。


## 解除绑定google验证

### HTTP 请求

- POST `/v1/admin/admins/unbind?id=1`


### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | --------- | -------- | ------- | -----------
| id         | true    | int        | NA    | 管理员ID

> Response:


### 响应数据
返回对应错误码。

