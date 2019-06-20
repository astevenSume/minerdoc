# 服务端 - 代理管理
## 获取所有代理

### HTTP 请求

- GET `/v1/admin/agents`

### 请求参数

| 参数名称          | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | ------- | ------ | ----- | -----------
| page            | false   | int    | NA    | 当前显示分页号
| per_page        | false   | int    | 10    | 每页显示条数
| puid            | false   | long   | NA    | 筛选指定 uid 的子代理
| invite_code     | false   | string | NA    | 筛选指定邀请码的代理
| whitelist_id    | false   | int    | NA    | 筛选指定白名单档位的代理

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "uid": "23456789",
        "puid": "23456789",
        "whitelist_id": "0",
        "invite_code": "RSXKLZ",
        "invite_num": 123,
        "commission": "10000.00",
        "balance": "3421.00",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": "123456790",
        "uid": "23456789",
        "puid": "23456789",
        "whitelist_id": "0",
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

## 获取代理

### HTTP 请求

- GET `/v1/admin/agents/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 代理 id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "uid": "23456789",
    "puid": "23456789",
    "whitelist_id": "0",
    "invite_code": "RSXKLZ",
    "invite_num": 123,
    "commission": "10000.00",
    "balance": "3421.00",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ----------- | ------- | ------ | ---------- | ------- |
| id          | true    | long   | 代理 ID     |         |
| uid         | true    | long   | 代理用户id   |         |
| puid        | true    | long   | 上级代理用户id|         |
| whitelist_id| true    | int    | 白名单档位id | 默认值为0，不在白名单内 |
| invite_code | true    | long   | 邀请码       |         |
| invite_num  | false   | int    | 邀请人数      |         |
| commission  | false   | string | 累计佣金      |         |
| balance     | false   | string | 可提现余额    |         |
| ctime       | false   | long   | 代理创建时间  |         |
| utime       | false   | long   | 代理更新时间  |         |


## 更新代理

### HTTP 请求

- PUT `/v1/admin/agents/{id}`

```json
{
  "whitelist_id": "1"
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值   | 描述 
| ------------ | ------- | ------ | ------- | -----------
| whitelist_id | true    | int    | 0       | 白名单档位id

> Response:

```json
{  
  "data": {
    "id": "123456789",
    "uid": "23456789",
    "puid": "23456789",
    "whitelist_id": "0",
    "invite_code": "RSXKLZ",
    "invite_num": 123,
    "commission": "10000.00",
    "balance": "3421.00",
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
}
```

### 响应数据
返回的主数据对象是一个对应代理完整对象。
