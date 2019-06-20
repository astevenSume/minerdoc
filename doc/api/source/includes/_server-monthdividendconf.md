# 服务端 - 月分红配置管理
## 获取所有月分红配置

### HTTP 请求

- GET `/v1/admin/monthdividendconf/conf`

### 请求参数



> Response:

```json
{
    "code": 200,
    "data": {
        "list": {
            "1": [
                {
                    "id": 1,
                    "agent_lv": 1,
                    "position": 1,
                    "max": 1,
                    "dividend_ratio": 25,
                    "ctime": 1559282445809,
                    "utime": 1559282445809
                },
                {
                    "id": 2,
                    "agent_lv": 1,
                    "position": 2,
                    "min": 1,
                    "max": 5,
                    "activity_num": 5,
                    "dividend_ratio": 30,
                    "ctime": 1559282445809,
                    "utime": 1559282445809
                },
                {
                    "id": 3,
                    "agent_lv": 1,
                    "position": 3,
                    "min": 5,
                    "max": 15,
                    "activity_num": 10,
                    "dividend_ratio": 35,
                    "ctime": 1559282445809,
                    "utime": 1559282445809
                },
                {
                    "id": 4,
                    "agent_lv": 1,
                    "position": 4,
                    "min": 15,
                    "max": 60,
                    "activity_num": 15,
                    "dividend_ratio": 40,
                    "ctime": 1559282445809,
                    "utime": 1559282445809
                },
                {
                    "id": 5,
                    "agent_lv": 1,
                    "position": 5,
                    "min": 60,
                    "max": 150,
                    "activity_num": 20,
                    "dividend_ratio": 45,
                    "ctime": 1559282445809,
                    "utime": 1559282445809
                },
                {
                    "id": 6,
                    "agent_lv": 1,
                    "position": 6,
                    "min": 150,
                    "activity_num": 30,
                    "dividend_ratio": 50,
                    "ctime": 1559282445809,
                    "utime": 1559282445809
                }
            ],
            "2": [
                {
                    "id": 41,
                    "agent_lv": 2,
                    "position": 1,
                    "max": 1,
                    "dividend_ratio": 15,
                    "ctime": 1559282581178,
                    "utime": 1559282581178
                },
                {
                    "id": 42,
                    "agent_lv": 2,
                    "position": 2,
                    "min": 1,
                    "max": 4,
                    "activity_num": 5,
                    "dividend_ratio": 20,
                    "ctime": 1559282581178,
                    "utime": 1559282581178
                },
                {
                    "id": 43,
                    "agent_lv": 2,
                    "position": 3,
                    "min": 4,
                    "max": 12,
                    "activity_num": 10,
                    "dividend_ratio": 25,
                    "ctime": 1559282581178,
                    "utime": 1559282581178
                },
                {
                    "id": 44,
                    "agent_lv": 2,
                    "position": 4,
                    "min": 12,
                    "max": 45,
                    "activity_num": 15,
                    "dividend_ratio": 30,
                    "ctime": 1559282581178,
                    "utime": 1559282581178
                },
                {
                    "id": 45,
                    "agent_lv": 2,
                    "position": 5,
                    "min": 45,
                    "max": 100,
                    "activity_num": 20,
                    "dividend_ratio": 35,
                    "ctime": 1559282581178,
                    "utime": 1559282581178
                },
                {
                    "id": 46,
                    "agent_lv": 2,
                    "position": 6,
                    "min": 100,
                    "activity_num": 30,
                    "dividend_ratio": 40,
                    "ctime": 1559282581178,
                    "utime": 1559282581178
                }
            ],
            "3": [
                {
                    "id": 81,
                    "agent_lv": 3,
                    "position": 1,
                    "max": 1,
                    "dividend_ratio": 5,
                    "ctime": 1559282824363,
                    "utime": 1559282824363
                },
                {
                    "id": 82,
                    "agent_lv": 3,
                    "position": 2,
                    "min": 1,
                    "max": 3,
                    "activity_num": 5,
                    "dividend_ratio": 10,
                    "ctime": 1559282824363,
                    "utime": 1559282824363
                },
                {
                    "id": 83,
                    "agent_lv": 3,
                    "position": 3,
                    "min": 3,
                    "max": 8,
                    "activity_num": 10,
                    "dividend_ratio": 15,
                    "ctime": 1559282824363,
                    "utime": 1559282824363
                },
                {
                    "id": 84,
                    "agent_lv": 3,
                    "position": 4,
                    "min": 8,
                    "max": 30,
                    "activity_num": 15,
                    "dividend_ratio": 20,
                    "ctime": 1559282824363,
                    "utime": 1559282824363
                },
                {
                    "id": 85,
                    "agent_lv": 3,
                    "position": 5,
                    "min": 30,
                    "max": 60,
                    "activity_num": 20,
                    "dividend_ratio": 25,
                    "ctime": 1559282824363,
                    "utime": 1559282824363
                },
                {
                    "id": 86,
                    "agent_lv": 3,
                    "position": 6,
                    "min": 60,
                    "activity_num": 30,
                    "dividend_ratio": 30,
                    "ctime": 1559282824363,
                    "utime": 1559282824363
                }
            ]
        }
    }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 返佣等级 ID    |         |
| min       | true    | Int | 月分红开始金额 单位万 |         |
| max       | true    | Int | 月分红结束金额 单位万 |         |
| position | true    | Int | 该等级下的档位信息 |         |
| ctime     | true | long   | 返佣等级创建时间 |         |
| utime     | true | long   | 返佣等级更新时间 |         |
| activity_num | true | int | 下级代理的活跃人数 | |
| dividend_ratio | true | Int | 分红百分比 | |
| agent_lv | true | int | 该配置对应的代理等级 | |

## 创建月分红等级

### HTTP 请求

- POST `/v1/admin/monthdividendconf/conf`

```json
{ 
  "data": 
  [
    {
  	  "position":1,
  	  "agent_lv":1,
      "min": 2000,
      "max": 15000,
  	  "dividend_ratio":25,
      "activity_num": 0
    },
	{
	    "position":2,
	    "agent_lv":1,
	    "min": 15000,
	    "max": 50000,
	    "dividend_ratio":30,
	    "activity_num": 5
	},
	{
  	  "position":3,
  	  "agent_lv":1,
      "min": 50000,
      "max": 150000,
  	  "dividend_ratio":35,
      "activity_num": 10
    },
    {
  	  "position":4,
  	  "agent_lv":1,
      "min": 150000,
      "max": 600000,
  	  "dividend_ratio":40,
      "activity_num": 15
    },
    {
  	  "position":5,
  	  "agent_lv":1,
      "min": 600000,
      "max": 1500000,
  	  "dividend_ratio":45,
      "activity_num": 20
    },
    {
  	  "position":6,
  	  "agent_lv":1,
      "min": 1500000,
      "max": 0,
  	  "dividend_ratio":50,
      "activity_num": 30
    }
  ]
}

```

### 请求参数

| 参数名称       | 是否必须 | 类型 | 默认值 | 描述                                   |
| -------------- | -------- | ---- | ------ | -------------------------------------- |
| position       | true     | int  |        | 档位，根据dividend_ratio排档位         |
| min            | true     | int  |        | 该阶段月分红最小值，单位是元           |
| max            | true     | int  |        | 该阶段月分红最大值，单位是元           |
| dividend_ratio | true     | int  |        | 分红比例，按照这个值排序，单位是百分比 |
| activity_num   | true     | int  |        | 要达到的活跃人数                       |
| agent_lv       | true     | int  |        | 该配置对应的代理等级                   |

> Response:

```json
{"code":200}
```

### 响应数据
返回的主数据对象和传递过来的内容一样


## 获取月分红配置中的档位数据

### HTTP 请求

- GET `v1/admin/monthdividendconf/positionconf`

> Response:

```json
{
    "code": 200,
    "data": {
        "list": {
            "1": [
                {
                    "position": 1,
                    "dividend_ratio": 25
                },
                {
                    "position": 2,
                    "dividend_ratio": 30
                },
                {
                    "position": 3,
                    "dividend_ratio": 35
                },
                {
                    "position": 4,
                    "dividend_ratio": 40
                },
                {
                    "position": 5,
                    "dividend_ratio": 45
                },
                {
                    "position": 6,
                    "dividend_ratio": 50
                }
            ],
            "2": [
                {
                    "position": 1,
                    "dividend_ratio": 15
                },
                {
                    "position": 2,
                    "dividend_ratio": 20
                },
                {
                    "position": 3,
                    "dividend_ratio": 25
                },
                {
                    "position": 4,
                    "dividend_ratio": 30
                },
                {
                    "position": 5,
                    "dividend_ratio": 35
                },
                {
                    "position": 6,
                    "dividend_ratio": 40
                }
            ],
            "3": [
                {
                    "position": 1,
                    "dividend_ratio": 5
                },
                {
                    "position": 2,
                    "dividend_ratio": 10
                },
                {
                    "position": 3,
                    "dividend_ratio": 15
                },
                {
                    "position": 4,
                    "dividend_ratio": 20
                },
                {
                    "position": 5,
                    "dividend_ratio": 25
                },
                {
                    "position": 6,
                    "dividend_ratio": 30
                }
            ]
        }
    }
}
```



## 删除指定等级的配置数据

### HTTP请求

- DELETE `v1/admin/monthdividendconf/conf`

### 请求参数

| 参数名称 | 是否必须 | 类型 | 默认值 | 描述                                         |
| -------- | -------- | ---- | ------ | -------------------------------------------- |
| level    | 是       | Int  | 0      | 要删除的配置的等级，只能是最后一个配置的等级 |

> Response:

```json
{  
  "code":200,
}

//如果配置有5个等级的配置，level传了4或者比4小的数进来因为还有等级为5的没有删除，所以会返回下面删除失败的数据
{  
  
  "code":224,
  "msg":"只能删除最低等级的配置",
}
```




# 服务端 - 代理月分红等级管理

## 添加代理到指定月分红档位

### HTTP 请求

- POST `/v1/admin/agentmonthdividend/agents`

### 请求参数

| 参数名称      | 是否必须 | 类型    | 默认值  | 描述 
| ------------- | ------- | ------ | ------ | -----------
| mobile  | true    | int    | NA     | 代理用户 手机号
| position_id           | true    | int   | NA     | 分红档位id

> Response:

```json
{  
  "data": {
    "mobile": 13559185291,
    "position_id": 1
  }
}
```

### 响应数据

返回的主数据对象是一个对应代理白名单档位id及代理用户id。

## 从月分红档位删除代理

### HTTP 请求

- DELETE `/v1/admin/agentmonthdividend/agents?uid=123456`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| uid     | true    | int    | NA    | 代理用户 id

> Response:

```json
{
    "code": 200,
    "data": {
        "uid": "123456"
    }
}
```

### 响应数据

返回的主数据对象是一个代理用户id。

## 分页获取指定档位的代理数据

### HTTP 请求

- get `/v1/admin/agentmonthdividend/agents?uid=123456`

### 请求参数

| 参数名称    | 是否必须 | 类型 | 默认值 | 描述             |
| ----------- | -------- | ---- | ------ | ---------------- |
| agent_level | 是       | int  | 1      | 代理等级         |
| position    | 是       | int  | 1      | 月分红配置档位   |
| page        | 是       | int  | 1      | 页数             |
| limit       | 是       | int  | 10     | 每页需要数据数量 |
> Response:

```json
{
    "code": 200,
    "data": {
        "list":[
          {
            "uid":1,
            "level":1,
            "ctime":1234567,
            "dividend_position":1
          },
          {
            "uid":2,
            "level":1,
            "ctime":12345678,
            "dividend_position":1
          }
        ]
    }
}
```


