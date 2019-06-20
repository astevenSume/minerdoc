# 客户端 - 通知

## 通知类型: 
| 类型      | 描述    |
| -------- | ------- |
| system   | 系统通知 |
| fund     | 资金通知 |
| withdraw | 提现通知 |

## 获取通知统计

### HTTP 请求

- GET `/v1/notification/statistics`

> Response:

```json
{  
  "data": {
    "unread_count": 4,
    "last_ctime": 1494901162595,
  }
}
```

### 响应数据

| 字段名称       | 是否必须 | 类型   |  描述         | 取值范围 |
| ------------- | ------- | ------ | ------------ | ------- |
| unread_count  | true    | int    | 未读通知数量    |         |
| last_ctime    | true    | long   | 最后一条通知时间 |         |

## 获取通知列表

### HTTP 请求

- GET `/v1/notifications`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 默认值 | 描述 
| --------- | ------- | -----  | ----- | -----------
| type      | false   | string | NA    | 通知类型
| page      | false   | int    | NA    | 当前显示分页号
| per_page  | false   | int    | 10    | 每页显示条数

> Response:

```json
{
  "data": {
    "list": [
      {
        "id": "28290050-b655-4709-b004-dd1be04974e8",
        "ctime": 1494901162595,
        "read_at": null,
        "type": "system",
        "content": "这是一条系统通知",
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

| 字段名称      | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| id           | true    | long   | 通知 ID     |         |
| ctime        | true    | long   | 通知创建时间 |         |
| read_at      | true    | long   | 通知已读时间 |         |
| type         | true    | string | 通知类型    |         |
| content      | true    | text   | 通知内容    |         |

## 标记通知已读 （不需要，只要前端请求，直接标记已读）

### HTTP 请求

- PUT `/v1/notifications`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| type     | false   | string | NA    | 通知类型

> Response:

```json
{
  "data": {
    "ids": ["28290050-b655-4709-b004-dd1be04974e8", ...]
  }
}
```

### 响应数据
返回的主数据对象是标记已读的通知id数组.