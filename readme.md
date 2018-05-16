# V2ray

「 说是`代理`, 其实用`通道`来, 更合适 」

这里是 explain 单元, 但只解释, 概念

[![explain](http://llever.com/explain.svg)](https://github.com/chinanf-boy/Source-Explain)
    
Explanation

> "version": "1.0.0"

[github source](https://github.com/v2ray/v2ray-core)

~~[english](./README.en.md)~~

---

一直以来, 通过科学上网让我对世界更多了份认识, 但手机似乎要收费,

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

它需要开了一边 比如 `socks5` 协议 -/- `http` 协议 等等

``` json
// socks 进
  "inbound" : {
    "listen" : "0.0.0.0", //✅ 和 127.0.0.1❌  是否正确只是区别在于 是否给局域网的其他设备访问 
    "port" : 1080, // 端口在设置外面
    "protocol" : "socks", // 协议
    "settings" : { // 协议设置
      "auth" : "noauth",
      "udp" : true,
      "ip" : "127.0.0.1"
    }
  },
```

  请求 -> socks5 ->  `）= 入口-socks === v2ray ======（）堵住的`


#### 一出

开了另一边 比如 `shadowsocks` 协议 -/- `vmess` 协议{v2ray安全🔐与复杂性}

``` json
// shadowsocks 出
  "outbound": {
    "protocol": "shadowsocks", // 协议
    "settings":{ // 协议设置
      
      // ⚠️ 以下命令 是安全信息, 请保管好自己的信息

      "servers": [ // 注意是 server s  是 Array 类型
      	{
          // 身份🆔
          "address": "192.168.11.103", // Shadowsocks 的服务器地址
          "email": "love@v2ray.com", // 用户名标示
          "method": "chacha20-ietf", // Shadowsocks 的加密方式
          "password": "asdfasdfasdf", // Shadowsocks 的密码
          "ota": true,
          "port": 5000
        }
    ]
}
}
```

`) == 入口-socks ==== V2ray ====== 出口-shadowsocks ==> 有🆔身份的shadowsocks => 找servers == (`

#### 通道说明

>比作 socks === 🐱 , shadoawsocks === 🐶

> 我们手机-电脑浏览器的`请求`通过 代理软件 就可以 装得像猫

#### 1. 请求 -> socks5 -> 🐱 ==>  

> 用户端 -> 匹配通道入口协议

#### 2. `) == 入口-socks ==== V2ray ====== 出口-shadowsocks ==> 🐶 => 找servers == (`

> 进入通道后

好了, 我们的 🐱 , 进来通道后发现, 出口限制🚫说: 只有 🐶 能通过?

这个时候, `V2ray-{化妆师}出场了`, ta/居然能把 __🐱变🐶__ , _我的天啊_

#### 3. 🐱 变 🐶 , 化妆就是这样化腐朽为神奇

#### 4. 找 servers

> 好了, `V2ray`, 会领着你到下一个 `舞台-通道`


---

### 第一通道

就这样, 🐱变成🐶, 进入下一个舞台

### 第一通道-通道图

`) == 入口-socks ==== V2ray ====== 出口-shadowsocks ==> 🐶 => 找servers == (

<details>

<summary>完整config.json</summary>

``` json
// 
{
// socks 进
  "inbound" : {
    "listen" : "0.0.0.0", //✅ 和 127.0.0.1❌  是否正确只是区别在于 是否给局域网的其他设备访问 
    "port" : 1080, // 端口在设置外面
    "protocol" : "socks", // 协议
    "settings" : { // 协议设置
      "auth" : "noauth",
      "udp" : true,
      "ip" : "127.0.0.1"
    }
  },
  // shadowsocks 出
  "outbound": {
    "protocol": "shadowsocks", // 协议
    "settings":{ // 协议设置
      
      // ⚠️ 以下命令 是安全信息, 请保管好自己的信息

      "servers": [ // 注意是 server s  是 Array 类型
      	{
          "address": "192.168.11.103", // Shadowsocks 的服务器地址
          "email": "love@v2ray.com", // 用户名标示
          "method": "chacha20-ietf", // Shadowsocks 的加密方式
          "password": "asdfasdfasdf", // Shadowsocks 的密码
          "ota": true,
          "port": 5000
        }
    ]
  }
  }
}
```

</details>

---

### 第二通道

我来布置第二个通道吧

上文说到 , __🐱 进入 [第一通道](#第一通道) 后被 `V2ray-化妆师` 变 🐶, 进入了限制 只许🐶出的__, [第二通道](#第二通道)

那么一上来, 我们的狗就迎来了挑战

#### 第二通道-入口

> V2ray === 化妆师

``` json
// 第二通道-入口
  "inbound": {
    "port": 5000, // 对口, 不然路都找不到
    "protocol": "shadowsocks", // 要是🐶
    "settings": {
      // 身份身份
      "email": "love@v2ray.com",
      "method": "chacha20-ietf",
      "ota": true,
      "password": "asdfasdfasdf"
    }
  },
```
1. 只需 🐶, 噢不, 只许有身份的🐶, 进入

身份？[==》》那是我们在上一个通道的事情啦](#一出)

``` json
// 上一通道-出口
  "outbound": {
    "protocol": "shadowsocks", // 协议
    "settings":{ // 协议设置
      "servers": [ 
      	{
          // 👇👇👇👇👇👇👇👇👇
          "address": "192.168.11.103", // Shadowsocks 的服务器地址
          "email": "love@v2ray.com", // 用户名标示
          "method": "chacha20-ietf", // Shadowsocks 的加密方式
          "password": "asdfasdfasdf", // Shadowsocks 的密码
          "ota": true,
          "port": 5000
        }
    ]
}
}
```

我们的 `化妆师`, 除了 把 `__🐱变成🐶__`, 还给了我们身份, 太感动了, 一只有身份的🐶

好了我们交上 `爪`上的身份信息, 进入到了 第二通道里面

2. `) == 入口-身份-shadowsocks ==== V2ray ===()`

#### 第二通道-出口

``` json
// 第二通道-出口
  "outbound": {
      "protocol" : "freedom",
      "tag" : "direct",
      "settings" : {
      }
  }
```

这个时候, 我们其实有很多选择, 可以是象征 `自由的freedom` `严谨的vmess`, `再变🐱的socks`

而`freedom`，顾名思义 自由请求, 是最终解

> 其他的协议, 自然需要另一个通道的入口配置

> ⚠️ 自由之后, 还要回来的, 我们的用户要`接受请求的数据`, 也就是说 `🐶需要重新变成🐱,在第一通道`？

那么`freedom`出口, 你以为 化妆师 不用工作, 🐶 要变回 请求, 才能被外界认识

#### 第二通道-通道图

`) == 入口-身份-🐶 ==== V2ray ==== 出口-freedom ==> 🐶->请求 => * == (`



因为两次 V2ray 的 作用, 所以我称之为 通道, 只要一进一出互通的, 就能一直下去

---

## 总结

理解`通道`, 比理解 `S/C` 可能更贴切一点

> v2ray-mac-iphone 名字 随便写的, 可能是我用 mac客户端d代理我的iphone 的灵感

有用的东西

1. https://github.com/wangyi2005/v2ray-heroku

> `heroku` 上的 v2ray 通道

> 入口-`vmess`， 出口-`freedom`

2. 你需要一个客户端

https://www.v2ray.com/ui_client/

3. 既然 1 中 `入-vmess, 出-freedom`

但是, 我们手机上的 `免费代理{非中华地区}` 只能 `socks/shadowsocks/http` - 

那么我们, 再在 heroku 上 一个 入口 `socks` - 出口 - `vmess`

接入 1 中, 经过两通道, 手机自然能连

> `socks/shadowsocks` 不知道会不会被`heroku`禁用

> 这也是为什么 入口用 `严谨的vmess` , 化得太多数人都不认识, 自然通行

### 通道 通道 通道

- https://www.v2ray.com

- https://github.com/v2ray

---


