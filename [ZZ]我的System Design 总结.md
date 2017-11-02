[原文链接](https://www.mitbbs.com/article_t/JobHunting/32777529.html)
发信人: flamingos (flamingos), 信区: JobHunting
标  题: 我的System Design总结
发信站: BBS 未名空间站 (Mon Sep  8 02:49:55 2014, 美东)

== Update ==
好久没回来逛贴了 承蒙大家厚爱 这篇文章已经有接近8万的访问量了
最近我准备把内容深入的写一下 以一个系列文章的方式发出来 供大家参考
由于和包子的团队都是很多年的老朋友 就发在他们的平台 如果有兴趣的话可以关注微
信号: baozitraining

我的面试也结束了 因为知道FLAG这类公司都会问到System Design的问题 所以这次面
试着重准备了一下 在这里分享给大家 如果有不对或者需要补充的地方 大家可以留言

这里说的System Design和OO Design不同 System Design在FLAG以及很多大公司中主要
是design scalable distributed systems 这里只讨论如何准备这种题目

== 入门 ==
对于0基础的同学们 下面的资料可以按顺序开始看
1. http://www.hiredintech.com/app#system-design
这是一个专门准备面试的网站 你只用关心system design部分 有很多的link后面会重
复提到 建议看完至少一遍

2. https://www.youtube.com/watch?v=-W9F__D3oY4
非常非常好的入门资料 建议看3遍以上！
这是1里面提到的资料 是Harvard web app课的最后一节 讲scalability 里面会讲到很
多基础概念比如Vertical scaling, Horizontal scaling, Caching, Load balancing,
Database replication, Database partitioning 还会提到很多基本思想比如avoid 
single point of failure
再强调一遍 非常好的资料！

3. http://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones
1里面提到的 Scalability for Dummies 还算不错 可以看一遍 知道基本思想

结束语：当你结束这一部分的学习的时候 你已经比50%的candidate知道的多了(因为很
多人都不准备 或者不知道怎么准备system design) 恭喜:)

== 进阶 ==
这一部分的资料更加零散 每个看的可能不一样 但是你每多看一篇文章或者一个视频 
你就比别人强一点
这部分你会遇到很多新名词 我的建议是每当你遇到一个不懂的概念时 多google一下 
看看这个概念或者技术是什么意思 优点和缺点各是什么 什么时候用 这些你都知道以
后 你就可以把他运用到面试中 让面试官刮目相看了

4. http://highscalability.com/blog/2009/8/6/an-unorthodox-approach-to-database-design-the-coming-of-the.html
Database Sharding是一个很重要的概念 建议看一看

5. http://highscalability.com/all-time-favorites/
这个里面会讲到很多非常流行的网站架构是如何实现的 比如Twitter, Youtube, 
Pinterest, Google等等 我的建议是看5-6个 然后你应该已经建立起了一些基本的意识
还有知道了某些技术和产品的作用和mapping 比如说到cache你会想到memcached和
Redis 说到
load balancer你会想到 Amazon ELB, F5一类的

6. http://www.infoq.com/
5里面很多的文章都会有链接 其中有很多会指向这个网站 这里面有很多的tech talk 
很不错 可以看看

7. https://www.facebook.com/Engineering/notes
Facebook非常好的技术日志 会讲很多facebook的feature怎么实现的 比如facebook 
message:https://www.facebook.com/notes/facebook-engineering/the-underlying-
technology-of-messages/454991608919 建议看看 尤其是准备面facebook的同学
这有一个facebook talk讲storage的https://www.youtube.com/watch?v=5RfFhMwRAic

8. 一些国内网站上的资料
http://blog.csdn.net/sigh1988/article/details/9790337
http://blog.csdn.net/v_july_v/article/details/6279498

9. 最后一些概念很有用 都是我再看这些资料的时候发现的 如果你没有遇到或者查过 
建议查查
Distributed Hash Table
Eventual Consistency vs Strong Consistency
Read Heavy vs Write Heavy
Consistent Hashing
Sticky Sessions
Structured Data(uses DynamoDB) vs Unstructured Data(uses S3)http://smartdatacollective.com/michelenemschoff/206391/quick-guide-structured-and-unstructured-data http://stackoverflow.com/questions/18678315/amazon-s3-or-dynamodb

10 给有兴趣深入研究的人看的
Mining Massive Datasets --讲很多big data和data mining的东西
Big Data: Principles and best practices of scalable realtime data systems(http://www.amazon.com/gp/product/1617290343) --
twitter的前员工讲述如何处理实时数据 目前市面上讲解big data最好的一本书

10 凌乱的资料 随便看看吧
http://highscalability.com/blog/2013/10/28/design-decisions-for-scaling-your-high-traffic-feeds.html
== 小结＝＝
看多了以后 你的最终目标应该是心里有了一个大框架 一个基本的distributed system
是怎么搭起来的 然后心里有很多if condition 如果要是满足这个条件 我应该用什么
技术 比如如果read heavy那么用cache会提升performance之类的 同时知道应该避免什
么东西 比如避免single point of failure 再比如时间和空间的tradeoff在read 
heavy的时候应该倾向于时间 Write heavy的时候倾向于空间等等

你总结出来的和我总结出来的大框架和if conditions肯定不完全一样 但因为system 
design本来就是一个open ended question 所以不用害怕 能够自圆其说 就不会有问题

最后 本文纯属抛砖引玉 如果有大牛发现有错误或者有补充 欢迎留言 大家一起讨论

---
System design 一直是程序员面试时候的拦路虎, 一开始接触到的时候真的很迷茫, 不知道从哪里下手, 市面上的参考资料我基本上都读了一遍 ,  后来我自己一边面试一边总结, 终于摸到一套适合自己的方法, 并且很快就拿到了几个offer.  下面试着总结一下,也欢迎小伙伴们跟我一起讨论.

明确面试官的要求. 比如面试官问你: design a xxx. 这时候你就应该问: XXX 都有哪些功能呢?  一般面试官都会说2-3个. 这些功能就是你接下来设计的核心.

明确功能以后, 你就在黑板上画一个最简单的结构图, 一般系统设计都是从最简单的开始, 然后一点点往上加. 一遍在黑板上画, 一边解释为什么会有这些module

有了图以后, 面试官就会问你, 如何存 data, 用什么样的数据库.

这时候咱们已经有了一个基本的可以work 的 solution了, 接下来 面试官就会根据你的设计,问一些问题, 这些问题每个公司不一样, 但是关键点是你要说trade off, system design 没有正确答案, 就是看你肚里有多少货. 不熟悉的就千万别扯了,万一被面试官问到说不上了就扣分了.
资料链接: https://www.mitbbs.com/article_t/JobHunting/32777529.html

http://blog.csdn.net/sigh1988/article/details/9790337
