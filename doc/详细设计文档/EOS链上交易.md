****EOS链上交易，主要用EOS-Go SDK 并在此基础上封装****

其中可分为利用Keosd节点签名，和KeyBag签名 两种方式

Keosd节点允许本地访问，或内网访问，签名前 需要在keosd导入私钥

KeyBag签名，需要在初始化时 导入私钥

```go
a.keyBag = &eos.KeyBag{}
err = a.keyBag.ImportPrivateKey(EosConfig.ActivePrivateKey)
```
**1.创建新账户**
```mermaid
graph TB;  
    创建账户-->生成创建账户的bin字符串;
    创建账户-->生成购买内存的bin字符串;
    创建账户-->生成抵押资源的bin字符串;
    生成创建账户的bin字符串-->用active权限签名;
    生成购买内存的bin字符串-->用active权限签名;
    生成抵押资源的bin字符串-->用active权限签名;
    用active权限签名-->广播交易数据;    

```
**2.转账**
```mermaid
graph TB; 
    交易转账-->生成转账的bin字符串
    生成转账的bin字符串-->用active权限签名
    用active权限签名-->广播交易

```
**购买资源，回收资源等流程类似，都是先序列化josn数据，然后签名，最后广播;**   

**获取节点数据，获取余额等流程相对简单，直接请求节点就可以了;**
