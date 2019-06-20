# 服务端 - 平台账号组

## 添加平台账号组分类

### HTTP 请求

- POST `/v1/admin/platformusercate/add`

```json
{
	"name":"分红"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| name         | true    | string |        | 分类名称

> Response:

```json
{
  "code": 200
}
```



## 平台账号组分类列表

### HTTP 请求

- GET `/v1/admin/platformusercate`

> Response:

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1,
                "name": "游戏平台",
                "ctime": 1556532348
            },
            {
                "id": 2,
                "name": "分红",
                "ctime": 1556533077
            }
        ]
    }
}

```


## 增加平台账号

### HTTP 请求

- POST `/v1/admin/platformuser/add`

```json
{
	"pid":1,
	"uid": ""
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| pid         | true    | int |        | 分类ID
| uid         | true    | string |     | 用户ID，="" 临时创建一个账号，不可登录

> Response:

```json
{
  "code": 200
}
```



## 平台账号列表

### HTTP 请求

- GET `/v1/admin/platformuser`

> Response:

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "uid": 175228111384739840,
                "status": 1,
                "account": "123123asdv",
                "id": 1,
                "name": "游戏平台"
            }
        ]
    }
}

```

## 设置平台账号状态

### HTTP 请求

- POST `/v1/admin/platformuser/status`

```json
{
	"status":1,
	"uid": "1"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| status         | true    | int |        | 状态 1-可用，0-不可用
| uid         | true    | string |     | 用户ID

> Response:

```json
{
  "code": 200
}
```
