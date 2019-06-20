# 客户端 - 广告
## 获取广告列表

### HTTP 请求

- GET `/v1/banners`

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "123456789",
        "subject": "送iphone活动",
        "image": "https://baidu.com/huodong/1.png",
        "url": "https://baidu.com/huodong/1.html"
      },
      {
        "id": "123456790",
        "subject": "澳门行活动",
        "image": "https://baidu.com/huodong/2.png",
        "url": "https://baidu.com/huodong/2.html"
      }
    ]
  }
}
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围 |
| --------- | ------- | ------ | ---------- | ------- |
| id        | true    | long   | 广告 ID    |         |
| subject   | true    | string | 广告主题    |         |
| image     | true    | string | 广告图片地址 |         |
| url       | true    | string | 广告跳转链接 |         |
