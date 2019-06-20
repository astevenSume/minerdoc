# 服务端 - 服务维护状态管理
## 获取所有版本

### HTTP 请求

- GET `/v1/admin/serverstop`


- Status 状态定义

| 状态       | 定义    |
| ----------| ------  |  
| 0         | 正常 
| 1         | 维护阶段1   
| 2         | 维护中   


> Response:

```json
{
    "code": 200,
    "data": {
        "list": {
            "1": "OTC服务",
            "2": "EUSD服务",
            "3": "USDT服务",
            "4": "游戏服务",
            "5": "OTC交易"
        },
        "status": {
            "1": "1",
            "2": "2",
            "3": "2",
            "4": "2",
            "5": 0
        }
    }
}
```

## 获取版本

### HTTP 请求

- POST `/v1/admin/serverstop/set`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| server  | true    | int    | NA    | 版本 id
| able    | true |bool|  |  true-开启 false-关闭

> PS: 关闭OTC服务分成两阶段(status=1、2),其他直接2阶段

> Response:

```json
{
    "code": 200,
    "data": {
        "list": {
            "1": "OTC服务",
            "2": "EUSD服务",
            "3": "USDT服务",
            "4": "游戏服务",
            "5": "OTC交易"
        },
        "result": {
            "1": "1",
            "2": "2",
            "3": "2",
            "4": "2",
            "5": 0
        }
    }
}
```

## 服务维护日志（cron暂停日志，从redis读取）

### HTTP 请求

- GET `/v1/admin/serverstop/log`

> Response:

```json
{
    "code": 200,
    "data": [
        "TransferRun:20190517163900",
        "TransferCheck:20190517163900"
    ]
}
```
