# 客户端 - 基础信息

## 获取通用信息

此接口返回客户端通用信息

```shell
curl "https://api.wallet.io/v1/common"
```

### HTTP 请求

- GET `/v1/common`

### 请求参数
此接口不接受任何参数。

> Responds:

```json
  "data": {
    "platform_name": "钱多多",
    "buy_fee_rate": "0.002",
    "sell_fee_rate": "0.002",
    "contact_wechat": "winpay",
    "contact_telegram": "https:/t.me/winpay",
    "service_wechat": "http://weixin.qq.com/r/RHU6NQjE1japhxlWnyBg",
    "invite_wechat": "http://weixin.qq.com/r/RHU6NQjE1japhxlWnyBg",
  }
```

### 响应数据
| 字段名称          | 是否必须 | 类型   | 描述          | 取值范围 |
| --------------- | ------- | ------ | ------------ | ------- |
| platform_name   | true    | string | 钱多多        |         |
| buy_fee_rate    | true    | string | 购买手续费率   |         |
| sell_fee_rate   | true    | string | 出售手续费率   |         |
| contact_wechat  | true    | string | 联系微信号     |         |
| contact_telegram| true    | string | 联系telegram号|         |
| service_wechat  | true    | string | 客服微信号     |         |
| invite_wechat   | true    | string | 邀请客服微信号  |         |

## 获取参考价格

此接口返回所有USDT参考价格

```shell
curl "https://api.wallet.io/v1/common/price"
```

### HTTP 请求

- GET `/v1/common/price`

### 请求参数
此接口不接受任何参数。

> Responds:

```json
  "data": {
    "currency": "USDT",
    "price": "6.74",
    "precision": 2
  }
```

### 响应数据

| 字段名称    | 类型    | 描述
| ---------- | -------| -----------
| price      | string | 对人民币参考价格
| precision  | int    | 报价的精度（小数点后位数）

## 获取当前系统时间

此接口返回当前的系统时间，时间是调整为北京时间的时间戳，单位毫秒。

```shell
curl "https://api.wallet.io/v1/common/timestamp"
```

### HTTP 请求

- GET `/v1/common/timestamp`

### 请求参数
此接口不接受任何参数。

> Response:

```json
  "data": 1494900087029
```

### 响应数据

返回的“data”对象是一个整数表示返回的调整为北京时间的时间戳，单位毫秒。

## 获取版本

此接口返回最新app版本

### HTTP 请求

- GET `/v1/common/{system}/version`

### 请求参数

| 参数名称  | 是否必须 | 类型   | 默认值 | 描述    | 取值范围      |
| -------- | ------- | ------ | ----- | ------| ------------ |
| system   | true    | int8   | NA    | 平台   | 1:安卓平台, 2:ios平台 |

- System 平台定义

| 状态       | 定义    |
| ----------| ------  |  
| 1         | 安卓平台
| 2         | ios平台   

> Responds:

```json
  "data": {
    "version": "1.0.0",
    "changelog": "更新日志",
    "download": "https://baidu.com/app.apk",
    "system": 1,
    "ctime": 1494901162595,
    "utime": 1494901162595
  }
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述        | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| version      | true    | string | 版本号      |         |
| changlog     | true    | string | 版本更新日志 |         |
| download     | true    | string | 版本下载链接 |         |
| system       | true    | int8   | 平台类型    | 1:安卓平台, 2:ios平台    |
| ctime        | false   | long   | 版本创建时间 |         |
| utime        | false   | long   | 版本更新时间 |         |



## 获取域名

此接口返回当前域名列表

### HTTP 请求

- GET `/v1/common/endpoint`

### 请求参数
此接口不接受任何参数。 

> Responds:

```json
  "data": {
    "list": [
      {
        "id": 1,
        "endpoint`": "https://www.qdd.com",
        "ctime": 1494901162595,
        "utime": 1494901162595,
      },
      {
        "id": 2,
        "endpoint`": "https://www.qdd.com",
        "ctime": 1494901162595,
        "utime": 1494901162595,
      }
    ]
  }
```

### 响应数据

| 字段名称   | 是否必须 | 类型   | 描述       | 取值范围|
| --------- | -------   | ------ | ---------- | ------- |
| id        | true      | int    | 域名id     |         |
| endpoint  | true      | string | 域名       |         |
| ctime     | false     | long   | 创建时间   |         |
| utime     | false     | long   | 更新时间   |         |

