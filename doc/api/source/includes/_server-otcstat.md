# 服务端 - OTC服务数据统计
## 获取OTC整体报表

### HTTP 请求

- GET `/v1/admin/otcstat`

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1,
                "date": 20190527,
                "num_order": 0,  //订单总数
                "num_login": 0, // 登录人数
                "num_user_new": 0, //新增人数
                "num_order_deal": 0, //完成的订单
                "num_funds": 0, // 交易金额（完成）
                "num_amount": 0,// 交易EUSD
                "num_fee": 0, // 手续费
                "num_game_income": 0, //游戏充值
                "num_game_expend": 0, //游戏提现
            }
        ],
        "meta": {
            "total": 1,
            "page": 1,
            "limit": 20,
            "total_page": 1,
            "offset": 0
        },
        "today": {
            "date": 20190528,
            "num_order": 0,  //订单总数
            "num_login": 0, // 登录人数
            "num_user_new": 0, //新增人数
            "num_order_deal": 0, //完成的订单
            "num_funds": 0, // 交易金额（完成）
            "num_amount": 0,// 交易EUSD
            "num_fee": 0, // 手续费
            "num_game_income": 0, //游戏充值
            "num_game_expend": 0, //游戏提现
        }
    }
}
```

## 获取个人OTC统计信息

### HTTP 请求

- GET `/v1/admin/otcstat/user`

### 请求参数
| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | -----  | ------- | -----------
| uid     | false   | int |    | 

> Response:

```json
{
    "code": 200,
    "data": {
        "num_amount_buy": 900000, // 购买的EUSD
        "num_amount_sell": 0, // 出售的EUSD
        "num_order_buy": 0, // 购买EUSD的订单
        "num_order_sell": 0, // 出售EUSD的订单
        "usdt_recharge": 0, //USDT 充值
        "usdt_withdrawal": 0 //USDT 提现
    }
}
```
