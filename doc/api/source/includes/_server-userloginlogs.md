# 服务端 - 登陆日志
## 获取所有登陆日志

### HTTP 请求

- GET `/v1/admin/userloginlogs`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| mobile   | false   | string | NA    | 手机号
| page     | false   | int    | NA    | 当前显示分页号
| per_page | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": {
    "list": [
      {
        "id": "1",
        "user_id": "123456",
		"mobile":"15512345671"
        "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWeb...",
        "ips": "114.114.144.11",
        "ctime": 1494901162,
      },
      {
        "id": "2",
        "user_id": "234567",
		"mobile":"15512345671"
        "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWeb...",
        "ips": "114.114.144.11",
        "ctime": 1494901162,
      },
    ],
    "meta": {
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    }
  }
}
```