# V2ray

「 说是`代理`, 其实用`通道`来, 更合适 」

[![explain](http://llever.com/explain.svg)](https://github.com/chinanf-boy/Source-Explain)
    
Explanation

> "version": "1.0.0"

[github source](https://github.com/v2ray/v2ray-core)

~~[english](./README.en.md)~~

---

一直以来, 通过科学上网让我对世界更多了份认识, 但手机似乎要收费

v2ray, 也正如此诞生的, 谢谢🙏

---

### 我是 iphone, 所以我需要一个代理软件, 只要支持 `socks5` 的就行

---


为什么我要明确 `通道 `这一说法 ,

长久以来, 我使用 `shadowsoks` 的应用让我惯性的理解 需要 _服务器和客户端_

它的协议, 能 `S <=> C` 沟通起来

> 那么 v2ray

为什么说, 他更像一个通道了, 因为 两个字

### 一进一出

#### 一进 

它就像开了一边 比如 `socks5` 协议 - `http` 协议 等等

  数据 -> socks5 这边   ）==========（）


#### 一出


开了另一边 比如 `shadowsocks` 协议 - `vmess` 协议{v2ray安全🔐与复杂性}

  socks5 -> 🐱 ==>  ) ======V2ray====== ( vmess ==> 🐶

>猫变成狗啦

猫从哪里来

我们手机-电脑浏览器的`请求`通过 代理软件 就可以 装得像猫

---

⚠️ 🐱 -变成-> 🐶 之后, 还要回来的


---

https://github.com/wangyi2005/v2ray-heroku

