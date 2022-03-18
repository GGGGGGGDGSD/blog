## HTTP
1. http 常见状态码
2.  http常见字段
  字段的能做如下分类分类
    - 通过字段头部
      connect
      cache-control

    - 请求字段头部
      accept
      accept-language
      accept-encoding
      connection
      cache-control
      host
      user-Agent
      referer
      if-none-match
      if-modified-Since

    响应字段头部
    Access-Control-Allow-Origin
    Etag
    Last-modified
    Set-Cookie
    keep-alive(原来这个是一个独立的response字段, 我还以为只是connection的一个值，当然这个字段只有在connection: keep-alive开启才有效，这是一个很重要字段 可以设置持久连接的超时时间和最大请求数目，一般服务器都有默认值)

    实体字段头部
    Content-Length
    Content-Type
    Content-Language
    Content-Encoding
    ExPires
   
3.  http 不同版本区别
4. http与https区别
5. http 1与 http2区别
6. http缓存
7. http与https区别
https://www.zhihu.com/question/19577317
8. cookie理解与实际运用
9. websocket理解

2. HTTPS的加密传输原理 **NICE**

 - https://zhuanlan.zhihu.com/p/43789231

> 首先需要理解对称加密与非对称加密 
  以及对称加密为什么不安全(如何保证秘钥被安全传输到服务器)
  以及非对称加密如何通过两对秘钥解决问题  但是要多次加密传输 耗费资源 性能
  刚好用非对称加密传输对称加密需要的秘钥就可以解决了  但是还是有一个问题 传输的秘钥被中间人掉包依然有问题（问题回归到如何保证收到的公钥的网站自己的）
  这就需要数字证书 那数字证书怎么防止被篡改呢  这就需要数字签名

3. http2理解
   > http2核心的就是二进制分帧层  下面这些特征都是基于这个底层技术

  - http1.0
  > 一个tcp连接只能发送一个请求，请求成功才能发送下一个请求， 响应返回tcp断开
  
  - http1.1(开启keep-alive)
  > 一个tcp连接可以发送多个请求 但是同一时刻一个连接仍然只能发送一个请求，改变的只是连接时间，但是请求发送机制并没有改变，如果要并发请求只能开启一个新的tcp连接，但是一个域名下一般最多只能同时开启6个 tcp连接, 对头阻塞问题仍然没有被解决（我现在想确认这个表述是否有问题

  - http2
  > 帧 消息  数据流（三个核心概念
  1. 帧是最小的数据单元 包好最基本的消息 比如属于哪个数据流
  2. 一个消息对应真实的一个请求或者响应的一些列帧
  3. 已经建立的连接内的双向字节流， 可以承载一条或者多条消息
  他们之间关系
  4. 一个tcp连接内可以承载任意数量的双向字节流，所有通信都在一个tcp连接内完成
  5. 每个数据流都有唯一的标识符和可选的优先级信息用于承载双向消息
  6. 每条消息都是一条逻辑http消息
  7. 帧是最小通信单元  承载特定类型数据 比如http标头 消息负载 不同数据流的帧可以交互发送 然后再根据每个帧投的数据标识符重新组装

  二进制编码
  多路复用
  服务器端推送
  发送请求优先级
  请求头部压缩
  [HTTP/2 简介  google dev](https://developers.google.com/web/fundamentals/performance/http2?hl=zh-cn)
  [HTTP/2 相比 1.0 有哪些重大改进? 知乎](https://www.zhihu.com/question/34074946)

  http2缺点
  1. http2丢包会导致整个tcp连接都阻塞  http1 只会影响单个tcp连接 其他tcp连接仍然可以继续使用
  

4. tcp 和udp区别
- TCP 是面向连接的协议 。 UDP 是无连接的协议
- TCP需要建立连接， UDP不需要
	         UDP	               TCP
是否连接	无连接	面向连接
是否可靠	不可靠传输，不使用流量控制和拥塞控制	可靠传输，使用流量控制和拥塞控制
连接对象个数	支持一对一，一对多，多对一和多对多交互通信	只能是一对一通信
传输方式	面向报文	面向字节流
首部开销	首部开销小，仅8字节	首部最小20字节，最大60字节
适用场景	适用于实时应用（IP电话、视频会议、直播等）	适用于要求可靠传输的应用，例如文件传输

5. http缓存

第一次请求后会把响应数据和缓存规则存入缓存系统，第二次及以后的请求先进入缓存系统 根据缓存规则查看是否支持缓存 
https://juejin.cn/post/6844903801778864136

浏览器缓存
强缓存
expires 设置过期时间 缺点是服务时间可能和客服端时间不一致
cache-control 设置过期时间长度（http1.1) cache-control 优先级比expires高

cache-control
- no-store 不缓存
- no-cache 强制发送请求比对（协商缓存

弱缓存
last-modified/if-modified-since 
etag/if-none-match

四种缓存的优先级：cache-control > expires > etag > last-modified

为什么Etag 优先级比last-modified高
1. last-modified只能精确到秒级别
2. 一些文件只是更改了修改时间，但是没有任何内容的修改（比如打包 缓存策略等）
 想想 我们需要的是比较内容更改 更改时间只是一种侧面判断方式 真正需要判断的还是内容  所有Eag优先级更高
3. etag通常用散列值生成

3. cookie
  补充http无状态的缺点
