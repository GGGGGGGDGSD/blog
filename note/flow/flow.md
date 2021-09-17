## fcl
four phases to the Flow JS-SDK
Build -> Resolve -> Send -> Decode
fcl接口调用说明 https://github.com/onflow/fcl-js/blob/master/packages/sdk/readme.md

## 合约Cadence
https://docs.onflow.org/cadence/
https://play.onflow.org/local?type=account&id=LOCAL-account-0



1. 创建测试网账户
  https://docs.onflow.org/dapp-deployment/testnet-deployment/

- flow keys generate
  下面就是我自己的测试账号

   Store private key safely and don't share with anyone!
Private Key      356cd3bdfa766e7f7754112cec0d109cf9c2bd45f50d328a93cac22719822ae0

Public Key       de9014345e4d4fc5d8a89fed892ea7259c635ffb3bd854a22826d57a8cb6a2b0799f18420166a35cb2bd4d3dd78090641165f06b257d490b0b1efcdbc30b47ea

Adress
0x78a93ff6d4ca79c3

0x7accf14c4fc449b2

测试网
0x8f0ffa54ba7521e7


1944210109@qq.com
0x9b3e51ddb87f1bf7

syi1944210109@gmail.com


    // "dev-wallet": "fcl-wallet PK=67ff105cfed60b0db9f95960851b9b96a73a03e972a09195a0efa709a828958b SERVICE_ADDR=f8d6e0586b0a20c7"



## 基础
1. 账户
 - 公共账户 代表帐户的公共可用部分 定地址的PublicAccount的对象
 - 授权账户   可以完全访问其存储，公钥和代码

2. Resources
   
3. 能力
   就是提供了访问某种功能的权利的接口

4. event
   event有点像node事件  event 关键词定义 emit触发  但是最主要的区别在于函数不是一等公民  不能作为值传递（不能赋值给变量 不能作为函数参数传递)

5. 交易的四个phases
transaction {
    prepare(signer1: AuthAccount) {
        // Access signing accounts for this transaction.
        //
        // Avoid logic that does not need access to signing accounts.
        //
        // Signing accounts can't be accesed anywhere else in the transaction.
    }

    pre {
        // Define conditions that must be true
        // for this transaction to execute.
    }

    execute {
        // The main transaction logic goes here, but you can access
        // any public information or resources published by any account.
    }

    post {
        // Define the expected state of things
        // as they should be after the transaction executed.
        //
        // Also used to provide information about what changes
        // this transaction will make to accounts in this transaction.
    }
}