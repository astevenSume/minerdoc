# 用户资产设计
available 可用资产
trade 交易冻结资产，出售时冻结
game 游戏冻结资产
transfer 转入中资产，已经买入或者转入但链上未确认资产
transfer_game 转入中资产但带入游戏中冻结

# 承兑商资产设计
available 可用资产
trade 交易冻结

## 资产变更
- OTC内部是实时划转
- 
- 链上转账由定时任务不断轮询处理

```mermaid
graph LR
subgraph 转账
    A(用户A.available)-.1000EUSD.->B(用户B.transfer)
   B--> C(用户B.available)
  end
subgraph 链上转账
    A1(用户A)-.1000EUSD.->B1(用户B)
    B1-->C1[确认转账成功]
    C1-->C
  end
```


# OTC 交易
- OTC购买 （用户购买、承兑商出售）
- OTC出售  (用户出售、承兑商购买)


# OTC购买
### 步骤
1. 承兑商开启收款服务（挂单）
2. 用户选择支付方式&下单 - 撮合交易
3. 用户标记付款（用户付款-线下操作）
4. 承兑商确认收款（承兑商-确认）
5. 链上转账
6. 转账确认
7. 订单实际完成
8. 用户取消订单
9. 15分钟自动取消订单
10. 申诉
11. 申诉-取消订单
12. 申诉-确认订单

### 简要主流程

```mermaid
graph TB
  S[承兑商 & 用户 准备步骤] --> A
  A[承兑商开启出售] --> B[用户下单]
  B-->C[用户付款]
  C-->D[承兑商确认付款]
  D-->E[订单结束]
  E-->F[链上转账]
```

### 详细流程图
```mermaid
graph TB
    start(承兑商开启收款服务) --> buy[用户下单购买]
    buy --> match[匹配承兑商]
    match --> lock[锁定承兑商代币 & 收款方式数据修改]
    lock --> waitUserPay{等待用户付款}
    waitUserPay --> userCancel[用户取消订单]
    userCancel --> unlock[解锁承兑商代币]
    unlock --> canceled[订单取消]
    waitUserPay --> userExpired[用户15分钟内无操作 超过付款时间]
    waitUserPay --> userConfirm[用户点击确认付款]
    userExpired --> systemCancel[系统强制取消订单]
    systemCancel --> unlock
    userConfirm --> waitExchangerConfirm{等待承兑商确认收款}
    waitExchangerConfirm --> appeal[用户或者承兑商申诉]
    waitExchangerConfirm -.取消这条线.-> exchangerExpired[承兑商15分钟内无操作 超过确认时间]
    waitExchangerConfirm --> exchangerConfirm[承兑商点击确认收款]
    exchangerExpired --> systemConfirm[系统确认收款]
    exchangerConfirm --> transfer[承兑商转币到用户账户]
    systemConfirm --> transfer
    transfer --> finished[订单完成]
    appeal --> adminProcess[客服介入]
    adminProcess --> unarrived[实际未收款]
    adminProcess --> arrived[实际已收款]
    arrived --> adminConfirm[客服确认收款]
    adminConfirm --> transfer
    unarrived --> adminCancel[客服取消订单]
    adminCancel --> unlock
    canceled --> stop(结束)
    finished --> stop
```


#### 承兑商开启收款服务
- 检查资格
- 检查资金
- 检查承兑商设置限额
- 检查收款方式，确定支持的方式&对应最小支付值、最大支付值
- 挂单状态判定（未完成）

#### 用户选择支付方式&下单
- 检查支付方式
- 检查用户下单状态（未完成）

#### 撮合交易
1. 通过 金额&支付方式 从数据库查询满足条件的承兑商
2. 随机排序承兑商信息
3. 轮询承兑商信息（4-7 如果失败，还原状态，从4重新开始）
4. 锁定承兑商的匹配
5. 匹配承兑商支付方式，锁定支付方式
6. 锁定承兑商资金
7. 修改承兑商挂单信息（扣除金额）
8. 生成订单
9. 通知承兑商

#### 用户付款
- 用户线下付款
- 用户标记付款

#### 承兑商确认收款
- 承兑商冻结资产扣除
- 用户资产添加
- 承兑商收款信息修改
- 链上转账请求记录

#### 取消订单
- 承兑商代币解冻 & 收款方式信息还原
- 订单状态改变
- 用户下单状态修改（未处理）



# OTC出售 (用户出售、承兑商购买)

### 步骤
1. 承兑商设置支付服务配置 & 开启服务
2. 用户选择收款方式&下单
3. 承兑商付款
4. 用户确认收款
5. 订单完成

### 流程
```mermaid
graph TB
    start[承兑商开启支付服务] --> buy[用户下单出售]
    buy --> lock[锁定用户代币]
    lock --> match[匹配承兑商]
    match --> waitExchangerPay{等待承兑商付款}
    waitExchangerPay --> exchangerCancel[承兑商取消订单]
    exchangerCancel --> unlock[解锁用户代币]
    unlock --> canceled[订单取消]
    waitExchangerPay --> exchangerExpired[承兑商15分钟内无操作 超过付款时间]
    waitExchangerPay --> exchangerConfirm[承兑商点击确认付款]
    exchangerExpired --> systemCancel[系统强制取消订单]
    systemCancel --> unlock
    exchangerConfirm --> waitUserConfirm{等待用户确认收款}
    waitUserConfirm --> appeal[承兑商或者用户申诉]
    waitUserConfirm -.XXX.-> userExpired[用户15分钟内无操作 超过确认时间]
    waitUserConfirm --> userConfirm[用户点击确认收款]
    userExpired --> systemConfirm[系统确认收款]
    userConfirm --> transfer[用户转币到承兑商账户]
    systemConfirm --> transfer
    transfer --> finished[订单完成]
    appeal --> adminProcess{客服介入}
    adminProcess --> unarrived[实际未收款]
    adminProcess --> arrived[实际已收款]
    arrived --> adminConfirm[客服确认收款]
    adminConfirm --> transfer
    unarrived --> adminCancel[客服取消订单]
    adminCancel --> unlock
    canceled --> stop(结束)
    finished --> stop
```

#### 承兑商开启支付服务
- 检查承兑商资格
- 检查承兑商支付设置

#### 用户选择收款方式&下单
- 检查用户状态
- 检查用户下单状态（未完成）
- 检查用户代币
- 检查收款方式
- 锁定代币
- 数据库搜索匹配的承兑商
- 承兑商随机排序
- 匹配承兑商
- 通知承兑商

#### 承兑商付款
- 承兑商线下付款
- 选择支付方式&标记付款
- 通知用户

#### 用户确认收款
- 用户代币划转 & 承兑商收代币
- 链上转账请求记录
- 标记订单完成

