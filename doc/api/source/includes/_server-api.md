# 服务端 - api接口

## usdt 账号设置锁定或解锁

### HTTP 请求

- POST `/v1/api/changeusdtstatus` 

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述 
| -------- | ------- | ------ | ----- | -----------
| uid      | true   | long | NA    | uid
| status   | true   | int    | NA    |  0-locked 1-working
| timestamp | true   | long    | NA    | 时间戳
| sign      | true   | string    | NA    | sign

> Response:

```json
{  
  "code": 200
}
```

