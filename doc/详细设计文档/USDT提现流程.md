# usdt提现流程

## 1 usdt提现申请单

#### 1.1 发起usdt提现申请单

```mermaid
sequenceDiagram
    participant client_user
    participant otc
    client_user->>otc:发起提现申请
    otc->>otc:检查用户钱包地址
    otc->>otc:检查余额是否充足
    Note right of otc: 检查条件不满足直接返回。
    otc->>client_user:拒绝提交申请单
    otc->>otc:生成临时转账申请单
    Note right of otc: 生成失败拒绝提交申请单。
    otc->>client_user:拒绝提交申请单
    otc->>otc:冻结申请金额
    Note right of otc: 冻结失败，写入审计。
    otc->>client_user:拒绝提交申请单
    otc->>otc:更新转账申请单状态为已提交
    Note right of otc: 更新状态失败，写入审计。
    otc->>client_user:拒绝提交申请单（资产已冻结，需要审计解冻）
    Note right of otc: 更新状态成功
    otc->>client_user:申请成功
```
<center>提现申请时序图</center>

## 2 usdt提现审批

#### 2.1 审批通过（链上转帐）

```mermaid
sequenceDiagram
    participant admin_user
    participant otc_admin
    participant otc
    admin_user->>otc_admin: 审批提现申请单（通过）
    otc_admin->>otc:请求转发
    otc->>otc:检查用户被冻结金额是否大于等于提现金额
    otc->>otc:检验用户钱包金额，足够生成签名信息
    otc->>otc:用户钱包金额不足，系统热钱包资金是否足够提现，生成签名信息
    otc->>otc:修改申请单为转账中
    Note right of otc: 失败直接返回。
    otc->>otc_admin:审批失败
    otc_admin->>admin_user:审批失败
    otc->>otc:推送转账到主链上
    Note right of otc: 推送失败
    otc->>otc:回滚申请单为已提交
    Note right of otc: 回滚失败，写入审计
    otc->>otc_admin:审批失败
    otc_admin->>admin_user:审批失败
    otc->>otc:申请单状态更新为已发出
    Note right of otc: 更新失败，写入审计
    otc->>otc:清除被冻结的金额
    Note right of otc: 清除失败，写入审计
    otc->>otc_admin:审批成功
    otc_admin->>admin_user:审批成功
   	otc->>otc:用户钱包有金额，加入待归集序列
```
<center>usdt审批通过时序图</center>

#### 2.2 审批通过（系统内转账）

```mermaid
sequenceDiagram
    participant admin_user
    participant otc_admin
    participant otc
    admin_user->>otc_admin: 审批提现申请单（通过）
    otc_admin->>otc:请求转发
    otc->>otc:检查用户被冻结金额是否大于等于提现金额
    otc->>otc:修改申请单为转账中
    Note right of otc: 失败直接返回。
    otc->>otc_admin:审批失败
    otc_admin->>admin_user:审批失败
    otc->>otc:平台内转账,修改双方金额
    Note right of otc: 修改失败，写入审计。
    otc->>otc_admin:审批失败
    otc_admin->>admin_user:审批失败
    otc->>otc:修改申请单为平台已转出
    otc->>otc:添加转出记录
    otc->>otc:添加转入记录
    Note right of otc: 添加失败，写入审计。
    otc->>otc_admin:审批成功
    otc_admin->>admin_user:审批成功
   	otc->>otc:用户钱包有金额，加入待归集序列
```
<center>usdt审批通过时序图</center>

#### 2.3 审批拒绝

```mermaid
sequenceDiagram
    participant admin_user
    participant otc_admin
    participant otc
    admin_user->>otc_admin: 审批提现申请单（拒绝）
    otc_admin->>otc:请求转发
    otc->>otc:更新转账申请单状态为审批中
    Note right of otc: 更新失败直接返回。
    otc->>otc_admin:审批失败
    otc_admin->>admin_user:审批失败
    otc->>otc:解冻资金
	Note right of otc: 解冻失败，写入审计。
	otc->>otc:更新申请单为已拒绝
	Note right of otc: 更新失败，写入审计。
	otc->>otc_admin:审批失败
    otc_admin->>admin_user:审批失败
	Note right of otc: 判断无异常。
	otc->>otc_admin:审批成功
    otc_admin->>admin_user:审批成功
```
<center>usdt审批拒绝时序图</center>


## 附：

#### status 抵押赎回状态定义：

| 类型        | 描述     |
| ----------- | ------- |
| 1           | 转入（充值） |
| 2           | 转出（提现） |
| 3           | 抵押    |
| 4           | 赎回    |

#### status 抵押赎回状态定义：

| 状态       | 描述    |
| ---------- | ------- |
| 1          | 抵押中 |
| 2          | 已抵押   |
| 3          | 赎回中   |
| 4          | 已赎回   |

#### status 充值状态定义：

| 状态       | 描述    |
| ---------- | ------- |
| 100        | 状态未知 |
| 101        | 待确认   |
| 102        | 确认中   |
| 103        | 已确认   |
| 104        | 已完成   |

#### status 提现状态定义：

| 状态            | 描述        |
| --------------- | ---------- |
| 201             | 状态未知    |
| 202             | 已提交      |
| 203             | 审核中      |
| 204             | 已取消      |
| 205             | 审批通过    |
| 206             | 审批拒绝    |
| 207             | 处理中      |
| 208             | 已汇出      |
| 209             | 区块已确认   |
| 210             | 区块交易错误 |
| 211             | 已撤销      |



