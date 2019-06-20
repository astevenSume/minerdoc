# 服务端 - 查询用户游戏中充值、提现记录

## 获取所有游戏帐号充值、提现记录

### HTTP 请求

- GET `/v1/admin/game/chargeinfo`

### 请求参数

| 参数名称        | 是否必须 | 类型   | 默认值 | 描述 
| --------------- | -------  | ------- | -----  | -----------
| uid or mobile   | ture     | string  | NA     | uid or mobile
| transfertype    | false    | int     | 0      | 0 全部 1 充值 2 提现
| page            | false    | int     | 1      | page
| limit           | false    | int     | 10     | limit
   

> Response:

```json
{
    "code":200,
    "data":{
        "list":[
            {
                "uid":188551845679988740,
                "channel_id":1,
                "account":"slong",
                "transfer_type":1,
                "order":"3",
                "game_order":"1",
                "coin_integer":"423770.0000",
                "eusd_integer":"123703.4000",
                "status":2,
                "ctime":1559719063134,
                "desc":"aaab",
                "step":"2"
            },
            {
                "id":1,
                "uid":188551845679988740,
                "channel_id":1,
                "transfer_type":2,
                "coin_integer":"423771.1122",
                "eusd_integer":"2323703.4000"
            }
        ],
        "meta":{
            "page":1,
            "limit":10,
            "total":3
        }
    }
}
```
### 响应数据

| 字段名称     | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | -------- | ------ | ---------- | ------- |
| uid          | false    | bigint | 用户 ID    |         |
| channel_id   | false    | int    | 用户姓名   |         |
| account      | false    | varchar| 帐号       |         |
| transfer_type| false    | int    | 转换类型   |         |
| order        | false    | varchar| 订单       | 1, 2, 3, 4 |
| game_order   | false    | varchar| 游戏订单   | 0不是 1是|     
| coin_integer | false    | bigint | 游戏币     |         |
| eusd_integer | false    | bigint | eusd币     |         |
| status       | false    | int    | 状态       |         |
| ctime        | false    | bigint | 创建时间   |         |
| desc         | false    | varchar| 描述       | true是  |
| step         | false    | varchar| 步骤       |         |
