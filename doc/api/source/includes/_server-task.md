# 服务端 - 定时任务管理
## 查询定时任务

### HTTP 请求

- GET `/v1/admin/task/query?appname=otc&page=1&limit=2`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| appname   | true    | string |        | 定时任务对应的服务应用名称
| page      | true    | int    |        | 页码
| limit     | true    | int    |        | 每页显示条数 

> Response:

```json
{  
    "code": 200,
    "data": {
        "list": [
            {
                "id": 5,
                "name": "SynUsdtPrice1",
                "alia": "同步usdt价格",
                "app_name": "otc",
                "func_name": "SyncUsdtPrice",
                "spec": "0 */5 * * * *",
                "status": 1,
                "ctime": 1559636947,
                "utime": 1559636947,
                "desc": "从okex和huobiex查询usdt的买卖价格推算出usdt当前的人民币价格"
            },
            {
                "id": 4,
                "name": "SyncBtcPrice",
                "alia": "同步btc价格",
                "app_name": "otc",
                "func_name": "SyncBtcPrice",
                "spec": "0 */5 * * * *",
                "status": 1,
                "ctime": 1559636311,
                "utime": 1559636947,
                "desc": "从okex和huobiex查询btc的买卖价格推算出usdt当前的人民币价格"
            }
        ],
        "meta": {
            "page": 1,
            "limit": 2,
            "total": 2
        }
    }
}
```

## 查询单个服务节点定时任务

### HTTP 请求

- GET `/v1/admin/task/querysingle?appname=otc&region_id=0&server_id=0`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| appname   | true    | string |        | 定时任务对应的服务应用名称
| region_id | true    | int    |        | 应用区域编码，[0,15]
| server_id | true    | int    |        | 应用服务编码，[0,1023]
| spec      | true    | string |        | 定时任务启动时间格式化字符串
| switch    | true    | int    |        | 任务开关 0-关闭，1-开启
| status    | true    | int    |        | 任务开关 0-空闲，1-运行中
| prev      | true    | uint32    |        | 上次运行时间戳
| next      | true    | uint32    |        | 下次运行时间戳

> Response:

```json
{  
    "code": 200,
    "data": {
        "app_name":"otc",
        "region_id":0,
        "server_id":1, 
        "list": [
            {
                "name": "SynUsdtPrice",
                "spec": "0 */5 * * * *",
                "status": 1,
                "switch":1,
                "prev":1560066449,
                "next":1560066449  
            },
            {
                "name": "SynBtcPrice",
                "spec": "0 */5 * * * *",
                "status": 1,
                "switch":1,
                "prev":1560066449,
                "next":1560066449  
            }
        ]
    }
}
```

## 查询定时任务结果

### HTTP 请求

- GET `/v1/admin/task/result?page=1&limit=20`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| appname   | true    | string |        | 定时任务对应的服务应用名称
| region_id | true    | int    |        | 应用区域编码，[0,15]
| server_id | true    | int    |        | 应用服务编码，[0,1023]
| page      | true    | int    |        | 页码
| limit     | true    | int    |        | 每页显示条数
| name      | true    | string |        | 定时任务名称
| begin_time| true    | uint32 |        | 开始时间戳
| end_time  | true    | uint32 |        | 结束时间戳
| ctime     | true    | uint32 |        | 创建时间戳 

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1,
                "app_name": "otc",
                "server_id": 1,
                "name": "SynUsdtPrice1",
                "end_time": 1559804895,
                "begin_time": 1559804880,
                "ctime": 1559804895
            },
            {
                "id": 4,
                "app_name": "otc",
                "server_id": 1,
                "name": "SynUsdtPrice1",
                "end_time": 1559804910,
                "begin_time": 1559804895,
                "ctime": 1559804910
            },
            {
                "id": 7,
                "app_name": "otc",
                "server_id": 1,
                "name": "SynUsdtPrice1",
                "end_time": 1559805045,
                "begin_time": 1559805030,
                "ctime": 1559805045
            }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 370
        }
    }
}        
```

## 增加定时任务

### HTTP 请求

- POST `/v1/admin/task/add`

```json
{
  "name": "SyncUdstPrice",
  "alia": "同步USDT行情价格",
  "spec": "0 */5 * * * *",
  "app_name": "otc",
  "func_name": "SyncUsdtPrice",
  "desc": "从okex和huobiex查询usdt的买卖价格推算出usdt当前的人民币价格"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| name       | true    | string |        | 定时任务名称，用英文标识
| alia       | true    | string |        | 定时任务别名
| spec       | true    | string |        | 定时任务执行时间，参照linux cron 时间格式
| app_name   | true    | string |        | 定时任务对应的服务应用名称
| func_name  | true    | string |        | 定时任务对应的服务函数名称
| desc       | true    | string |        | 定时任务描述 

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 12,
        "name": "SyncBtcPrice",
        "alia": "同步btc价格",
        "app_name": "otc",
        "func_name": "SyncBtcPrice",
        "spec": "0 */30 * * * *",
        "status": 1,
        "ctime": 1559806375,
        "utime": 1559806375
    }
}
```

## 编辑定时任务

### HTTP 请求

- POST `/v1/admin/task/edit`

```json
{
	"id": 12,
    "name": "SyncBtcPrice",
    "alia": "同步btc价格",
    "app_name": "otc",
    "func_name": "SyncBtcPrice",
    "spec": "0 */30 * * * *",
    "desc":"从okex和huobiex查询usdt的买卖价格推算出btc当前的人民币价格",
    "status": 1
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| name       | true    | string |        | 定时任务名称，用英文标识
| alia       | true    | string |        | 定时任务别名
| spec       | true    | string |        | 定时任务执行时间，参照linux cron 时间格式
| app_name   | true    | string |        | 定时任务对应的服务应用名称
| func_name  | true    | string |        | 定时任务对应的服务函数名称
| desc       | true    | string |        | 定时任务描述
| status     | true    | int    |        | 定时任务状态，0-disable 1-enable  

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 12,
        "name": "SyncBtcPrice",
        "alia": "同步btc价格",
        "app_name": "otc",
        "func_name": "SyncBtcPrice",
        "spec": "0 */30 * * * *",
        "status": 1,
        "ctime": 1559806375,
        "utime": 1559808753
    }
}
```

## 删除定时任务

### HTTP 请求

- POST `/v1/admin/task/del`

```json
{
	"id":12
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| id         | true    | int    |        | 定时任务标识

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 12
    }
}
```

## 下发定时任务到所有服务节点

### HTTP 请求

- POST `/v1/admin/task/distribute`

```json
{
	"id":12
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| id         | true    | int    |        | 定时任务标识

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 12
    }
}
```

## 启动/暂停所有服务节点定时任务

### HTTP 请求

- POST `/v1/admin/task/switch`

```json
{
	"id":4,
	"status":0
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| id         | true    | int    |        | 定时任务标识
| status     | true    | int    |        | 定时任务状态，0-disable 1-enable

> Response:

```json
{
    "code": 200
}
```

## 启动/暂停指定服务节点定时任务

### HTTP 请求

- POST `/v1/admin/task/switchsingle`

```json
{
	"id":4,
	"region_id":0,
	"server_id":0,
	"status":0
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| ---------  | ------- | ------ | ------ | -----------
| id         | true    | int    |        | 定时任务标识
| region_id  | true    | int    |        | 应用区域编码，[0,15]
| server_id  | true    | int    |        | 应用服务编码，[0,1023]
| status     | true    | int    |        | 定时任务状态，0-disable 1-enable

> Response:

```json
{
    "code": 200
}
```
