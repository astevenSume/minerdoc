# 服务端 - 用户管理

## 获取所有用户

### HTTP 请求

- GET `/v1/admin/users`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ----- | -----------
| exchanger | false   | bool   | NA    | 根据是否是承兑商筛选
| status    | false   | int    | 1    | 根据状态筛选
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "uid": "123456789",
        "name": "张三",
        "mobile": "13777777777",
        "status": 1,
        "exchanger": false,
        "parent_uid": "0",
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "ltime": 1494901162595,
        "dtime": 0,
      },
      {
        "uid": "123456790",
        "name": "李四",
        "mobile": "13999999999",
        "status": 1,
        "exchanger": true,
        "parent_uid": "123456789",
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

## 获取用户

### HTTP 请求

- GET `/v1/admin/users/{uid}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| uid     | true    | int    | NA    | 用户 uid

> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "mobile": "13777777777",
    "status": 1,
    "exchanger": false,
    "parent_uid": "0",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据

| 字段名称    | 是否必须 | 类型   | 描述       | 取值范围 |
| ---------- | ------- | ------ | ---------- | ------- |
| uid        | true    | long   | 用户 ID     |         |
| name       | true    | string | 用户姓名     |         |
| mobile     | true    | string | 手机号       |         |
| status     | true    | int    | 用户状态     | active, suspended, deleted |
| exchanger  | true    | bool   | 是否是承兑商  |         |
| uid        | true    | long   | 用户 ID      |         |
| ctime      | false   | long   | 用户创建时间  |         |
| utime      | false   | long   | 用户更新时间  |         |
| ltime      | false   | long   | 用户登陆时间  |         |
| dtime      | false   | long   | 用户删除时间  |         |

- 用户状态定义： 
| 状态| 描述  |
| --- | ----- |
| 1   | 激活   |
| 2   | 审核中 |
| 3   | 禁用   |
| 4   | 删除   |

## 更新用户

### HTTP 请求

- PUT `/v1/admin/users/{uid}`

```json
{
  "name": "张三",
  "mobile": "13777777777",
  "exchanger": false,
  "status": 1,
}
```

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| uid        | true    | long   | NA    | 用户 uid
| name       | false   | string | NA    | 用户姓名
| mobile     | false   | string | NA    | 手机号
| exchanger  | false   | bool   | NA    | 是否是承兑商
| status     | false   | string | NA    | 用户状态

> Response:

```json
{  
  "data": {
    "uid": "123456789",
    "name": "张三",
    "mobile": "13777777777",
    "status": 1,
    "exchanger": false,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "ltime": 1494901162595,
    "dtime": 0,
  }
}
```

### 响应数据
返回的主数据对象是一个对应用户完整对象。

## 删除用户

### HTTP 请求

- DELETE `/v1/admin/users/{uid}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| uid     | true    | long   | NA    | 用户 uid

> Response:

```json
{  
  "data": {
    "uid": "123456789"
  }
}
```

### 响应数据

返回的主数据对象是一个对应用户uid的字符串。

## 批量添加用户 (不需要)

### HTTP 请求

- POST `/v1/admin/users-bulk`

```json
{  
  "users": [
    {
      "name": "张三",
      "mobile": "13777777777",
      "exchanger": false,
      "status": 1,
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
    "users": [
      {
        "uid": "123456789",
        "name": "张三",
        "mobile": "13777777777",
        "exchanger": false,
        "status": 1,
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

返回的主数据对象是新添加的用户对象数组.

## 批量编辑用户 （不需要）

### HTTP 请求

- PUT `/v1/admin/users-bulk`

```json
{  
  "users": [
    {
      "uid": "123456789",
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
    "users": [
      {
        "uid": "123456789",
        "name": "张三",
        "mobile": "13777777777",
        "exchanger": false,
        "status": 1,
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

返回的主数据对象是编辑后的用户对象数组.

## 批量删除用户

### HTTP 请求

- DELETE `/v1/admin/users-bulk`

```json
{  
  "uids": ["123456789", ...]
}
```

> Response:

```json
{  
  "data": {
    "uids": ["123456789", ...]
  }
}
```

### 响应数据

返回的主数据对象是删除的用户id数组.


## 获取用户所有收付款方式

此接口返回用户所有的收付款方式。

### HTTP 请求

- GET `/v1/admin/users/{uid}/payment-methods`

```json
{  
  "data": {
    "list": [
      {
        "id": 123457,
        "type": 1, // 支付宝
        "name": "张三", // 姓名
        "account": "13777777777", // 支付宝账号
        "extra0" : "qrcode url",//收款二维码字符串
        "ord": 1, // 排序
        "status": 0, // 0-禁用 1-可用
        "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
        "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
        "times_per_day_limit": 5,//单日收款笔数
        "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
        "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
        "money_today" : 10000, //本日已收款额度，单位：分，uint64
        "times_today" : 2, //本日已收款次数
        "money_sum" : 5000000,//累计已收款，单位：分，uint64
      },
      {
        "id": 123458,
        "type": 2, // 微信支付
        "name": "张三", // 微信昵称
        "account": "13777777777", // 微信号
        "extra0" : "qrcode url",//收款二维码字符串
        "ord": 2, // 排序
        "status": 0, // 0-禁用 1-可用
        "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
        "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
        "times_per_day_limit": 5,//单日收款笔数
        "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
        "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
        "money_today" : 10000, //本日已收款额度，单位：分，uint64
        "times_today" : 2, //本日已收款次数
        "money_sum" : 5000000,//累计已收款，单位：分，uint64
      },
      {
        "id": 123456,
        "type": 3, // 银行卡
        "name": "张三", // 姓名
        "account": "5522451820999999", // 银行卡号
        "extra0": "中国建设银行", // 开户银行 
        "extra1": "福建支行", // 开户支行
        "ord": 3, // 排序
        "status": 0, // 0-禁用 1-可用
        "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
        "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
        "times_per_day_limit": 5,//单日收款笔数
        "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
        "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
        "money_today" : 10000, //本日已收款额度，单位：分，uint64
        "times_today" : 2, //本日已收款次数
        "money_sum" : 5000000,//累计已收款，单位：分，uint64
      }
    ]
  }
}
```

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| type     | true    | int    | NA    | 类型，包括 1-微信 2-支付宝 4-银行卡
| uid      | true    | long   | NA    | 用户 uid

## 获取用户收付款方式

### HTTP 请求

- GET `/v1/admin/users/{uid}/payment-methods/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| uid     | true    | long   | NA    | 用户 uid
| id      | true    | uint64 | NA    | 收付款方式 id

> Response:

```json
{  
  "code": 0,//错误码
  "data": {
    "id": 123457,
    "type": 1, // 支付宝
    "name": "张三", // 姓名
    "account": "13777777777", // 支付宝账号
    "extra0" : "qrcode url",//收款二维码字符串
    "ord": 1, // 排序
    "status": 0, // 0-禁用 1-可用
    "low_money_per_tx_limit": 1000,//单笔最低收款额, 单位：分，uint64
    "high_money_per_tx_limit": 10000000,//单笔最低收款额, 单位：分，uint64
    "times_per_day_limit": 5,//单日收款笔数
    "money_per_day_limit": 50000,//单日收款限额，单位：分，uint64
    "money_sum_limit": 50000000,//累计收款限额，单位：分，uint64
    "money_today" : 10000, // 本日已收款额度，单位：分，uint64
    "times_today" : 2, //本日已收款次数
    "money_sum" : 5000000,//累计已收款，单位：分，uint64
  }
}
```

### 响应数据

返回的主数据对象是获取的收付款方式对象。

## 通过用户名分页模糊查询用户

### HTTP 请求

- GET `/v1/admin/userfuzzysearch?nick=nick&page=1&limit=10`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述               |
| -------- | -------- | ------ | ------ | ------------------ |
| nick     | true     | String | ""     | 要模糊查询的用户名 |
| page     | true     | int    | 1      | 当前页数           |
| limit    | true     | Int    | 10     | 每页的数量         |

> Response:

```json
//数据库里一共有15条数据
page=1,limit=10的数据
{
    "code": 200,
    "data": {
        "list": [
            {
                "uid": 1,
                "nick": "nick"
            },
            {
                "uid": 2,
                "nick": "nick2"
            },
            {
                "uid": 3,
                "nick": "nick3"
            },
            {
                "uid": 4,
                "nick": "nick4"
            },
            {
                "uid": 5,
                "nick": "nick5"
            },
            {
                "uid": 6,
                "nick": "nick6"
            },
            {
                "uid": 7,
                "nick": "nick7"
            },
            {
                "uid": 8,
                "nick": "nick8"
            },
            {
                "uid": 9,
                "nick": "nick9"
            },
            {
                "uid": 10,
                "nick": "nick10"
            }
        ],
        "total": 15
    }
}
//page=2,limit=10的数据
{
    "code": 200,
    "data": {
        "list": [
            {
                "uid": 11,
                "nick": "nick11"
            },
            {
                "uid": 12,
                "nick": "nick12"
            },
            {
                "uid": 13,
                "nick": "nick13"
            },
            {
                "uid": 14,
                "nick": "nick14"
            },
            {
                "uid": 15,
                "nick": "nick15"
            }
        ],
        "total": 15
    }
}
```

### 响应数据

主要返回uid和用户的列表 以及模糊匹配到的数据数量
