# The-Adventures-of-AI
Record AI learning experiences, mainly used to document pitfalls encountered, solutions, and some new knowledge.


2026.3.10
初次接触opencla

安装了git、node.js(版本要大于22)，安装了Linux

在Linux环境上安装了openclaw

从17号来回顾这天的安装来说，有几个事情想说

1、导航界面选择Model的时候，按照b站的视频，选择了千问模型授权，但是因为当时并不知道需要购买模型，所以在安装完成后，聊了两句，就被限制了

2、于是，查看视频后购买了火山方舟计划，首次购买仅需￥9.9， 但是当时不知道大模型的购买后，是由一定时间内的token限制，所以在五小时以内的token被消耗完以后，我以为是“充的钱被用完了”，所以又买了一个月度会员（￥40），导致现在我有两个月的方舟计划会员


2026.3.11
安装skill
解决openclaw没有记忆的问题



2026.3.12
研究Github
解决openclaw没有记忆的问题


2026.3.13
给mac安装openclaw


2026.3.14
解决openclaw没有记忆的问题


2026.3.15
解决openclaw没有记忆的问题


2026.3.16
这个“历险记”是17号创建的，所以16号的事情已经不太记得了

今天主要是在解决openclaw在飞书上不能创建与编辑飞书文档的问题

网上看到飞书推出了官方接入openclaw的插件，于是安装了插件，但是还是没有解决问题

由于一直想依赖openclaw本身来解决问题，但飞书上的openclaw感觉上真的会比网页端显得要蠢很多

所以，想到换更聪明的大模型

于是在当天晚上，充值了openai的会员

但是这天并没有顺利接入openclaw


2026.3.17
昨晚发现openai官网购买的plus会员不能直接接入open claw

于是今天致力于探究原因和解决方案

结果就是，官网购买的会员或是APIKey，都几乎不可能在国内环境下接入openclaw，原因是openai对国内的区域限制。

这里先说一下我的环境：
我有两个环境，一个是win11环境，一个是mac环境

win11环境上安装了Linux子系统，openclaw安装在Linux子系统上，访问国外网站的时候使用Xlink代理软件

在openai接入openclaw失败后，寻找原因的过程中，发现代理其实只监听win11系统的端口进行转发，也就是在我开着代理的情况下，实际上openclaw所在的环境实际上并没有被代理，仍然是国内网络。

于是我大费一番周折将Linux环境的网络镜像到win11的端口，进行代理，成功后，再次尝试将openai接入openclaw，但还是失败了

这次最后失败在了认证网页

后来我想着，我直接在mac环境上开代理把openai接入openclaw，结果是一样的。

于是我明白了，无论openclaw所在的环境是否被正确代理，openai都无法在国内接入openclaw

这源于openai对于国内的区域限制
但是，我还是不确定这是不是一个无法解决的问题，或许是我没找到解决方案

于是，我着眼于APIKey的方式接入，因为在调查过程中一种说法是用APIKey的方式更容易接入

（顺便在这里着重提一句：大模型的会员和API是完全不同的两种计算方式，开通会员不代表APIKey有使用权限，通常意义上APIKey是单独按消耗的Token计费的，而会员通常是一个月或一年内的使用权限，两者完全不同）

于是又在b站找到了一种中转站（https://jiekou.ai/）的方式去购买了openai的APIKey的额度：花费￥34

感觉上这种中转站应该就是立足于解决openai对于国内的区域限制问题的

我通过中转站购买的APIKey接入了openclaw，显示是可以work的，但是问题仍然不少

第一是配置方式中有一个字段与通常配置model的字段不同
      "Jiekou": {
        "baseUrl": "https://api.jiekou.ai/openai/v1",
        "apiKey": "sk_GQwCV5l7tRzEFP782uWYnCSEGkqnXpvesL3D-jbBKQc",
        "api": "openai-responses",
        "models": [
          {
            "id": "gpt-5.4",
            "name": "gpt-5.4 (Custom Provider)",
            "reasoning": false,
            "input": [
              "text"
            ],
            "cost": {
              "input": 0,
              "output": 0,
              "cacheRead": 0,
              "cacheWrite": 0
            },
            "contextWindow": 16000,
            "maxTokens": 16384
          }
        ]
      }
就是这个Jiekou.api,卖家让我在枚举中试哪一个可用...

第二个问题就是，随着上下文的增加，貌似达到了一个token总量的上线，报错为：
The AI service is temporarily overloaded. Please try again in a moment.

于是，这个APIKey不能用了...

所以，我不得已又转向了稳定运行的火山方舟计划，没在探究这个事情了



后面我在解决另一个问题：openclaw生成的图片带有“ai生成”的水印

同时我又想使用nanobanana来生图，所以又找到了一个类似“中转站” 的网站

这个网站用的提供APIKey，类似火山方舟计划，只不过这个API下的模型全是Image模型，

但是尴尬的是，我事先并不知道这个网站也分为会员和“APIKey”，也是因为没有想起openai的二分情况

所以我上去就买了个会员，花费￥49，

结局就是生成的APIKey根本没有额度，于是就又充值了APIKey，花费￥69

这个网站附带一个skill， 原理就是让open claw去他的网站获取图片生成的image大模型，去生图

——————————————————————————————————————————————————————————————————————————————————————

截止到目前，三个比较大的问题

1、openai等国外的大模型怎么接入openclaw
答案就是今天得到的一个大概的答案，国外的大模型基本无法通过官方的方式接入openclaw

2、openclaw在飞书中不能操作文档

3、openclaw没有记忆的问题
其实这个问题今天有些意外，就是今天打开她的时候，给他的任务他竟然带上了之前写在他的md文件中的记忆，看上去像是有了一些记忆，所以这个问题只能等明天在观察



