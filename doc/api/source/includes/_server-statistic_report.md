# 服务端 - 查询用户游戏报表数据和统计数据

## 获取 AG 游戏报表数据明细

### HTTP 请求

- GET `/v1/admin/game/report/ag`

### 请求参数

| 参数名称        | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | -------  | ------- | -----  | -----------
/ stime           | false    | int     | 0      | start time
| etime           | false    | int     | 0      | end time
| page            | false    | int     | 1      | page
| limit           | false    | int     | 10     | limit
   

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
             {
                  "id": 3,
                  "account": "liu",
                  "game_type": "66",
                  "game_name": "ag_kx",
                  "order_id" : "",
                  "table_id" : "",
                  "bet": 11,
                  "valid_bet": 11,
                  "profit": 3,
                  "ctime": 1560394132,
                  "uid": 2
             },
            {
                "id": 2,
                "game_name_id": "56",
                "bet": 222222,
                "ctime": 1560394132,
                "uid": 302
            }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 2
        }
    }
}
```

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | -------- | ------ | ---------- | ------- |
| account      | false    | varchar| 帐户名称   |         |
| game_type    | false    | varchar| 游戏ID     |         |
| game_name    | false    | varchar| 游戏名     |         |
| order_id     | false    | varchar| 订单编号   |         |
| table_id     | false    | varchar| 桌号       |         |
| bet          | false    | bigint | 投注       |         |     
| valid_bet    | false    | bigint | 有效投注   |         |
| profit       | false    | bigint | 利润       |         |
| bet_time     | false    | varchar| 投注时间   |         |
| ctime        | false    | bigint | 创建时间   |         |
| uid          | false    | bigint | 用户ID     |         |

## 获取 KY 游戏报表数据明细

### HTTP 请求

- GET `/v1/admin/game/report/ky`

### 请求参数

| 参数名称        | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | -------  | ------- | -----  | -----------
| stime           | false    | int     | 0      | start time
| etime           | false    | int     | 0      | end time
| page            | false    | int     | 1      | page
| limit           | false    | int     | 10     | limit
   

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
             {
                  "id": 201,
                  "account": "",
                  "game_id": "",
                  "game_name": "",
                  "server_id": 8,               
                  "kind_id": "33",
                  "table_id": 12,
                  "chair_id": 4,                 
                  "bet": 4000,
                  "valid_bet": 666666666666666,
                  "profit": 5555555,
                  "revenue": 123,
                  "start_time": 1560476338,
                  "end_time": 1560476999,
                  "ctime": 1560476338,
                  "uid": 201
             }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 1
        }
    }
}
```

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | -------- | ------ | ---------- | ------- |
| id           | true     | bigint | id         |         |
| account      | false    | varchar| 帐户名称   |         |
| game_id      | false    | varchar| 游戏局号   |         |
| game_name    | false    | varchar| 游戏名     |         |
| server_id    | false    | int    | 房间ID     |         |
| kind_id      | false    | varchar| 游戏ID     |     
| table_id     | false    | int    | 桌子号     |         |
| chair_id     | false    | int    | 椅子号     |         |
| bet          | false    | bigint | 投注       |         |     
| valid_bet    | false    | bigint | 有效投注   |         |
| profit       | false    | bigint | 利润       |         |
| revenue      | false    | bigint | 抽水       |         |
| start_time   | false    | varchar| 开始时间   |         |
| end_time     | false    | varchar| 结束时间   |         |
| ctime        | false    | bigint | 创建时间   |         |
| uid          | false    | bigint | 用户ID     |         |




## 获取 RG 游戏报表数据明细

### HTTP 请求

- GET `/v1/admin/game/report/rg`

### 请求参数

| 参数名称        | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | -------  | ------- | -----  | -----------
| stime           | false    | int     | 0      | start time
| etime           | false    | int     | 0      | end time
| page            | false    | int     | 1      | page
| limit           | false    | int     | 10     | limit
   

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [        
            {
                "id": 1,
                "account": "xiaolee",
                "game_name_id": "56",
                "game_name": "zhaojihua",
                "game_kind_name": "rgone",
                "order_id": "32",
                "open_date": "234",
                "period_name": "aaa",
                "open_number": "222",
                "status": 1,
                "bet": 222222,
                "valid_bet": 4444,
                "profit": 234,
                "bet_time": "1560394132",
                "bet_content": "1560394999",
                "ctime": 1560394132,
                "uid": 302
            }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 1
        }
    }
}
```

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | -------- | ------ | ---------- | ------- |
| id           | true     | bigint | id         |         |
| account      | false    | varchar| 帐户名称   |         |
| game_name_id | false    | varchar| 游戏ID     |         |
| game_name    | false    | varchar| 游戏名     |         |
| game_kind_name| false   | varchar| 玩法名称   |         |
| order_id     | false    | int    | 订单编号   |         |
| open_date    | false    | int    | 开奖时间   |         |
| status       | false    | tinyint| 订单状态   |
| bet          | false    | bigint | 投注额     |         |  
| valid_bet    | false    | bigint | 有效投注   |         |
| profit       | false    | bigint | 利润       |         |
| bet_time     | false    | varchar| 下注时间   |         |
| bet_content  | false    | varchar| 下注内容   |         |
| ctime        | false    | bigint | 创建时间   |         |
| uid          | false    | bigint | 用户ID     |         |

## 获取 AG、KY、RG 游戏合计数据

### HTTP 请求

- GET `/v1/admin/game/statistic/ky`
- GET `/v1/admin/game/statistic/ag`
- GET `/v1/admin/game/statistic/rg`

### 请求参数

| 参数名称        | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | -------  | ------- | -----  | -----------
/ stime           | false    | int     | 0      | start time
| etime           | false    | int     | 0      | end time
| page            | false    | int     | 1      | page
| limit           | false    | int     | 10     | limit
   

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
             {
                 "id": 44,                           
                 "newer_nums": 1,
                 "bet": 4000,
                 "valid_bet": 666666666666666,
                 "profit": 5555555,
                 "revenue": 123,                        
                 "ctime": 1560568310,
                 "note": "",
                 "game_id": 33
             }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 1
        },
        "total": {
                    "channel_id": 2,
                    "channel_salary_daily": 1231312,
                    "channel_recharge_eusd": 21000000000001,
                    "channel_withdraw_eusd": 31000000000000,
                    "ctime": 1560738059,
                    "channel_rg_dividend": 2222
        }
    }
}
```

### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | -------- | ------ | ---------- | ------- |
| id           | true     | bigint | ID         |         |
| channel_id    | false   | int    | 游戏ID     | 平台ID  |
| newer_nums    | false   | bigint | 新增人数   |         |
| bet          | false    | bigint | 投注额     |         | 
| valid_bet    | false    | bigint | 有效投注   |         |
| profit       | false    | bigint | 利润       |         |
| revenue      | false    | bigint | 抽水       |         |
| channel_salary_daily    |false   | bigint     | 平台工资    |         |
| channel_recharge_eusd   |false   | bigint     | 平台充值    |         |
| channel_withdraw_eusd   |false   | bigint     | 平台提现    |         |
| ctime        | false    | bigint | 创建时间   |             |         |
| note         | false    | varchar| 描述       |             |         |
| game_id      | false    | int    | 游戏ID     |             |         | 
| channel_positive_nums   | false  | bigint      | 平台活跃人数|         |
| channel_rg_dividend     |false   | bigint     |  红包月分红  |         |

| 字段名称    | 值   |  类型   | 描述                   | 取值范围 |
| code        | 1003 |  int    | 空数据无写入（非合计） | -------  |

注： 响应数据中字段以channel_开头的都是查询时间内数据总和，即整个平台数据

