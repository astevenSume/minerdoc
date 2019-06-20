# 客户端 - 应用

## 获取渠道列表

### HTTP 请求

- GET `/v1/apps/channel`

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": 123456789,
		"is_third_hall":1,
        "name": "金龙",
        "desc": "金龙应用平台",
        "ctime": 1494901162595,
        "utime": 1494901162595
      },
      {
        "id": 123456790,
		"is_third_hall":2,
        "name": "无双",
        "desc": "无双应用",
        "ctime": 1494901162595,
        "utime": 1494901162595
      }
    ]
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述                | 取值范围 |
| ------------- | ------- | ------ | -------------------- | ------- |
| id            | true    | int   | 应用渠道 ID           |         |
| is_third_hall | true    | string | 渠道方是否有应用大厅 |1:有(直接登录应用大厅) 2:没有(请求后台配置游戏大厅即渠道应用列表,用渠道跟appid登录游戏)|
| name          | true    | string | 应用渠道名称         |         |
| desc          | true    | string | 应用渠道描述         |         |
| ctime         | false   | long   | 应用渠道创建时间     |         |
| utime         | false   | long   | 应用渠道更新时间     |         |



## 获取渠道应用列表

### HTTP 请求

- GET `/v1/apps/{channel_id}/list`

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "name": "租赁市场",
        "url": "https://baidu.com/app/1",
		"icon_url": "https://baidu.com/app/1",
        "desc": "去中心化CPU租赁市场",
        "type_id": 1,
        "channel_id": 1,
        "app_id": "327",
        "featured": 0,
		"orientation":1,
        "status": 2,
      },
      {
        "id": "123456790",
        "name": "糖果盒",
        "url": "https://baidu.com/app/2",
		"icon_url": "https://baidu.com/app/1",
        "desc": "免费领取EOS糖果",
        "type_id": 2,
        "channel_id": 1,
        "app_id": "328",
        "featured": 1,
		"orientation":1,
        "status": 3,
      }
    ],
    "type_list":[
      {
        "id": 1,
        "name": "全部",
        "desc": "XXXXXX"
      },
      {
        "id": 2,
        "name": "热门",
        "desc": "XXXXXX"
      }      
    ]
  }
}
```

### 响应数据

| 字段名称    | 是否必须 | 类型    | 描述       | 取值范围         |
| --------- | ------- | ------ | ---------- | -------------- |
| id        | true    | long   | 应用 ID    |                 |
| name      | true    | string | 应用名称    |                 |
| desc      | true    | string | 应用描述     |                |
| url       | true    | string | 应用地址     |                |
| icon_url  | true    | string | 应用图标地址 |				   |
| featured  | true    | int    | 是否推荐     | 1-不推荐, 2-推荐 |
| type_id   | true    | int    | 应用分类ID   |                |
| channel_id | true    | int    | 渠道ID   |                |
| app_id   | true    | string    | 渠道应用ID   |                |
| status   | true    | int    | 应用状态     |                |
| orientation | true    | int  | 应用朝向     |                |

- Status 状态定义

| 状态       | 定义    |
| ----------| ------- |
| 1         | 等待上线  |
| 2         | 已上线   |
| 3         | 计划上线 |

- orientation 定义

| 状态       | 定义    |
| ----------| ------- |
| 1         | 横屏    |
| 2         | 竖屏    |
