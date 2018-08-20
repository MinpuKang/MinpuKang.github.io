---
layout: post
title: 通信新人如何学信令？
date: 2018-08-20
categories: blog
tags: [通信, 信令]
description: 任何一次触发都会引发一系列的效应
---

<style>
img{
  display:block;
  margin:0
  auto;
}
</style>

<meta name="referrer" content="never">

最近想起了七年前的自己，也作为一个通信freshman，每天往返于学校和公司之间，以实习生的身份开始通信生活，毕业后入职，一干就是七年。

之前也没想过自己的职业生活是一个什么样子，想来这就是一个没有计划的体现，所谓职业规划在最开始的初期是根本没有什么意识的，即便是到现在意识也没有那么明显，得过且过。

但是在最初的日子里，那种初入职场学习的兴趣和激情，却是现在想要拥抱的，随着时间的流逝，激情退却，剩下只是为数不多的经验和什么都可以试一试的淡定了。

回归主题，今天想总结一下信令学习的一些感悟，可能会有一些偏颇之词，还望大家加以指点。

####1. 信令是什么

什么是信令呢？从字面上看，信就是一种信息，令就是一种命令，所以信令字面意思就是信息命令。

专业上的定义就是通信设备之间传送的控制消息，从而对相关设备产生影响而引发下一步的动作。

通俗的举个例子，比如妈妈叫吃饭的这个过程：
```
妈妈：浑小子！
自己：妈，干嘛呀？
妈妈：快回家吃饭！
自己：马上就回啦。
```
这个过程中妈妈和自己就类比了通信中的两个设备，“浑小子！”和“妈，干嘛呀？”是一对儿信令，“快回家吃饭！”和“马上就回啦。”又是一对儿信令，而由此信令所产生的结果就是你得速度回家吃饭，妈妈才不会生气。

在这个妈妈发起的信令中要求你要做的就是回家完成吃饭的动作。

划重点，信令是要成对出现的，发出的一条信令都需要一个响应。

假如你因为没听到或者置若罔闻没有回答，以妈妈的容忍度呼叫你三次，这个就是信令超时重传；此时妈妈已经没有了忍耐力，不继续叫你了，最终的结果就是没饭吃，这个时候信令没有能完成，妈妈就要做troubleshooting来看看你到底出什么问题了(怕不怕)。

####2. 信令中都要完成什么呢？

首先先聊一个三A的问题——AAA。

这三个A按照顺序分别是Authentication、Authorization和Accounting。

#####2.1 Authentication——“你是谁”

Authentication就是鉴权，什么是鉴权呢？就是要完成“你是谁”的过程。

继续妈妈叫吃饭的这个例子，首先你听到妈妈的声音“浑小子”瞬间验证了这个是自己亲妈的声音，从而完成了对妈妈的鉴权——这个是我妈；然你回答“妈，干啥呀”，妈妈听到这个声音立马判断出这是自己的亲儿子回答的，从而完成了妈妈对你的身份认证，而且是双向认证。

在这个过程中，如果你的好朋友“靓丫头”响应了你妈妈的召唤，你妈妈就会想“这是哪儿个妮儿？”，从而验证失败。

#####2.2 Authorization——“要干嘛”

第二个A就是Authorization——授权，授权又是什么鬼？这个就是要完成“要干啥”的过程。

继续妈妈叫吃饭(╮(￣▽￣"")╭)，妈妈和自己都认证亲妈亲儿子之后，你是不是得想知道妈妈叫你“干嘛呀？”，然后妈妈告诉你“快回家吃饭！”。

这就是Authorization——“要干嘛”的过程。

#####2.3 Accounting——“干了多少”

最后一个Accounting——核算又是什么玩意呢？这个其实就是要统计“干了多少”。

继续妈妈叫吃饭，因为妈妈的招呼，你不得不跟“靓丫头”约定一会儿再玩儿，然后迅速回家吃了十碗米饭，妈妈一看吃了十碗米饭锅底都没了，决定“明儿得多做一点儿了”，这个“看你吃了十碗米饭”就是一个Accouting的过程。

#####2.4 通信中的信令都干嘛了？

那么回到本节的问题——信令都要干嘛。

其实我们所学习到的信令就为了完成三A这件事儿：你是谁，你要干嘛，干了多少。

拿最基本的附着信令来说，如下图从**1.Attach Request**到**5b.ME Identity(IMEI) check**完毕的整个过程都是在问**你是谁**，包括了MME和HSS的针对用户sim的鉴权，以及MME和EIR对于手机防山寨的验证等等。
![1.附着信令][1]

之后的信令就是一个**你要干嘛**的过程，比如你想上网，那就通过**Update Location Request**和**Response(Answer)**来完成授权，并通过上网APN建立PDN来准备好你要干嘛，PDN建立好之后，你才可以去上网；其中PGW和PCRF交互的过程也包含了鉴权这件小事儿。

#####2.5 通信里的Accounting
那么问题来了，Accounting哪里去了？我们说Accounting就是一个“干了多少”这个问题。

继续那妈妈叫吃饭来说，你得回到家去吃饭了才开始统计吧？通信也一样，你说我想上网了，但是结果你告诉完了之后什么也不干，那就不涉及到“干了多少”这个问题了。

当你真的开始上网了，开始发微信刷微博了，这个时候就开始统计了。

所以Accounting是在做这件事(上网，或者打VoLTE)的时候才发生的，这个也是运营商的关键——Charging，也就是统计你的流量，从而匹配你所定的套餐来判断你是否可以继续上网。

比如你预定了20G的流量，结果通过统计，你已经用了19G了，这个时候运营商就会给你发短信了：“小哥，来个叠加包吧！”。

这些都是Accounting的内容。

####3.如何学习信令

所以在最开始学习信令的时候，要捋清**你是谁**和**你要干什么**这两个问题，然后抓住谁发起第一个消息，为什么发起这个消息，收到消息之后要干什么等问题，基本就可以事半功倍了。

比如还是这个附着信令，永远都是手机发起，网络不会管你要不要附着，网络只负责响应；那么为什么要起？因为要上网呀，所以开机打开数据开关就要发起附着了；MME收到Attach Request之后需要先完成你是谁的验证，等等等。

就聊这么多吧，不足之处还望指正。

最后放一张今天台风过后傍晚的照片，虽然台风确实造就了交通的瘫痪、财产的损失，但是在自然面前，毕竟我们是那么的渺小，只能忍了，然后重新继续，不过台风的洗礼，却让风景也更加的通透和清澈了。
![2.凌水湾晚霞][2]


------------
<p align="center">欢迎关注公众号：</p>
<img src="https://mmbiz.qpic.cn/mmbiz_jpg/QqiaFS6NT0eD1g2UjYu4VfCGHmbhgVqOAnNnJQfN7ZhRVUCopYOsfpPtIEB95VNEqu8trAxJXzGDg01ka6z6wzQ/0?wx_fmt=jpeg" width="30%" />

<p align="center">感觉内容不错，读后有收获？欢迎小额赞助：</p>
<img src="https://mmbiz.qpic.cn/mmbiz_jpg/QqiaFS6NT0eAzA577Ce49rCLiby9EtT195GRiaqKCT6QCQ5Weia9OZD72MJz4ABlqAy1gbHepk5hHM464hCiarQRI7w/0?wx_fmt=jpeg" width="30%" />

  [1]: https://mmbiz.qpic.cn/mmbiz_png/QqiaFS6NT0eDu6dhxd49JRRBjCcibUUSickoQzIda16ic3RcicbEB28S5awaUF2nlic9PiajGDOpZraPQBiaVTOFGfbcPQ/0?wx_fmt=png
  [2]: https://mmbiz.qpic.cn/mmbiz_jpg/QqiaFS6NT0eDu6dhxd49JRRBjCcibUUSickrRuib5LicnZXDSIByYG4DlIqtvvCViaNpLPCDjSFfAAiclDHniaj8FaGt6Q/0?wx_fmt=jpeg

