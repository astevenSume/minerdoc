# 客户端 - 分润报表

## 获取个人分润报表

### HTTP 请求

- GET `/v1/profitreport/getpersonreports`

### 请求参数

| 字段名称   | 是否必须 | 类型 | 描述                          |
| ---------- | -------- | ---- | ----------------------------- |
| channel_id | true     | int  | 搜索的渠道号                  |
| start_time | true     | int  | 开始时间，64位时间戳,精确到秒 |
| end_time   | true     | int  | 结束时间，64位时间戳,精确到秒 |



> Response:

```json
{
    "code": 200,
    "data": {
        "profit_report": {
            "ProfitReports": {
                "0": {
                    "uid": 1,
                    "bet": 2600000,
                    "total_valid_bet": 2600000,
                    "profit": 2600000,
                    "salary": 2600000,
                    "self_dividend": 1600000,
                    "agent_dividend": 800000,
                    "result_dividend": 800000,
                    "game_withdraw_amount": 2600000,
                    "game_recharge_amount": 2600000
                },
                "1": {
                    "uid": 1,
                    "channel_id": 1,
                    "bet": 900000,
                    "total_valid_bet": 900000,
                    "profit": 900000,
                    "salary": 900000,
                    "game_withdraw_amount": 900000,
                    "game_recharge_amount": 900000
                }
            },
            "SumWithdraw": 0,
            "EusdBuyNum": 300000,
            "EusdSoldNum": 400000
        }
    }
}
```
### 响应数据

| 字段名称             | 是否必须 | 类型 | 描述                                                         | 取值范围                                   |
| -------------------- | -------- | ---- | ------------------------------------------------------------ | ------------------------------------------ |
| sum_withdraw         | true     | long | 佣金提现                                                     |                                            |
| profit_reports       | true     | 字典 | 个人记录报表,是一个key-value的字典,0代表全部平台总和，1代表开元棋牌，2代表AG，3代表彩票 |                                            |
| bet                  | true     | int  | 自己的投注额                                                 |                                            |
| total_valid_bet      | true     | long | 总有效投注额(自己加无限下级)                                 |                                            |
| profit               | true     | long | 盈亏                                                         |                                            |
| salary               | true     | long | 日工资                                                       |                                            |
| self_dividend        | false    | long | 自己的月分红                                                 | 月分红相关字段目前只有彩票渠道和总计里才有 |
| agent_dividend       | false    | long | 应该分给下级的月分红                                         |                                            |
| result_dividend      | true     | long | 最终的月分红<br>self_dividend-agent_dividend                 |                                            |
| game_withdraw_amount | true     | long | 游戏提现                                                     |                                            |
| game_recharge_amount | true     | long | 游戏充值                                                     |                                            |
| eusd_buy_num         | true     | long | eusd购买                                                     |                                            |
| eusd_sold_num        | true     | long | eusd出售                                                     |                                            |

