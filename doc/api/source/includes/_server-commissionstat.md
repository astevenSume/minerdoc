# 服务端 - 佣金统计
## 获取所有佣金统计信息

### HTTP 请求

- GET `/v1/admin/commissionstat`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| status   | false   | int    | NA    | 发放状态
| page     | false   | int    | NA    | 当前显示分页号
| limit    | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "ctime": 1554739200,
        "tax": "1.1233",
        "channel": "1.1233",
        "commission": "1.1233",
        "profit": "1.1233",
        "utime": 1554739200,
		"status":1
      },
      {
        "ctime": 1554739200,
        "tax": "1.1233",
        "channel": "1.1233",
        "commission": "1.1233",
        "profit": "1.1233",
        "utime": 1554739200,
		"status":1
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

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| ctime     | true    | long   | 每天0点时间戳单位秒  |         |
| tax       | true    | string | 税收                 |         |
| channel   | true    | string | 渠道                 |         |
| commission| true    | string | 佣金                 |         |
| profit    | true    | string | 利润                 |         |
| utime     | true    | long   | 更新时间单位秒       |         |
| status    | true    | int    | 发放状态             |         |


-发放状态 status 定义：
| 状态      | 描述   |
| --------- | -----  |
| 1         | 未发放 |
| 2         | 已发放 |



## 发放佣金

### HTTP 请求

- POST `/v1/admin/commissionstat/distribute`

### 请求参数

| 参数名称 | 是否必须 | 类型    | 默认值 | 描述 
| ------ | ------- | ------ | ----- | -----------
| ctime  | true    | long   | NA    | 列表中的时间戳

> Response:

### 响应数据

返回的错误码。
