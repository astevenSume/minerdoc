# 服务端 - 配置

## 获取action所有配置

### HTTP 请求

- GET `/v1/admin/config/{action}`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| action     | true    | string | NA    | 配置类型
| page       | false   | int    | NA    | 当前显示分页号
| limit      | false   | int    | 10    | 每页显示条数

- action 配置类型：
| 类型    | 描述     |
| ------- | -------- |
| trade   | 交易配置 |
| usdt    | usdt配置 |
| eos     | eos配置  |
| game    | 游戏配置 |
| sys     | 系统配置 |

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 1,
        "key": "system_conf_key",
		"action": 1,
        "value": "true",
        "desc": "系统配置：",
        "ctime": 1494901162595
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

| 字段名称      | 是否必须  | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| id           | true    | long   |  ID        |         |
| key          | true    | string | 配置关键字   |         |
| action       | false   | int    | 配置类型     |         |
| value        | true    | string | 配置项值     |         |
| desc         | true    | string | 配置描述     |         |
| ctime        | false   | long   | 创建时间     |         |

- action 配置类型：

| 类型    | 描述     |
| ------- | -------- |
| 1       | 交易配置 |
| 2       | usdt配置 |
| 3       | eos配置  |
| 4       | 游戏配置 |
| 5       | 系统配置 |



## 创建action配置

### HTTP 请求

- POST `/v1/admin/config/{action}`

```json
{
    "key": "system_conf_key",
    "value": "true",
    "desc": "系统配置："
}
```

### 请求参数

| 参数名称      | 是否必须  | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ----------   | ------- |
| action       | true    | string | 配置类型     |         |
| key          | true    | string | 配置关键字   |         |
| value        | true    | string | 配置项值     |         |
| desc         | true    | string | 配置描述     |         |

- key 配置关键字
  主键，创建时不可重复

> Response:

```json
{  
  "data": {
        "id": 1,
        "key": "system_conf_key",
        "value": "true",
        "desc": "系统配置：",
        "ctime": 1494901162595
    }
}
```

## 更新action配置

### HTTP 请求

- PUT `/v1/admin/config/{action}`

### 请求参数

| 参数名称      | 是否必须  | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| action       | true    | string | NA           | 配置类型
| key          | true    | string | 配置关键字   | 不可修改 |
| value        | true    | string | 配置项值     |         |
| desc         | true    | string | 配置描述     |         |

- key 配置关键字
  key不可修改，保证url中的key和请求参数中的key一致

```json
{
    "id": 1,
    "key": "system_conf_key",
    "value": "true",
    "desc": "系统配置："
}
```
> Response:

```json
{  
  "data": {
        "id": 1,
        "key": "system_conf_key",
        "value": "true",
        "desc": "系统配置：",
        "ctime": 1494901162595
    }
}
```
## 删除action配置

### HTTP 请求

- DELETE `/v1/admin/config/{action}?id=11`

### 请求参数

| 参数名称      | 是否必须  | 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| action       | true    | string | NA           | 配置类型
| id           | true    | int    | 配置ID     |         |


> Response:

```json
{  
  "data": {
    "key": "system_conf_key"
  }
}
```

## 刷新action配置缓存（全部）

### HTTP 请求

- PUT `/v1/admin/config/{action}/refresh`

### 请求参数

| 参数名称     | 是否必须| 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ----------| -------  |
| action       | true    | string | 配置类型  |   |

> Response:


## 根据id刷新action配置缓存（单个）

### HTTP 请求

- PUT `/v1/admin/config/{action}/refresh?id=1`

### 请求参数

| 参数名称     | 是否必须| 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ----------| -------  |
| action       | true    | string | 配置类型  |   |
| id           | true    | int    | 配置ID    |   |


> Response:


## 清除action配置缓存（全部）

### HTTP 请求

- DELETE `/v1/admin/config/{action}/clean`

### 请求参数

| 参数名称     | 是否必须| 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ----------| -------  |
| action       | true    | string | 配置类型  |   |

> Response:


## 根据id清除action配置缓存（单个）

### HTTP 请求

- DELETE `/v1/admin/config/{action}/clean?id=1`

### 请求参数

| 参数名称     | 是否必须| 类型   | 描述      | 取值范围 |
| ------------ | ------- | ------ | ----------| -------  |
| action       | true    | string | 配置类型  |   |
| id           | true    | int    | 配置ID    |   |


> Response:



