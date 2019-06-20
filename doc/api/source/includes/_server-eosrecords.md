# 服务端 - EOS Record 记录数据
## 获取所有记录

### HTTP 请求

- GET `/v1/admin/eosrecords`

### 请求参数

| 参数名称    | 是否必须 | 类型   | 默认值 | 描述 
| ---------- | --------| --- -- | ----- | -----------
| page       | false   | int    | NA    | 当前显示分页号
| per_page   | false   | int    | 10    | 每页显示条数

> Response:

```json
{  
  "data": [
    {
      "id": "28290050-b655-4709-b004-dd1be04974e8",
      "type": 1,
      "rid": "adfd1231-b655-4709-b004-dd1be04974e8",
      "uid": "123456",
      "uid2": "234567",
      "address": "eosaddress1",
      "address2": "eosaddress2",
      "amount": "0.05",
      "memo": "hello there",
      "txid": "2f2419ed0be5bd7408aa3d7f6e8800cdc481023f31673edc54b03a924040c2bf",
      "block_num": "45725844",
      "ctime": 1494901162595,
      "utime": 1494901162595,
      "status": "submitted",
      }
    ],
    "meta": {
      "page": 1, // 当前页码
      "limit": 10,// 每页数据条数
      "total": 100, // 总个数
    }
  }
}
```

### 响应数据

| 字段名称        | 是否必须 | 类型   | 描述       | 取值范围 |
| -------------- | ------- | ------ | ---------- | ------- |
| id             | true    | long   | 记录 ID     |         |
| rid            | true    | long   | 关联记录ID  | 跟 orders, transfers, settlements 表关联 |
| type           | true    | long   | 类型        | 见下表  |
| uid            | true    | long   | 用户ID     |          |
| uid2           | true    | long   | 对方用户ID  |          |
| address        | true    | long   | 用户区地址  |          |
| address2       | true    | long   | 对方用户地址 |         |
| amount         | true    | long   | 金额        |         |
| memo           | true    | long   | 备注        |         |
| status         | true    | string | 状态        | 见下表   |
| txid           | true    | string | 交易 ID     |        |
| block_num      | true    | string | 区块号      |        |
| ctime          | true    | long   | 发起时间    |        |
| utime          | true    | long   | 最后更新时间 |        |

##### 类型定义:

| 类型        | 描述     |
| ----------- | ------- |
| transfer-in | 转入    |
| transfer-out| 转出    |
| buy         | 购买    |
| sell        | 支出    |
| game        | 游戏结算 |

#### 充值状态定义：

| 状态       | 描述    |
| ---------- | ------- |
| unknown    | 状态未知 |
| pending    | 待确认   |
| confirming | 确认中   |
| confirmed  | 已确认   |
| finished   | 已完成   |

#### 提现状态定义：

| 状态            | 描述        |
| --------------- | ---------- |
| submitted       | 已提交      |
| reexamine       | 审核中      |
| canceled        | 已取消      |
| approved        | 审批通过    |
| rejected        | 审批拒绝    |
| transfering     | 处理中      |
| transferred     | 已汇出      |
| confirmed       | 区块已确认   |
| failure         | 区块交易错误 |
| revoke          | 已撤销      |

## 获取记录

### HTTP 请求

- GET `/v1/admin/eosrecords/{id}`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 默认值 | 描述 
| ------- | ------- | ------ | ----- | -----------
| id      | true    | int    | NA    | 记录 id

> Response:

```json
{  
  "data": {
    "id": "28290050-b655-4709-b004-dd1be04974e8",
    "type": "transfer-in",
    "uid": "123456",
    "uid2": "234567",
    "address": "eosaddress1",
    "address2": "eosaddress2",
    "amount": "0.05",
    "fee": "0.01",
    "memo": "hello there",
    "txid": "2f2419ed0be5bd7408aa3d7f6e8800cdc481023f31673edc54b03a924040c2bf",
    "block_num": "45725844",
    "ctime": 1494901162595,
    "utime": 1494901162595,
    "status": "submitted",
  }
}
```

### 响应数据
返回的主数据对象是一个对应财务记录对象。
