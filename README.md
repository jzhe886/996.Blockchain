# 996.Blockchain

[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu)   [![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)

## 目录

* [项目背景](#项目背景)
* [运行模式](#运行模式)  
    * [节点部署](#节点部署)  
    * [客户端使用](#客户端使用)  
* [Q&A](#qa)

**其他文档**
* [安装指引](doc/install.md)  
* [操作指引](doc/instructions.md)
* [协议与接口](doc/technical.md)

## 写在最前

这是一个代码型项目，为抗议996发声。它通过区块链的特性，加强加班取证的真实性，未来希望通过客户端的能力进一步加强取证的规范性、便捷性，甚至基于哈希共识扩展出其它应用场景。

目前希望项目得到更多的部署，另一方面希望找到有精力和兴趣的小伙伴参与手机端的开发。有任何想法都欢迎发邮件沟通，我会一直关注着邮件，对项目也是长期维护。

## 项目背景

当部分996的劳动者尝试对自身合法权益进行维权时，可能会面临存证难、举证难的问题。996.Blockchain 尝试通过区块链技术进行协助，因为它天生具备防篡改、可追溯的特征，在司法存证领域早已有所影响：

> 2018年9月7日最高人民法院日前发布的《关于互联网法院审理案件若干问题的规定》（以下简称《规定》）开始施行，《规定》提出，通过电子签名、可信时间戳、哈希值校验、区块链等证据收集、固定和防篡改的技术手段或者通过电子取证存证平台认证，能够证明其真实性的，互联网法院应当确认。

**希望健康高效的工作方式有朝一日可替代浮于表面的996工作制**。

## 运行模式

996.Blockchain 以公链的形式运行，属于志愿型项目，**不发行代币,参与者无法从该系统中获得经济收益。** 但它有个基于链上数据的得分统计，每挖出一个块得一分，让参与者知道自己对系统的贡献度。  

### 节点部署
    
* anti996程序，它是区块链网络的一个全节点，和网络中的其他节点相互连接
* 每个节点会同步保存所有区块数据，之间通过POW进行共识
* 任意节点都可以接收证据摘要，并广播给全局，定时产出的区块会把它们打包入块

节点安装[参考](doc/install.md)  
节点启动、配置[参考](doc/instructions.md#示例一-运行anti996接入主网)  

### 客户端使用

client程序，**用户可通过它将带有自己签名的哈希上传至区块链，并在需要的时候取得相关信息。**

如何理解:  
1. 链上只存储照片、视频、录音等的**摘要**，原始数据需要用户自己妥善保管  
2. 996.Blockchain**能**帮助你：
    * 证明你是摘要（原始数据）的所有者
    * 证明摘要（原始数据）产生于某一个时间点之前，即它所在的块的时间点之前
3. 996.Blockchain**不能**帮助你：
    * 保存管理证据
    * 直接取证

注意客户端并非轻节点或类似概念的东西，只是对全节点提供的HTTP接口的调用封装，客户端使用[参考](doc/instructions.md#示例二-上传证据到网络中)

## Q&A

**0 为什么没有代币？**

这是一个志愿型项目，不参杂经济利益能让项目意图更纯粹，也更易合法合规。

----

**1 直接用手机拍得照片去举证和把证据哈希传到链上再举证有什么区别？**   

从目前阶段来说并没有太大的区别，但还是欢迎使用。

理想中的取证系统应该包含：
1. 友好的客户端，协助规范取证，为证据归档、分类，连接后端提供检索、验证能力
2. 可靠的云服务存储
3. 公正透明的区块链，提供电子签名、可信时间、哈希校验能力

996.Blockchain 项目当前主要具备第3点能力，迈出了第一步。虽然产品的体验还不完善，但其大体功能和逻辑是完整和闭环的，使用者可以通过命令行完成管理密钥、生成、上传、查询证据摘要、查询区块数据等操作。

----

**2 996.Blockchain与现有的存证区块链系统有什么区别？**

当前基于区块链的存证系统多以联盟链甚至私链形式存在，存证数据托管于某几个或某个第三方的机构，而996.Blockchain是公链，没有准入机制，数据管理在网络上的每个节点。存在形式的不同，会导致一系列的区别，在此不赘述。**除此以外最大的区别是其诞生背景和含义。**

----

**3 996.Blockchain除了存证还能做什么？**

996.Blockchain 的本质是Hash的共识，基于此可以有不同的应用场景猜想，比如：

* 防伪查询  
    1. 商家对售出商品的摘要H和随机值R进行签名上链(HR = hash(H+R))
    2. 商家在官网公布自己的公钥，并将相关二维码贴在商品刮层下
    3. 消费者购买商品刮开涂层，扫描后得到H、R、公钥，并触发商家对H'(H' = f(H)，是一个公认的转换函数)签名上链
    4. 消费者首次在链上查询验证HR通过，且查不到H'，一段时间后验证H’的产生时间和签名合法性通过；则说明这是正品且是一手货
* 版权保护
    1. 创作者在创作过程中对每个阶段的成果保存下来并将其摘要上链
    2. 当发现被抄袭时，可以举证相关内容已于某一时间点前由本人创作

**以上仅是猜想**

----

**4 怎么参与项目？**

0. 分享给身边的朋友，或许ta刚好对此感兴趣
1. 参考[安装文档](doc/install.md)和[操作指引](doc/instructions.md)进行安装操作，为网络增添一份力量和稳固
2. 参考[技术文档](doc/technical.md)的接口和协议，按需实现想要的功能，如架设反代提供区块查询、证据上链的网站，开发友好的客户端等
3. 对问题代码进行修复
4. 对项目进行法律相关的指导说明
5. 发邮件至 996blockchain@gmail.com 提出更多想法

