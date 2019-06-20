# 客户端 - 邀请返佣

## 获取代理汇总信息

### HTTP 请求

- GET `/v1/agent`

> Response:

```json
{  
  "data": {
    "invite_code": "hdai3",
    "sum_salary": 50074362,
    "sum_can_withdraw": 12344362,
    "yesterday_chips": 100000000,
    "invite_num": 3,
    "invite_url":"https://renrenotc.com/hc?code=VG6MDE"
  }
}
```

### 响应数据

| 字段名称         | 是否必须 | 类型   | 描述          | 取值范围 |
| ---------------- | -------  | ------ | ------------  | ------- |
| invite_code      | true     | string | 邀请码        |         |
| invite_num       | true     | int    | 已邀请人数    |         |
| sum_salary       | true     | long   | 累计日工资    |         |
| sum_can_withdraw | true     | long   | 可用提现余额  |         |
| yesterday_chips  | true     | long   | 昨日业绩      |         |
| invite_url       | true     | string | 邀请链接      |         |
sum_salary,sum_can_withdraw,yesterday_chips需要除以10000

## 提现

### HTTP 请求

- POST `/v1/agent/withdraw`

```json
{
  "amount": 5000,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型 | 描述      | 取值范围 |
| --------- | ------- | ------ | --------  | ------- |
| amount    | true    | long   | 提币数量  |        |
amount除以10000等于eusd个数
例如amount=5000即提现0.5个eusd


> Response:

```json
{
  "data": {
    "id": 12345678,
    "amount": 5000,
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "status": 1,
  }
}
```

### 响应数据

返回的主数据对象是一个对应提现数据。


## 获取所有提现记录

### HTTP 请求

- GET `/v1/agent/withdraws`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ----- | ------ | -----------
| time     | false   | string | NA    | 时间过滤条件，例如：2019-03 表示查询2019年3月
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list":[ 
      {
        "id": 12345678,
        "amount": 5000,
        "ctime": 1494901162595,
        "utime": 1494901162595,
        "status": 1,
      },
      ...
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

| 字段名称 | 是否必须 | 类型   | 描述       | 取值范围    |
| ------- | ------- | ------ | ---------- | --------- |
| id      | true    | long   | 提现 ID    |            |
| amount  | true    | long   | 提现金额    |           |
| status  | true    | int    | 状态        | 状态参见下表|
| ctime   | true    | long   | 发起时间    |           |
| utime   | true    | long   | 最后更新时间 |           |

#### Status 状态定义：

| 枚举 | 状态            | 描述        |
| ----- | --------------- | ---------- |
| 1 | submitted  | 处理中 |
| 2 | decreased  | 已扣除 |
| 3 | done | 已完成 |
| 4 | failed | 失败 |


## 获取代理详细汇总信息

### HTTP 请求

- GET `/v1/agent/sumdetail`

> Response:

```json
{  
  "data": {
    "status": 1,
    "salary": 50000,
    "sum_salary": 100000,
    "month_bonus": 100000000,
	"sum_month_bonus": 100000000,
	"sum_can_withdraw": 50000,
    "sum_withdraw": 100000,
  }
}
```

### 响应数据

| 字段名称          | 是否必须 | 类型   | 描述       | 取值范围 |
| ---------------   | ------- | ------ | ------------ | ------- |
| status            | true    | int    | 账户状态     |         |
| salary            | true    | long   | 昨天工资     |         |
| sum_salary        | true    | long   | 累计日工资   |         |
| month_bonus       | true    | long   | 上月月分红     |         |
| sum_month_bonus   | true    | long   | 累计月分红   |         |
| sum_can_withdraw  | true    | long   | 可用提现余额 |         |
| sum_withdraw      | true    | long   | 累计已提现   |         |

#### Status 状态定义：

| 枚举  | 描述       |
| ----- | ---------- |
| 0     | 锁定       |
| 1     | 正常       |

status 除外其他字段精度为4 需要除以10000



## 获取代理工资列表

### HTTP 请求

- GET `/v1/agent/game/salary`

### 请求参数

| 参数名称  | 是否必须| 类型   | 默认值   | 描述 
| --------  | ------- | ------ | -------- | -----------
| btime     | true    | long   |          | 查询起始时间
| etime     | true    | long   |          | 查询结束时间

> Response:

```json
{  
  "data": {
    "list":[ 
      {
        "salary": 12345678,
        "status": 1,
        "ctime": 1494901162595,
		"type": 1,
      },
      ...
    ]
  }
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述        | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
| salary          | true    | long   | 工资         |         |
| status          | true    | int    | 领取状态     |1已发放 2未发放 3:等待发放|
| ctime           | true    | long   | 工资时间     |         |
| type            | true    | int    | 类型         |1日工资 2月分红         |


## 获取代理日工资详情

### HTTP 请求

- GET `/v1/agent/game/daysalary/{timestamp}`

> Response:

```json
{  
  "data": {
    "list":[ 
      {
        "channel_id": 1,
        "salary": 10000,
        "total_valid_bet": 10000,
		"profit": 10000
      },
      ...
    ]
  }
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述        | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
| channel_id      | true    | int    | 渠道         |         |
| salary          | true    | long   | 工资         |         |
| total_valid_bet | true    | long   | 有效投注金额 |         |
| profit          | true    | long   | 盈亏         |         |

#### channel_id 渠道定义：

| 枚举  | 描述       |
| ----- | ---------- |
| 1     | 开元棋牌   |
| 2     | AG         |
| 3     | 彩票       |



## 获取游戏累计充值提现详情

### HTTP 请求

- GET `/v1/agent/game/transferInfo`

### 请求参数

| 参数名称  | 是否必须| 类型   | 默认值   | 描述 
| --------  | ------- | ------ | -------- | -----------
| btime     | true    | long   |          | 查询起始时间
| etime     | true    | long   |          | 查询结束时间

> Response:

```json
{  
  "data": {
    "list":[ 
      {
        "channel_id": 1,
        "transfer_type": 1,
        "amount": "1.21",//1.21个eusd
      },
      ...
    ]
  }
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述        | 取值范围  |
| --------------- | ------- | ------ | ------------ | ----------|
| channel_id      | true    | int    | 渠道         |           |
| transfer_type   | true    | int    | 1充值2提现   |           |
| amount          | true    | string | 提现单位eusd |           |
