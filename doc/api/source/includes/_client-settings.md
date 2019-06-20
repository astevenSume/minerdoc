# 客户端 - 配置

## 获取所有配置

此接口返回用户所有的配置。

### HTTP 请求

- GET `/v1/settings`

> Response:

```json
{
  "faceid_payment_enabled": true, // 面容支付
  "faceid_unlock_enabled": false, // 面容解锁
  "gesture_payment_enabled": false, // 手势支付
  "gesture_unlock_enabled": false, // 手势解锁
  "two_step_enabled": false, // 两步验证
  "push_fund_arrived": true, // 资金到账通知
  "push_new_order": true, // 新订单通知
}
```

### 响应数据

返回的主数据对象是所有配置请求数据。

## 获取某个配置

### HTTP 请求

- GET `/v1/settings/{setting}`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 描述         |
| -------- | ------- | ------ | ----------- |
| setting  | true    | string | 配置名称      | 

> Response:

```json
{  
  "data": {
    "faceid_unlock_enabled": false
  }
}
```

### 响应数据

返回的主数据对象是请求配置的值。

## 更新某个配置

### HTTP 请求

- PUT `/v1/settings/{setting}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述         |
| ------- | ------- | ------ | ------------ |
| setting | true    | string | 配置名称      | 
| value   | true    | mix    | 配置值        | 

> Response:

```json
{  
  "data": {
    "faceid_unlock_enabled": true
  }
}
```

### 响应数据

返回的主数据对象是请求配置的值。

## 删除某个配置

### HTTP 请求

- DELETE `/v1/settings/{setting}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述         |
| ------- | ------- | ------ | ------------ |
| setting | true    | string | 配置名称      | 

> Response:

```json
{  
  "data": {
    "setting": "unused_setting_name"
  }
}
```

### 响应数据

返回的主数据对象是请求配置的配置名。
