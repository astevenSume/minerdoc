# 服务端 - 管理员相关

## 管理员登录
### HTTP 请求

- POST `/v1/admin/login`

```json
{
  "email": "zhangsan@gmail.com",
  "password": "123456"
  "verify_code":"123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| ----------- | ------- | ------ | ----- | -----------
| email       | true    | string | NA    | 邮箱
| password    | true    | string | NA    | 密码
| verify_code | true    | string | NA    | google验证码

> Response:

```json
{  
  "data": {
    "id": 123456789,
    "name": "张三",
    "email": "zhangsan@gmail.com",
    "roles": [{
      "id": 1,
      "name": "超级管理员"
    }],
    "permissions": [
      "LIST_USER",
      "EDIT_USER",
      "ADD_USER",
      "DELETE_USER",
      "LIST_ORDER",
      "EDIT_ORDER",
    ],
    "status": 1,
    "ctime": 1494901162595,
    "ltime": 1494901162595,
	"is_bind": false,
    "secret_id": "KSfLwIUSfYlcIxHVlKjmYixKRqBKYuQX",
    "qr_code":"data:image/png;base64,..."
  }
}
```

### 响应数据

| 字段名称      | 是否必须 | 类型   | 描述       | 取值范围 |
| ------------ | ------- | ------ | ---------- | ------- |
| id           | true    | int   | 管理员 ID     |         |
| name         | true    | string | 管理员姓名     |         |
| email        | true    | string | 管理员邮箱     |         |
| status       | true    | int    | 管理员状态     | 1, 2, 3 |
| roles        | true    | array  | 管理员角色     |         |
| permissions  | true    | array  | 管理员权限表    |         |
| ctime        | false   | long   | 管理员创建时间  |         |
| utime        | false   | long   | 管理员更新时间  |         |
| ltime        | false   | long   | 管理员登陆时间  |         |
| dtime        | false   | long   | 管理员删除时间  |         |
| is_bind      | false   | bool   | 是否已绑定谷歌验证|         |
| secret_id    | false   | string | 谷歌验证秘钥    |         |
| qr_code      | false   | string | 谷歌验证二维码  |         |

- 管理员状态定义：
| 状态       | 描述  |
| --------- | ----- |
| 1         | 激活   |
| 2         | 禁用   |
| 3         | 删除   |


## 管理员登出
### HTTP 请求

- POST `/v1/admin/logout`

> Response:

```json
{  
  "data": {
    "id": 123456789
  }
}
```

### 响应数据

返回的主数据对象是一个对应管理员id。


## 修改密码
### HTTP 请求

- POST `/v1/admin/password`

```json
{
  "oldpwd": "123",
  "newpwd": "123456"
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述 
| -----------  | ------- | ------ | ----- | -----------
| oldpwd       | true    | string | NA    | 旧密码
| newpwd       | true    | string | NA    | 新密码

### 响应数据

返回的主数据对象是一个对应管理员id。



## 更新token
### HTTP 请求

- POST `/v1/admin/relogin`

### 请求参数


### 响应数据

返回错误码。
```