---
title: API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:
  - rules
  - errors
  - client-admin
  - client-common
  - client-sms
  - client-users
  - client-exchanger
  - client-usdt
  - client-eos
  - client-orders
  - client-buy
  - client-sell
  - client-payment-methods
  - client-payment-password
  - client-apps
  - client-banners
  - client-announcements
  - client-agent
  - client-notifications
  - client-settings
  - client-game
  - server-admin
  - server-admins
  - server-users
  - server-roles
  - server-permissions
  - server-topagent
  - server-agents
  - server-agentwhitelists
  - server-exchangersverify
  - server-exchangers
  - server-operations
  - server-userloginlogs
  - server-versions
  - server-smscodes
  - server-smstemplates
  - server-eosaddresses
  - server-eoswallets
  - server-eosrecords
  - server-eos
  - server-platform
  - server-usdt
  - server-prices
  - server-appealservice
  - server-appeals
  - server-orders
  - server-messages
  - server-commissionrates
  - server-commissionstat
  - server-notifications
  - server-banners
  - server-announcements
  - server-apps
  - server-apptypes
  - server-appchannels
  - server-appwhite
  - server-endpoint
  - server-config
  - server-config-warning
  - server-serverstop
  - server-otcstat
  - server-general
  - server-task
  - server-monthdividendconf
---
# 简介

REST（Representational State Transfer）是一种轻量级的 Web Service 架构风格，可以翻译成“表述性状态转移”，实现和操作明显比 SOAP 和 XML-RPC 更为简洁，可以完全通过 HTTP 协议实现，还可以利用缓存 Cache 来提高响应速度，性能、效率和易用性上都优于 SOAP 协议。

REST 架构遵循了 CRUD 原则，CRUD 原则对于资源只需要四种行为：Create（创建）、Read（读取）、Update（更新）和Delete（删除）就可以完成对其操作和处理。这四个操作是一种原子操作，对资源的操作包括获取、创建、修改和删除资源的操作正好对应 HTTP 协议提供的 GET、POST、PUT 和 DELETE 方法，因此 REST 把 HTTP 对一个 URL 资源的操作限制在 POST、GET、PUT 和 DELETE 这四个之内。这种针对网络应用的设计和开发方式，可以降低开发的复杂性，提高系统的可伸缩性。

更多 REST API 背景知识可以参考 [RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)。

以及 [REST-API-Design-Guide](https://github.com/NationalBankBelgium/REST-API-Design-Guide/wiki)

# 接入说明

## 接入 URLs

**REST API**

**`https://api.wallet.io`**

## 请求格式

所有的API请求都以GET或者POST形式发出。对于GET请求，所有的参数都在路径参数里；对于POST请求，所有参数则以JSON格式发送在请求主体（body）里。

## 返回格式

所有的接口返回都是JSON格式。在JSON最上层有几个表示请求状态和属性的字段："code"业务错误码, 实际的接口返回内容在"data"字段里.

### 返回内容格式

> 返回内容将会是以下格式:

```json
{
  "code": "200",
  "data": // per API response data in nested JSON object
}
```

参数名称| 数据类型 | 描述
--------- | --------- | -----------
code      | int       | 业务错误码
data      | object    | 接口返回数据主体, 如果是**数组**，则对应最外层是 **\[\]** 的数组, 如果是**对象**，则对应最外层是 **\{\}** 的对象

#### 成功返回示例

````json
{
  "code": 0,
  "data": {
    "id": "132fb6ae-456b-4654-b4e0-d681ac05cea1",
    "name": "张三",
    "password": "123456",
    "phone": "13008888888",
    "ctime": 1494901162595,
    "utime": 1494901162595
    ......
  }
}
````

#### 错误返回示例

````json
{
    "code": 2,
}
````

### 数据格式标准规范
本章节主要为标准规范的细节分以下两个方面：

- 数字
- ID
- 时间

#### 数字
为了保持跨平台时精度的完整性，十进制数字作为字符串返回。建议您在发起请求时也将数字转换为字符串以避免截断和精度错误。

整数（如交易编号和顺序）不加引号。

#### ID

除非另有说明，大多数标识符是UUID。当提出一个需要UUID的请求时，以下两个形式（有和没有破折号）都被接受。

132fb6ae-456b-4654-b4e0-d681ac05cea1 或者 132fb6ae456b4654b4e0d681ac05cea1

#### 时间

所有的时间都会是13位时间戳：

> 1494901162595

## 参数 

许多 API 采用可选参数，对于 GET 请求任何参数都可以在 URL 中传递：

```shell
curl -i "https://api.wallet.io/v1/users?user=1"
```

对于 POST 、 PATCH 、 PUT 和 DELETE 请求， URL 中没有包含的参数应该为请求体的 JSON，其中，请求头应该设置 `Content-Type` 为 `application/json` ：

```shell
curl -i -d '{"login": ":username", "password": ":password"}' https://api.wallet.io/v1/tokens
```

### 常见请求参数

比如在数据过多, 需要对数据进行分页请求的时候, 我们应该统一 API 请求参数. 常见的有这些.

参数 | 说明
--------------------- | -----------------------------------
page=2&limit=100   | 指定第几页，以及每页的记录数
sortby=name&order=asc | 指定返回结果按照哪个属性排序，以及排序顺序

### 常见返回参数

请求列表时，返回的分页参数信息

```json
{
  "code": 0,
  "data": {
    "list": [...],
    "meta": {
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    },
    ...
  }
}
```

## 授权 

一旦用户使用授权凭证，下一步应该使用令牌来请求用户信息，以便可以将其显示为“已登陆”。

令牌存储方式： 使用HTTP Cookie的方式存储令牌，Cookie生成规则参照Json Web Tokens规则。 

多终端使用限制：服务端对令牌做了多终端使用限制机制，例如一个用户A在终端1登录，生成有效令牌token1，在令牌有效期内，如果用户在终端2登录，则服务端生成token2，并且将token1置为无效。

客户端可基于有效的令牌实现自动登录机制。


## otc系统反重放攻击策略

客户端和otc系统通信，遵循以下签名规则:

1 app端请求的 header 中增加以下2个参数：

参数 | 说明
--- | ---
timestamp  | 时间戳
sign       | md5hash


POST : md5(md5(url + post_string +time)+salt)  
GET： md5(md5(url +time)+salt)     //url里包含querystring参数

服务端校验参数无误后检查是否存在上次请求的时间戳，存在且比当前请求时间戳大的则返回错误

例:

put 请求: http://localhost/v1/user/info?=

body 参数:
```json
{"name":"test"}
```

header :
```
timestamp : 1557222562000
sign : 6f52b7d6c475939bc85d0ae951490d3a
```
salt: ZyGYFWIWO1BWYl9lpBKaNtKmXxFRrHwu5PgJD9V332AEWweZY1QdrRyTbjcAjmaq

md5(md5("/v1/user/info?={"name":"test"}1557222562000")+"ZyGYFWIWO1BWYl9lpBKaNtKmXxFRrHwu5PgJD9V332AEWweZY1QdrRyTbjcAjmaq")


---
## otc系统通信数据加密

otc系统返回数据结构中的 data 将经过 aes-gcm 算法进行加密:

```json
{                     
  "code":200,
  "data":"密文字符串"
}
```

开发环境的 key 为: `TrW24fxMP6QL7sB1GHcrlKROAUC3DSc=`

目前开发环境 `请求头 Headers` 中需要增加 `enable-encrypt` , 值为任意非空字符串即可开启返回数据加密功能 , 功能上线前将会去除该限制
