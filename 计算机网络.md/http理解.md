## HTTP
1. http与https区别
https://www.zhihu.com/question/19577317

2. HTTPS的加密传输原理 **NICE**

 - https://zhuanlan.zhihu.com/p/43789231

> 首先需要理解对称加密与非对称加密 
  以及对称加密为什么不安全(如何保证秘钥被安全传输到服务器)
  以及非对称加密如何通过两对秘钥解决问题  但是要多次加密传输 耗费资源 性能
  刚好用非对称加密传输对称加密需要的秘钥就可以解决了  但是还是有一个问题 传输的秘钥被中间人掉包依然有问题（问题回归到如何保证收到的公钥的网站自己的）
  这就需要数字证书 那数字证书怎么防止被篡改呢  这就需要数字签名

3. http2理解

  二进制编码 多路复用 服务器端推送 发送请求优先级 请求头部压缩
  https://www.zhihu.com/question/34074946
  https://developers.google.com/web/fundamentals/performance/http2?hl=zh-cn

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

弱缓存
last-modified/if-modified-since 
etag/if-none-match

四种缓存的优先级：cache-control > expires > etag > last-modified