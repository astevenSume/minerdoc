# 服务端 - EOS

## 冻结EOS账户

### HTTP 请求

- POST `/v1/admin/eos/frozen`

```json
{
  "uid": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| uid         | true    | string |        | 用户ID

> Response:


### 响应数据
返回的错误码。


## 解冻EOS账户

### HTTP 请求

- POST `/v1/admin/orders/eos/unfrozen`

```json
{
  "uid": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ------ | -----------
| uid         | true    | string |        | 用户ID

> Response:


### 响应数据
返回的错误码。

