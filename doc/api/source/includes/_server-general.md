# 服务端 - 通用功能
## 冻结用户账户

### HTTP 请求

- POST `/v1/admin/general/frozenuser`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| uid     |  true  | string    | NA    | 用户UID
| reason     | false   | string    | NA    |  冻结原因

> Response:

```json
{"code":200}
```

## 解冻用户账户

### HTTP 请求

- POST `/v1/admin/general/unfrozenuser`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| uid        |  true  | string    | NA    | 用户UID
| reason     | false   | string    | NA    |  冻结原因

> Response:

```json
{"code":200}
```

## 禁止用户登录

### HTTP 请求

- POST `/v1/admin/general/lockuser`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| uid     |  true  | string    | NA    | 用户UID
| reason     | false   | string    | NA    |  冻结原因

> Response:

```json
{"code":200}
```

## 解禁用户登录

### HTTP 请求

- POST `/v1/admin/general/unlockuser`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | ------- | ------ | ----- | -----------
| uid     |  true  | string    | NA    | 用户UID
| reason     | false   | string    | NA    |  冻结原因

> Response:

```json
{"code":200}
```
