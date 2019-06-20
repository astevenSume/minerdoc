# 服务端 - 权限管理
## 获取所有权限

### HTTP 请求

- GET `/v1/admin/permissions`

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
        "slug": "USER_MANAGE",
        "desc": "用户管理",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "dtime": 0,
      },
      {
        "id": "123456790",
        "slug": "ADMIN_MANAGE",
        "desc": "管理员管理",
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

## 获取权限

### HTTP 请求

- GET `/v1/admin/permissions/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 权限 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "slug": "USER_MANAGE",
    "desc": "用户管理",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 权限 ID    |         |
| slug      | true    | string | 权限标识    |         |
| desc      | true    | string | 权限描述    |         |
| ctime     | false   | long   | 权限创建时间  |         |
| utime     | false   | long   | 权限更新时间  |         |
| dtime     | false   | long   | 权限被删时间  |         |

## 创建权限

### HTTP 请求

- POST `/v1/admin/permissions`

```json
{
  "slug": "USER_MANAGE",
  "desc": "用户管理",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| slug      | true    | string |        | 权限标识
| desc      | true    | string |        | 权限描述 

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "slug": "USER_MANAGE",
    "desc": "用户管理",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应权限完整对象。

## 更新权限

### HTTP 请求

- PUT `/v1/admin/permissions/{id}`

```json
{
  "slug": "USER_MANAGE",
  "desc": "用户管理"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| slug      | true    | string |        | 权限标识
| desc      | true    | string |        | 权限描述 

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "slug": "USER_MANAGE",
    "desc": "用户管理",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "dtime": 0
  }
}
```

### 响应数据
返回的主数据对象是一个对应权限完整对象。

## 删除权限

### HTTP 请求

- DELETE `/v1/admin/permissions/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 权限 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应权限id的字符串。