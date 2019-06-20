# USDT

## 1 资产查询

```mermaid
sequenceDiagram
    participant client
    participant otc
    participant db_otc
    
    %%校验access_token
    client->>otc:查询
    otc->>+otc:校验access_token
    opt 校验失败
    otc->>-client:返回用户未登录错误
    end
    
    %% todo 修改为异步创建+实时分配
    otc->>+otc:查询usdt_account数据（usdt_account）
    otc->>+db_otc:查询
    db_otc->>-otc:返回结果
    alt 数据库错误
    otc->>client:返回DB错误
    
    %% 不存在，则尝试创建
    else 不存在
    otc->>otc:尝试创建
    otc->>+db_otc:创建usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 创建失败
    otc->>client:返回创建账号失败错误
    end
    
    %% 尝试绑定pk
    otc->>otc:尝试绑定pk
    otc->>+db_otc:获取一条未绑定pk(usdt_prikey)
    db_otc->>-otc:返回结果
    opt 获取失败
    otc->>client:返回错误
    end
    otc->>+db_otc:绑定pk(usdt_prikey)
    db_otc->>-otc:返回结果
    opt 绑定失败
    otc->>client:返回错误
    end
    otc->>+db_otc:查询pk数据(udst_prikey)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end

    end
    otc->>-client:返回结果

```
<center>账户查询时序图</center>

## 2 账户余额

```mermaid
sequenceDiagram
    participant client
    participant otc
    participant db_otc
    
    %%校验access_token
    client->>otc:查询
    otc->>+otc:校验access_token
    opt 校验失败
    otc->>-client:返回用户未登录错误
    end
    
    %% 查询usdt_account数据
    otc->>+otc:查询usdt_account数据
    otc->>+db_otc:查询usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end
    
    %% 计算金额
    otc->>otc:计算余额字段，包括available、frozen、mortgage
    otc->>-client:返回结果
    
```

<center>账户余额查询时序图</center>

## 3 充值

```mermaid
sequenceDiagram
    participant client
    participant otc
    participant redis
    participant db_otc
    participant omni_info
    
    %% 系统外充值
    client->>omni_info:系统外充值
    otc->>otc:定时检测usdt_account
    
    %% 系统内死循环检测
    loop 死循环 
        otc->>+redis:获取同步锁（redis）"usdt_sync_onchain_tx"
            redis->>-otc:返回结果
        alt 获取锁失败
            %% 什么都不做 
        else 获取到锁
            otc->>+db_otc:查询账户总数（usdt_account）
            db_otc->>-otc:返回结果
            loop 100个/页
                otc->>+db_otc:查询当页账户（usdt_account）
                db_otc->>-otc:返回结果
                loop usdt_account
                    otc->>+db_otc:查询地址信息（usdt_pk_relation）
                    db_otc->>-otc:返回结果                 
                    opt !force
                        %% 校验sync频度
                        otc->>+db_otc:查询上次同步时间戳（usdt_onchain_data）
                        db_otc->>-otc:返回结果
                        opt 操作过频
                              otc->>otc:终止同步
                        end
                    end
                    %% 同步每页onchain数据
                    loop 每页onchain数据
                        otc->>+omni_info:同步当前页onchain数据
                        omni_info->>-otc:返回结果
                        otc->>+db_otc:保存onchain数据
                        db_otc->>-otc:返回结果
                    end
                    %% 如果有新的lastTx，则保存
                    opt newLastestTx
                        otc->>+db_otc:保存lastestTx
                        db_otc->>-otc:返回结果
                        otc->>+db_otc:保存lastSyncTimestamp
                        db_otc->>-otc:返回结果                            
                    end
                    %% 对比获取充值差额
                    otc->>+db_otc:查询本地transaction数据（usdt_transaction）
                    db_otc->>-otc:返回结果
                    otc->>+db_otc:查询链上transaction数据（usdt_onchain_transaction）
                    db_otc->>-otc:返回结果
                    opt 差额小于0
                        otc->>otc:返回错误
                    end
                    otc->>otc:获取差量tx数据
                    otc->>+db_otc:增加资产变更日志（usdt_wealth_log）
                    db_otc->>-otc:返回结果
                    otc->>+db_otc:增加差量tx数据（usdt_transaction）
                    db_otc->>-otc:返回结果
                    opt 增加失败
                        otc->>db_otc:更新资产变更日志状态（usdt_wealth_log）     
                    end
                    otc->>db_otc:更新资产变更日志状态（usdt_wealth_log）
                    otc->>+db_otc:更新用户可用资产（usdt_account）
                    db_otc->>-otc:返回结果
                    opt 更新失败
                        otc->>db_otc:更新资产变更日志状态（usdt_wealth_log）     
                    end
                    otc->>db_otc:更新资产变更日志状态（usdt_wealth_log）
                    
                    %% 休眠10秒钟
                    otc->>otc:休眠10秒钟（避免访问omni_info过于频繁导致被禁）
                end
            end
        end
    end
```
<center>账户充值时序图</center>

## 4 抵押

```mermaid
sequenceDiagram
    participant client
    participant otc
    participant db_otc
    participant redis
    
    %%校验access_token
    client->>otc:查询
    otc->>+otc:校验access_token
    opt 校验失败
    otc->>-client:返回用户未登录错误
    end
        
    %% 加分布式锁，todo 修改为数据库锁
    otc->>+redis:对usdt_account加分布式锁
    redis->>-otc:返回结果
    opt 加锁失败
    otc->>client:返回分布式加锁错误
    end
    
    %% 创建订单数据
    otc->>+db_otc:增加订单数据（usdt_wealth_log）
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end    
    
    %% 查询usdt_account数据
    otc->>+db_otc:查询usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end
    
    %% 判断余额是否足够抵押
    otc->>otc:校验余额是否足够抵押
    opt 余额不足
    otc->>client:返回错误
    end
    
    %% 更新账户数据
    otc->>+db_otc:更新账户数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end
    
    %% 发放eusd
    otc->>otc:发放eusd
    opt 发放失败
       otc->>+db_otc:回滚(usdt_account)
       db_otc->>-otc:返回结果
       opt 回滚失败
           otc->>db_otc:更新订单数据（usdt_wealth_log）
       end
    end
    
    %% 更新订单数据
    otc->>db_otc:更新订单数据（usdt_wealth_log）
```
<center>账户抵押时序图</center>

## 5 赎回

```mermaid
sequenceDiagram
    participant client
    participant otc
    participant db_otc
    participant redis
    
    %%校验access_token
    client->>otc:查询
    otc->>+otc:校验access_token
    opt 校验失败
    otc->>-client:返回用户未登录错误
    end
    
    %% 创建订单数据
    otc->>+db_otc:增加订单数据（usdt_wealth_log）
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end   

    %% 加分布式锁，todo 修改为数据库锁
    otc->>+redis:对usdt_account加分布式锁
    redis->>-otc:返回结果
    opt 加锁失败
    otc->>client:返回分布式加锁错误
    end
        
    %% 查询usdt_account数据
    otc->>+db_otc:查询usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end
    
    %% 判断金额是否足够赎回
    otc->>otc:校验金额是否足够赎回
    opt 余额不足
    otc->>client:返回错误
    end
    
    %% 更新账户数据
    otc->>+db_otc:更新账户数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 更新失败
    otc->>client:返回错误
    end
    
    %% 释放eusd
    otc->>otc:释放eusd
    opt 释放失败
        otc->>db_otc:记录订单数据(usdt_wealth_log)
        otc->>client:返回错误
    end
    
    %% 更新账户
    otc->>+db_otc:更新账户数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 更新失败
         otc->>db_otc:记录订单数据(usdt_wealth_log)
         otc->>client:返回错误
    end
    
    otc->>db_otc:记录订单数据(usdt_wealth_log)
    otc->>client:返回结果
```
<center>账户赎回时序图</center>

## 6 提现

```mermaid
  graph TD;
    Initial-->|Frozen成功|Submitted;
    Initial-->|Frozen失败|Failure;
    Submitted-->|Cancel|Canceling;
    Canceling-->|Unfrozen成功|Canceled;
    Canceling-->|Unfrozen失败|Failure;
    Submitted-->|Reject|Rejecting;
    Rejecting-->|Unfrozen成功|Rejected;
    Rejecting-->|Unfrozen失败|Failure;
    Submitted-->|Approve|Approved;
    Approved-->|ClearFrozen失败|Failure;
    Approved-->|查找私钥失败|Failure;
    Approved-->|离线签名失败|Failure;
    Approved-->|pushSignedTx失败|Failure;
    Approved-->|pushSignedTx失败|Failure;
    Approved-->|余额不足|Transfered;
    Transfered-->|onchainTxConfirme|Confirmed;
    
```
<center>转账状态图</center>

### 6.1 提现申请

```mermaid
sequenceDiagram
    participant client
    participant otc
    participant db_otc
    participant redis
    
    client->>otc:提现
    
    %%校验access_token
    otc->>+otc:校验access_token
    opt 校验失败
    otc->>-client:返回用户未登录错误
    end
    
    %%校验输入参数
    otc->>+otc:校验参数
    opt method不是address
    otc->>client:返回参数错误
    end
    opt address为空
    otc->>-client:返回参数错误
    end
    
    %%进行二次认证
    otc->>otc:二次认证
    otc->>+db_otc:查询user_pay_pass数据(user_pay_pass)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>client:返回错误
    end
    opt 密码不可用
    otc->>client:返回错误
    end
    otc->>+redis:查询密码锁定时间
    redis->>-otc:返回
    opt 密码被锁定
    otc->>client:返回错误
    end
    opt 请求中token为空
    otc->>client:返回错误
    end
    otc->>+redis:查询支付密码token
    redis->>-otc:返回
    opt token校验失败
    otc->>client:返回错误
    end
    otc->>redis:删除支付密码token

    %% 校验转账条件
    otc->>+otc:校验转账条件
    
    otc->>+db_otc:查询usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    
    opt 查询失败
    otc->>client:返回错误
    end
    
    opt 余额不足
    otc->>client:返回余额不足错误
    end
    
    otc->>+db_otc:查询pk数据
    db_otc->>-otc:返回结果
    opt pk数据不存在
    otc->>client:返回错误
    end
    
    %% 新增转账订单数据
    otc->>+db_otc:新增转账订单数据(usdt_wealth_log)
    db_otc->>-otc:返回结果
    opt 新增失败
    otc->>client:返回交易提交失败
    end
    
    %% 冻结转账金额
    otc->>+db_otc:冻结转账金额（修改available和frozen字段）(usdt_account)
    db_otc->>-otc:返回结果
    opt 冻结失败
    otc->>client:返回冻结失败
    end
    
    %% 更新订单状态为已提交
    otc->>+db_otc:更新转账订单状态为已提交(usdt_wealth_log)
    db_otc->>-otc:返回结果
    
    otc->>-client:返回转账结果
```
<center>提现申请时序图</center>

### 6.2 拒绝提现

```mermaid
sequenceDiagram
    participant otc_admin
    participant otc
    participant db_otc
    participant redis
    
    otc_admin->>+otc:取消订单
    
    %%校验签名
    otc->>+otc:校验签名
    opt 校验失败
    otc->>-otc_admin:返回参数错误
    end
    
    %% 获取id参数
    otc->>+otc:获取id参数
    opt 获取失败
    otc->>-otc_admin:返回参数错误
    end
 
    %% 获取订单信息
    otc->>+db_otc:查询订单数据(usdt_wealth_log)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end
 
    %% 加分布式锁，todo 修改为数据库锁
    otc->>+redis:对usdt_account加分布式锁
    redis->>-otc:返回结果
    opt 加锁失败
    otc->>otc_admin:返回分布式加锁错误
    end

    opt 订单类型非提现
    otc->>otc_admin:返回错误
    end

    opt 订单状态非已提交
    otc->>otc_admin:返回拒绝取消
    end
    
    %% 更新订单状态为取消
    otc->>+db_otc:更新订单状态为取消(usdt_wealth_log)
    db_otc->>-otc:返回结果
    opt 更新失败
    otc->>otc_admin:返回错误
    end
    
    %% 解冻资产
    otc->>+db_otc:解冻转账金额（修改available和frozen字段）(usdt_account)
    db_otc->>-otc:返回结果
    opt 更新失败
    otc->>otc_admin:返回错误
    end
    
    %% 组装返回订单信息
    otc->>+db_otc:查询订单数据(usdt_wealth_log)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end    

    otc->>-otc_admin:返回结果
    
    
```

### 6.3 批准申请单

```mermaid
sequenceDiagram
    participant otc_admin
    participant otc
    participant db_otc
    participant redis
    participant sighTx_nodejs
    participant omni_info
    
    otc_admin->>+otc:批准订单
    
    %%校验签名
    otc->>+otc:校验签名
    opt 校验失败
    otc->>-otc_admin:返回参数错误
    end
    
    %% 获取id参数
    otc->>+otc:获取id参数
    opt 获取失败
    otc->>-otc_admin:返回参数错误
    end
 
    %% 获取订单信息
    otc->>+db_otc:查询订单数据(usdt_wealth_log)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end
    
    %% 加分布式锁，todo 修改为数据库锁
    otc->>+redis:对usdt_account加分布式锁
    redis->>-otc:返回结果
    opt 加锁失败
    otc->>otc_admin:返回分布式加锁错误
    end

    opt 订单类型非提现
    otc->>otc_admin:返回错误
    end

    opt 订单状态非已提交
    otc->>otc_admin:返回拒绝取消
    end
    
    %% 从用户账户中转账
    otc->>+db_otc:查询用户usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end

    %% 校验资金是否足够
    otc->>+otc:校验资金是否足够
    opt 资金余额不足
    otc->>otc_admin:返回错误
    end
    
    %% 查数据询发送者私钥
    otc->>+db_otc:查询发送者私钥数据(usdt_prikey)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end
        
    %% 查询发送者utxo信息
    otc->>+omni_info:查询发送者utxo
    omni_info->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end
    
    %% 查询fee账户私钥数据
    otc->>+db_otc:查询fee账户私钥数据(usdt_prikey)
    db_otc->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end

    %% 查询fee账户utxo信息
    otc->>+omni_info:查询发送者utxo
    omni_info->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end

    %% 离线签名
    otc->>+sighTx_nodejs:离线签名
    sighTx_nodejs->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end
    
    %% 根据transaction字节大小计算fee
    otc->>+otc:计算fee值
    opt fee>max fee
    otc->>-otc:fee设置为max fee
    end
    
    %% 离线签名
    otc->>+sighTx_nodejs:离线签名
    sighTx_nodejs->>-otc:返回结果
    opt 查询失败
    otc->>otc_admin:返回错误
    end
    
    %% 更新订单状态为转账中
    otc->>db_otc:更新转账订单状态为转账中(usdt_wealth_log)
    
    %% transaction 广播到主网
    otc->>+omni_info:tx广播到主网
    omni_info->>-otc:返回结果
    opt 返回失败
    otc->>otc_admin:返回错误
    end
    opt 返回结果解码失败
    otc->>db_otc:更新转账订单状态为已提交(usdt_wealth_log)
    otc->>otc_admin:返回错误
    end
    opt 返回结果状态不正确
    otc->>db_otc:更新转账订单状态为已提交(usdt_wealth_log)
    otc->>otc_admin:返回错误
    end
    opt 返回结果非success
    otc->>db_otc:更新转账订单状态为已提交(usdt_wealth_log)
    otc->>otc_admin:返回错误
    end

    %% 记录订单详情数据
    otc->>+db_otc:记录订单详情数据(usdt_wealth_log)
    db_otc->>-otc:返回结果

    %% 更新冻结金额
    otc->>+db_otc:更新冻结金额(usdt_account)
    db_otc->>-otc:返回结果
        
```

## 7 查询

## 8 提现记录查询

## 9 抵押赎回记录查询

## 10 归集

| 目的 | 描述 | 备注 |
| ---- | ---- | ---- |
|   安全性   |   在用户钱包密钥丢失的情况下，最小化资产损失   |      |
| 操作性 | 对用户资产的统一调配管理 | |
| 可用性 | 平台内的账户转账，直接走数值修改，不走链上操作，节约转账手续费成本，同时提高效率 | |

```mermaid
sequenceDiagram
    participant usdtsvr
    participant db_otc
    participant db_usdt
    participant omni_info
    %% 读取所有账户数据
    usdtsvr->>+db_otc:查询所有账户（usdt_account）
    db_otc->>-usdtsvr:返回所有账户总数
    loop 分页
        usdtsvr->>+db_otc:查询本页账户数据（usdt_account）
        db_otc->>-usdtsvr:返回本页账户数据
        loop 每个账户
        end
    end
```

## 11 密钥管理

```mermaid
sequenceDiagram
    participant otc
    participant usdtsvr
    participant db_otc
    participant db_usdt
    otc->>otc:创建usdt_account
    otc->>+db_otc:增加usdt_account数据(usdt_account)
    db_otc->>-otc:返回结果
    otc->>+db_otc:增加usdt_pk_relation数据(usdt_pk_relation)
    db_otc->>-otc:返回结果
    usdtsvr->>+db_otc:读取未分配pk的usdt账户数据(usdt_pk_relation)
    db_otc->>-usdtsvr:返回结果
    loop 未分配prikey的账户
        usdtsvr->>+db_usdt:生成prikey数据
        db_usdt->>-usdtsvr:返回结果
        usdtsvr->>+db_usdt:绑定prikey
        db_usdt->>-usdtsvr:返回结果
    end
```
