# 服务端 - 个人报表

## 获取个人报表

### HTTP 请求

- GET `/v1/admin/personalreport`

### 请求参数

| 字段名称   | 是否必须 | 类型   | 描述                          |
| ---------- | -------- | ------ | ----------------------------- |
| user_name  | false    | string | 搜索的用户名                  |
| channel_id | true     | int    | 搜索的渠道号                  |
| start_time | true     | int    | 开始时间，64位时间戳,精确到秒 |
| end_time   | true     | int    | 结束时间，64位时间戳,精确到秒 |
| page       | false    | int    | 分页查询当前页数,默认是1      |
| limit      | false    | int    | 每页数据条数,默认是10         |



> Response:

```json
//带user_name查询的返回结果,只有一条数据代表这个人这段时间的总计,0代表全部渠道的总和，1代表开元棋牌渠道,
//2代表AG,3代表彩票
{
    "code": 200,
    "data": {
        "list": [
            {
                "uid": 1,
                "nick": "nick",
                "register_time": 123456,
                "last_login_time": 123456,
                "referrer_name": "",
                "agent_lv": 1,
                "sum_can_withdraw": 2002222,
                "sum_withdraw": 200,
                "bet": 900000,
                "total_valid_bet": 900000,
                "profit": 900000,
                "salary": 900000,
                "game_recharge_amount": 900000,
                "eusd_buy_num": 300000,
                "eusd_sold_num": 400000
            }
        ],
        "meta": {
            "limit": 3,
            "page": 2,
            "total": 1
        },
        "total": [
            {
                "bet": 900000,
                "total_valid_bet": 900000,
                "profit": 900000,
                "salary": 900000,
                "result_dividend": 0,
                "game_withdraw_amount": 0,
                "game_recharge_amount": 900000,
                "eusd_buy_num": 300000,
                "eusd_sold_num": 400000,
                "sum_can_withdraw": 2002222,
                "sum_withdraw": 200
            }
        ]
    }
}
//数据库里没有个人报表数据的情况
{
    "code": 200,
    "data": {
        "list": [],
        "meta": {
            "limit": 3,
            "page": 2,
            "total": 1
        },
        "total": [
            {
                "bet": 0,
                "total_valid_bet": 0,
                "profit": 0,
                "salary": 0,
                "result_dividend": 0,
                "game_withdraw_amount": 0,
                "game_recharge_amount": 0,
                "eusd_buy_num": 0,
                "eusd_sold_num": 0,
                "sum_can_withdraw": 0,
                "sum_withdraw": 0
            }
        ]
    }
}
```
```json
//不带user_name的情况
{
    "code": 200,
    "data": {
        "list": [
            {
                "uid": 2,
                "nick": "nick2",
                "register_time": 123456,
                "last_login_time": 123456,
                "referrer_name": "",
                "agent_lv": 1,
                "sum_can_withdraw": 0,
                "sum_withdraw": 0,
                "bet": 900000,
                "total_valid_bet": 900000,
                "profit": 900000,
                "salary": 900000,
                "game_recharge_amount": 900000,
                "eusd_buy_num": 0,
                "eusd_sold_num": 0
            },
            {
                "uid": 1,
                "nick": "nick",
                "register_time": 123456,
                "last_login_time": 123456,
                "referrer_name": "",
                "agent_lv": 1,
                "sum_can_withdraw": 2002222,
                "sum_withdraw": 200,
                "bet": 900000,
                "total_valid_bet": 900000,
                "profit": 900000,
                "salary": 900000,
                "game_recharge_amount": 900000,
                "eusd_buy_num": 300000,
                "eusd_sold_num": 400000
            }
        ],
        "meta": {
            "limit": 3,
            "page": 2,
            "total": 5
        },
        "total": [
            {
                "bet": 1800000,
                "total_valid_bet": 1800000,
                "profit": 1800000,
                "salary": 1800000,
                "result_dividend": 0,
                "game_withdraw_amount": 0,
                "game_recharge_amount": 1800000,
                "eusd_buy_num": 300000,
                "eusd_sold_num": 400000,
                "sum_can_withdraw": 2002222,
                "sum_withdraw": 200
            }
        ]
    }
}
//数据库没有数据的情况
{
    "code": 200,
    "data": {
        "list": [],
        "meta": {
            "limit": 3,
            "page": 1,
            "total": 0
        },
        "total": [
            {
                "bet": 0,
                "total_valid_bet": 0,
                "profit": 0,
                "salary": 0,
                "result_dividend": 0,
                "game_withdraw_amount": 0,
                "game_recharge_amount": 0,
                "eusd_buy_num": 0,
                "eusd_sold_num": 0,
                "sum_can_withdraw": 0,
                "sum_withdraw": 0
            }
        ]
    }
}
```

### 响应数据

| 字段名称             | 是否必须 | 类型   | 描述                                         | 取值范围                                                     |
| -------------------- | -------- | ------ | -------------------------------------------- | ------------------------------------------------------------ |
| uid                  | true     | long   | 用户id                                       |                                                              |
| nick                 | true     | Int    | 昵称                                         |                                                              |
| register_time        | true     | Int    | 注册时间                                     |                                                              |
| last_login_time      | true     | Int    | 最近登陆时间                                 |                                                              |
| referrer_name        | true     | string | 推介人昵称                                   |                                                              |
| agent_lv             | true     | long   | 代理等级                                     |                                                              |
| sum_withdraw         | true     | long   | 佣金提现                                     | 带名字查询的表示这段时间的佣金提现总额<br>没有带名字查询表示和这条记录同一天的拥挤提现值 |
| bet                  | true     | int    | 自己的投注额                                 |                                                              |
| total_valid_bet      | true     | long   | 总有效投注额(自己加无限下级)                 |                                                              |
| profit               | true     | long   | 盈亏                                         |                                                              |
| salary               | true     | long   | 日工资                                       |                                                              |
| self_dividend        | false    | long   | 自己的月分红                                 | 月分红相关字段目前只有彩票渠道和总计里才有                   |
| agent_dividend       | false    | long   | 应该分给下级的月分红                         |                                                              |
| result_dividend      | true     | long   | 最终的月分红<br>self_dividend-agent_dividend |                                                              |
| game_withdraw_amount | true     | long   | 游戏提现                                     |                                                              |
| game_recharge_amount | true     | long   | 游戏充值                                     |                                                              |
| eusd_buy_num         | true     | long   | eusd购买                                     |                                                              |
| eusd_sold_num        | true     | long   | eusd出售                                     |                                                              |

