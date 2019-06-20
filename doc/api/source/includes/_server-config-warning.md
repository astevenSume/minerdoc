# 服务端 - 预警配置

## 获取所有预警配置

### HTTP 请求

- GET `/v1/admin/configwarning`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| type     | false   | int    |        | 
| mobile   | false   | string |        |   
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
        "type": 1,
		"national_code":"86",
        "mobile": "1234567890",
      },
      {
        "id": 123456789,
        "type": 1,
		"national_code":"86",
        "mobile": "1234567890",
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

| 字段名称      | 是否必须 | 类型   | 描述      | 取值范围        |
| --------------| ------- | ------ | ---------- | --------------- | 
| id            | true    | int    | 配置 ID    |                 |
| type          | true    | int    | 预警type   |见下表定义       |
| national_code | true    | string | 国家码     | 目前不支持国内86|
| mobile        | true    | string | 通知手机号 |                 |


-系统预警类型 type 定义：
| 状态      | 描述    |
| --------- | -----   |
| 1         | usdt转账|



## 创建预警配置

### HTTP 请求

- POST `/v1/admin/configwarning`

```json
{
	"type": 1,
	"national_code":"86",
	"mobile": "1234567890",
}
```

### 请求参数

| 参数名称      | 是否必须| 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ------ | -----------
| type          | true    | int    |        |                 |
| national_code | true    | string |        | 目前不支持国内86|
| mobile        | true    | string |        |                 |

> Response:


### 响应数据
返回对应错误码。

## 更新预警配置

### HTTP 请求

- PUT `/v1/admin/configwarning`

```json
{
	"id": 123456789,
	"type": 1,
	"national_code":"86",
	"mobile": "1234567890",
}
```

### 请求参数

| 参数名称      | 是否必须| 类型   | 默认值 | 描述 
| ------------- | ------- | ------ | ------ | -----------
| id            | true    | int    |        | 配置ID
| type          | true    | int    |        |                 |
| national_code | true    | string |        | 目前不支持国内86|
| mobile        | true    | string |        |                 |

> Response:


### 响应数据
返回对应错误码。


## 删除预警配置

### HTTP 请求

- DELETE `/v1/admin/configwarning?id=123456789`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | --------- | ------ | ----- | -----------
| id      | true      | int    | NA    | 配置 id

> Response:


### 响应数据

返回对应错误码。
