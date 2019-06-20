# 服务端 - 代理白名单管理
## 获取所有代理白名单档位

### HTTP 请求

- GET `/v1/admin/agentwhitelists`

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
        "name": "黄金代理",
        "commission": "200",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456790",
        "name": "白银代理",
        "commission": "160",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456790",
        "name": "青铜代理",
        "commission": "140",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456789",
        "name": "黑铁代理",
		"min": "0",
        "max": "1",
        "commission": "120",
        "ctime": 1494901162595,
        "utime": 1494901162595
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

## 获取代理白名单档位

### HTTP 请求

- GET `/v1/admin/agentwhitelists/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 代理白名单档位 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "name": "黄金代理",
    "commission": "200",
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据

| 字段名称    | 是否必须 | 类型   | 描述            | 取值范围 |
| --------- | ------- | ------ | -------------- | ------- |
| id        | true    | long   | 代理白名单档位 ID |         |
| name      | true    | string | 代理白名单档位名称 |         |
| commission| true    | string | 每万业绩佣金      |         |
| ctime     | false   | long   | 创建时间         |         |
| utime     | false   | long   | 更新时间         |         |

## 创建代理白名单档位

### HTTP 请求

- POST `/v1/admin/agentwhitelists`

```json
{
  "name": "黄金代理",
  "commission": "200",
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| name      | true    | string |        | 代理白名单档位名称
| commission| true    | string |        | 每万业绩佣金

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "name": "黄金代理",
    "commission": "200",
    "ctime": 1494901162595,
    "utime": 1494901162595,
  }
}
```

### 响应数据
返回的主数据对象是一个对应代理白名单档位完整对象。

## 更新代理白名单档位

### HTTP 请求

- PUT `/v1/admin/agentwhitelists/{id}`

```json
{
  "name": "黄金代理",
  "commission": "金龙应用平台"
}
```

### 请求参数

| 参数名称    | 是否必须 | 类型    | 默认值  | 描述 
| --------- | ------- | ------ | ------ | -----------
| id        | true    | long   |        | 代理白名单档位 id
| name      | true    | string |        | 代理白名单档位名称
| commission| true    | string |        | 每万业绩佣金

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "name": "黄金代理",
    "commission": "200",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应代理白名单档位完整对象。

## 删除代理白名单档位

### HTTP 请求

- DELETE `/v1/admin/agentwhitelists/{id}`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 代理白名单档位 id

> Response:

```json
{  
  "data": {
    "id": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应代理白名单档位id的字符串。


## 获取代理白名单档位所有代理

### HTTP 请求

- GET `/v1/admin/agentwhitelists/agents`

### 请求参数

| 参数名称          | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | ------- | ------ | ----- | -----------
| page            | false   | int    | NA    | 当前显示分页号
| limit           | false   | int    | 10    | 每页显示条数
| puid            | false   | string | NA    | 筛选指定 uid 的子代理
| invite_code     | false   | string | NA    | 筛选指定邀请码的代理
| whitelist_id    | false   | int    | NA    | 筛选指定白名单档位的代理

> Response:

```json
{  
  "data": {
    "list": [
      {
        "uid": "23456789",
        "puid": "23456789",
        "whitelist_id": 0,
        "invite_code": "RSXKLZ",
        "invite_num": 123,
        "commission": "10000.00",
        "balance": "3421.00",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "uid": "23456789",
        "puid": "23456789",
        "whitelist_id": 0,
        "invite_code": "RSXKLZ",
        "invite_num": 123,
        "commission": "10000.00",
        "balance": "3421.00",
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

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ----------- | ------- | ------ | ---------- | ------- |
| uid         | true    | string | 代理用户id   |         |
| puid        | true    | string | 上级代理用户id|         |
| whitelist_id| true    | int    | 白名单档位id | 默认值为0，不在白名单内 |
| invite_code | true    | string | 邀请码       |         |
| invite_num  | false   | int    | 邀请人数      |         |
| commission  | false   | string | 累计佣金      |         |
| balance     | false   | string | 可提现余额    |         |
| ctime       | false   | long   | 代理创建时间  |         |
| utime       | false   | long   | 代理更新时间  |         |


## 添加代理到代理白名单档位

### HTTP 请求

- POST `/v1/admin/agentwhitelists/agents`

### 请求参数

| 参数名称      | 是否必须 | 类型    | 默认值  | 描述 
| ------------- | ------- | ------ | ------ | -----------
| whitelist_id  | true    | int    | NA     | 代理白名单档位 id
| uid           | true    | long   | NA     | 代理用户 id

> Response:

```json
{  
  "data": {
    "whitelist_id": 123456789,
    "uid": "123456",
  }
}
```

### 响应数据
返回的主数据对象是一个对应代理白名单档位id及代理用户id。


## 从代理白名单档位删除代理

### HTTP 请求

- DELETE `/v1/admin/agentwhitelists/agents?uid=123456`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| uid     | true    | int    | NA    | 代理用户 id

> Response:

```json
{  
  "data": {
    "uid": "123456",
  }
}
```

### 响应数据

返回的主数据对象是一个代理用户id。