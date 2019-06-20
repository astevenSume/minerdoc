# 客户端 - 公告
## 获取公告列表

### HTTP 请求

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
|type|true|int|NA|公告类型|


- GET `/v1/announcements/{type}`

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
        ]
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

|ID  | 描述        |
|----| ----------- |
|1   | 系统公告    |
|2   | 游戏公告    |