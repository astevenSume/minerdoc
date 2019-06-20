# 客户端 - 游戏

## 登录游戏

- POST `/v1/game/login` 

````json
{
    "channel_id" : 1,
    "app_id": "327",
}
```

`

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| channel_id  | true    | int    | NA    | 游戏渠道
| app_id      | true   | string | NA    | 游戏编号

> Response:

```json
{
    "code": 200,
    "data": {
        "url": "http://xxx.xxx.xxx/?xxx=xxx"
    }
}
```

### 响应数据

| 字段名称          | 是否必须 | 类型   | 描述          | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
|      url        |   true   | string | 游戏跳转链接  |         |

---

## 查询游戏余额

- GET `/v1/game/balance` 

`

> Response:

```json
{
    "code": 200,
    "data": [
        {
            "channel_name": "开元",
            "channel_id": 1,
            "value": "0"
        },
        {
            "channel_name": "AG",
            "channel_id": 2,
            "value": "0"
        }
    ]
}
```

### 响应数据

| 字段名称          | 是否必须 | 类型   | 描述          | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
|      channel_name    |   true   | string |  渠道名称  |         |
|      channel_id    |   true   | int |  渠道id  |         |
|      value    |   true   | string |  string类型的eusd金额  |         |

---

## 游戏充值

- POST `/v1/game/transferin` 

````json
{   
    "channel_id": 3,
    "eusd": "5.00"
}
```

`

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| channel_id    | true    | int | NA    | 游戏渠道
| eusd    | true    | string | NA    | 转入的eusd金额

> Response:

```json
{
    "code": 200,
    "data": true
}
```

```json
{
    "code": 2020,
    "msg": "币数量不足"
}
```

### 响应数据

| 字段名称          | 是否必须 | 类型   | 描述          | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
|      data    |   false   | bool | 充值成功为true  |         |

---

## 游戏提现

- POST `/v1/game/transferout` 

````json
{   
    "channel_id": 3,
    "eusd": "5.00"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| channel_id    | true    | int | NA    | 游戏渠道
| eusd    | true    | string | NA    | 提现的eusd金额

> Response:

```json
{
    "code": 200,
    "data": true
}
```

```json
{
    "code": 2020,
    "msg": "币数量不足"
}
```

### 响应数据

| 字段名称          | 是否必须 | 类型   | 描述          | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
|      data    |   false   | bool | 提现成功为true  |         |

---

## 游戏订单

- GET `/v1/game/order?page=1&limit=5&channel_id=1&status=` 

````json
{   
    "channel_id": "3",
    "status": "",
    "page": 1,
    "limit": 10,
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| channel_id    | false    | string | NA    | 游戏渠道, 为空不过滤
| status    | false    | string | NA    | 资产记录状态, 为空不过滤
| page    | true    | int | NA    | 当前页
| limit    | true    | int | NA    | 每页数量

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 181692645502877696,//订单id
                "channel_id": 1,//渠道id
                "transfer_type": 1,//订单类型 1:充值  2:提现
                "eusd": "50.1200",//金额
                "status": 1,//订单状态 0:待确认 1:完成 2:失败
                "ctime": 1558083702374//订单创建时间
            },
            {
                "id": 181693017638305792,
                "channel_id": 1,
                "transfer_type": 1,
                "eusd": "50.1200",
                "status": 1,
                "ctime": 1558083791098
            },
            {
                "id": 181694250541383680,
                "channel_id": 1,
                "transfer_type": 2,
                "eusd": "50.1200",
                "status": 1,
                "ctime": 1558084085045
            },
            {
                "id": 181697830094635008,
                "channel_id": 1,
                "transfer_type": 1,
                "eusd": "50.1212",
                "status": 1,
                "ctime": 1558084938477
            },
            {
                "id": 184225669348065280,
                "channel_id": 1,
                "transfer_type": 1,
                "eusd": "5.0000",
                "status": 2,
                "ctime": 1558687622320
            }
        ],
        "meta": {
            "total": 10,
            "page": 1,
            "limit": 5
        }
    }
}
```

### 响应数据

| 字段名称          | 是否必须 | 类型   | 描述          | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
|      data    |   true   | object | 返回结果, 参考json上标注的注释  |         
