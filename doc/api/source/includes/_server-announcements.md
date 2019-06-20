# 服务端 - 公告管理
## 获取所有公告

### HTTP 请求

- GET `/v1/admin/announcements`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
|stime|false|int|NA|开始时间 时间戳|
|etime|false|int|NA|结束时间 时间戳|
|type|false|int|NA|公告类型|
|page|false|int|NA|当前显示分页号|
|limit|false|int|10|每页显示条数|

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 2,
				"type":1,
                "title": "test1",
                "content": "test2",
                "stime": 1557027460619,
                "etime": 1557906038000,
                "ctime": 1557041957673,
                "utime": 1557042065003
            }
        ],
        "meta": {
            "page": 1,
            "limit": 10,
            "total": 1
        }
    }
}
```

## 获取公告

### HTTP 请求

- GET `/v1/admin/announcements?id=3`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 公告 id

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 3,
		"type":1,
        "title": "test1",
        "content": "test2",
        "stime": 1557027460619,
        "etime": 1557027460619,
        "ctime": 1557042705690,
        "utime": 1557042705690
    }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 公告 ID    |         |
| type      | true    | int    | 公告 类型  |         |
| title   | true    | string | 公告标题    |         |
| content     | true    | string | 公告内容  |         |
| stime       | true    | long | 公告开始时间  |         |
| etime    | true    | long | 公告结束时间     |         |
| ctime     | false   | long   | 公告创建时间  |         |
| utime     | false   | long   | 公告更新时间  |         |

#### type 类型定义:

|ID | 类型         | 描述           |
| -----------| ----------- | -------------- |
|1| sys      | 系统公告    |
|2| game     | 游戏公告    |

## 创建公告

### HTTP 请求

- POST `/v1/admin/announcements`

```json
{
  "type":1,
  "title": "公告标题",
  "content": "公告内容",
  "stime": 1557027460619,
  "etime": 1557027460619,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| type    | true    | int   |        | 公告类型
| title   | true    | string |        | 公告标题
| content     | true    | string |        | 公告内容
| stime       | true    | long |        | 开始时间
| etime       | true    | long |        | 结束时间

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 3,
		"type":1,
        "title": "test1",
        "content": "test2",
        "stime": 1557027460619,
        "etime": 1557027460619,
        "ctime": 1557042705690,
        "utime": 1557042705690
    }
}
```

### 响应数据
返回的主数据对象是一个对应公告完整对象。

## 更新公告

### HTTP 请求

- PUT `/v1/admin/announcements/{id}`

```json
{
  "type":1,
  "title": "公告标题",
  "content": "公告内容",
  "stime": 1557027460619,
  "etime": 1557027460619,
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | ------ | ------ | -----------
| type   | true    | int |        | 公告类型
| title   | true    | string |        | 公告标题
| content     | true    | string |        | 公告内容
| stime       | true    | long |        | 开始时间
| etime       | true    | long |        | 结束时间

> Response:

```json
{
    "code": 200,
    "data": {
        "id": 2,
		"type":1,
        "title": "test1",
        "content": "test2",
        "stime": 1557027460619,
        "etime": 1557906038000,
        "utime": 1557042065003
    }
}
```

### 响应数据
返回的主数据对象是一个对应公告完整对象。


## 删除公告

### HTTP 请求

- DELETE `/v1/admin/announcements?id=1`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | long   | NA    | 公告 id

> Response:

```json
{  
  "data": {
    "id": 1
  }
}
```

### 响应数据

返回的主数据对象是一个对应公告id。