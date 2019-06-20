# 服务端 - 角色管理

## 获取所有角色

### HTTP 请求

- GET `/v1/admin/roles`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------  | ------ | ------ | -----------
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "1",
        "name": "超级管理员",
        "desc": "拥有所有的管理权限",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "permissions": [
          "ADD_ADMIN",
          "EDIT_ADMIN",
          "READ_ADMIN",
          "DELETE_ADMIN",
          "MANAGE_SELLER",
          "MANAGE_APPEAL"
        ]
      },
      {
        "id": "2",
        "name": "普通管理员",
        "desc": "拥有普通的管理权限",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "permissions": [
          "MANAGE_SELLER",
          "MANAGE_APPEAL"
        ]
      },
      {
        "id": "3",
        "name": "承兑商审核员",
        "desc": "拥有审核承兑商的权限",
        "permissions": [
          "MANAGE_SELLER"
        ],
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "4",
        "name": "申诉客服",
        "desc": "拥有订单申诉管理权限",
        "permissions": [
          "MANAGE_APPEAL"
        ],
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

## 获取角色

### HTTP 请求

- GET `/v1/admin/roles/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 角色 id

> Response:

```json
{  
  "data": {
    "id": "1",
    "name": "超级管理员",
    "desc": "拥有所有的管理权限",
    "permissions": [
      "ADD_ADMIN",
      "EDIT_ADMIN",
      "READ_ADMIN",
      "DELETE_ADMIN",
      "MANAGE_SELLER",
      "MANAGE_APPEAL"
    ],
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

| 字段名称  | 是否必须 | 类型   | 描述        | 取值范围 |
| -------- | ------- | ------ | ---------- | ------- |
| id       | true    | long   | 角色 ID     |         |
| name     | true    | string | 角色名      |         |
| desc     | true    | string | 角色描述    |         |
| ctime    | false   | long   | 角色创建时间 |         |
| utime    | false   | long   | 角色更新时间 |         |

## 创建角色

### HTTP 请求

- POST `/v1/admin/roles`

```json
{
  "name": "申诉客服",
  "desc": "拥有订单申诉管理权限",
}
```

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| name     | true    | string | NA    | 角色名
| desc     | false   | string | NA    | 角色描述

> Response:

```json
{  
  "data": {
    "id": "4",
    "name": "申诉客服",
    "desc": "拥有订单申诉管理权限",
    "permissions": [
      "MANAGE_APPEAL"
    ],
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应角色完整对象。

## 更新角色

### HTTP 请求

- PUT `/v1/admin/roles/{id}`

```json
{
  "name": "超级管理员",
  "desc": "拥有所有的管理权限",
  "permissions": [
    "ADD_ADMIN",
    "EDIT_ADMIN",
    "READ_ADMIN",
    "DELETE_ADMIN",
    "MANAGE_SELLER",
    "MANAGE_APPEAL"
  ]
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| id        | true    | long   | NA    | 角色 id
| name      | true    | string | NA    | 角色名
| desc      | false   | string | NA    | 角色描述

> Response:

```json
{  
  "data": {
    "id": "1",
    "name": "超级管理员",
    "desc": "拥有所有的管理权限",
    "permissions": [
      "ADD_ADMIN",
      "EDIT_ADMIN",
      "READ_ADMIN",
      "DELETE_ADMIN",
      "MANAGE_SELLER",
      "MANAGE_APPEAL"
    ],
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应角色完整对象。

## 删除角色

### HTTP 请求

- DELETE `/v1/admin/roles/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 角色 id

> Response:

```json
{  
  "data": {
    "id": "1"
  }
}
```

### 响应数据

返回的主数据对象是一个对应角色id的字符串。

### 响应数据
返回的主数据对象是一个对应角色完整对象。

## 获取角色权限

### HTTP 请求

- GET `/v1/admin/roles/{id}/permissions`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 角色 id

> Response:

```json
{  
  "data": [
    "ADD_ADMIN",
    "EDIT_ADMIN",
    "READ_ADMIN",
    "DELETE_ADMIN",
    "MANAGE_SELLER",
    "MANAGE_APPEAL"
  ]
}
```

### 响应数据

返回的主数据对象是一个对应角色的权限列表。

## 添加角色权限

### HTTP 请求

- PUT `/v1/admin/roles/{id}/permissions`

```json
{
  "permissions": [
    "MANAGE_ACTIVITY"
  ]
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| id          | true    | long   | NA    | 角色 id
| permissions | true    | array  | NA    | 权限数组

> Response:

```json
{  
  "data": [
    "ADD_ADMIN",
    "EDIT_ADMIN",
    "READ_ADMIN",
    "DELETE_ADMIN",
    "MANAGE_SELLER",
    "MANAGE_APPEAL",
    "MANAGE_ACTIVITY"
  ]
}
```

### 响应数据

返回的主数据对象是一个对应角色的权限列表。

## 删除角色权限

### HTTP 请求

- DELETE `/v1/roles/{id}/permissions`

```json
{
  "permissions": [
    "MANAGE_SELLER",
    "MANAGE_APPEAL",
  ]
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值 | 描述 
| ------------ | ------- | ------ | ----- | -----------
| id           | true    | long   | NA    | 角色 id
| permissions  | true    | array  | NA    | 权限数组

> Response:

```json
{  
  "data": [
    "ADD_ADMIN",
    "EDIT_ADMIN",
    "READ_ADMIN",
    "DELETE_ADMIN"
  ]
}
```

### 响应数据

返回的主数据对象是一个对应角色的权限列表。

## 分配角色给管理员

### HTTP 请求

- PUT `/v1/admin/admins/{id}/roles/{role_id}`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| id       | true    | long   | NA    | 管理员 id
| role_id  | true    | int    | NA    | 角色 id

> Response:

```json
{  
  "data": {
    "role_id": 2,
    "admin_id": 123456790,
    "granted_by": 123456789,
    "granted_at": 1494901162595
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| role_id      | true    | int    | 角色 id     |         |
| admin_id     | true    | int    | 管理员 id    |         |
| granted_by   | true    | string | 指派管理员 id |         |
| granted_at   | false   | long   | 角色分配时间   |         |

## 移除管理员角色

### HTTP 请求

- DELETE `/v1/admin/admins/{id}/roles/{role_id}`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| id       | true    | long   | NA    | 管理员 id
| role_id  | true    | int    | NA    | 角色 id

> Response:

```json
{  
  "data": {
    "role_id": 2,
    "admin_id": 123456790
  }
}
```

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ----------- | ----- | ------ | ---------- | ------- |
| role_id     | true    | int    | 角色 id     |         |
| admin_id    | true    | int    | 管理员 id   |         |

## 获取管理员所有角色

<aside class="notice">管理员与角色的关系是一对多。</aside>

### HTTP 请求

- GET `/v1/admin/admins/{id}/roles`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ---- | -----------
| id        | true    | int    | NA   | 管理员 id
| page      | false   | int    | NA   | 当前显示分页号
| per_page  | false   | int    | 10   | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "2",
        "name": "普通管理员",
        "desc": "拥有普通的管理权限",
        "permissions": [
          "ADD_ADMIN",
          "EDIT_ADMIN",
          "READ_ADMIN",
          "DELETE_ADMIN",
          "MANAGE_SELLER",
          "MANAGE_APPEAL"
        ],
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "3",
        "name": "承兑商审核员",
        "desc": "拥有审核承兑商的权限",
        "permissions": [
          "MANAGE_SELLER"
        ],
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

## 获取角色所有成员

### HTTP 请求

- GET `/v1/admin/roles/{id}/members`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | -- --- | ----- | -------
| id       | true    | int    | NA    | 角色 id
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "name": "张三",
        "email": "zhangsan@gmail.com",
        "status": "active",
        "granted_by": "0",
        "granted_at": 1494901162595,
      },
      {
        "id": "123456790",
        "name": "李四",
        "email": "lisi@gmail.com",
        "status": "active",
        "granted_by": "123456789",
        "granted_at": 1494901162595,
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

### 响应数据

| 字段名称       | 是否必须 | 类型   | 描述        | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| id           | true    | int    | 管理员 id    |         |
| name         | true    | string | 管理员姓名    |         |
| email        | true    | string | 管理员邮箱    |         |
| status       | true    | string | 管理员状态    |         |
| granted_by   | true    | string | 指派管理员 id |         |
| granted_at   | false   | long   | 角色分配时间  |         |

