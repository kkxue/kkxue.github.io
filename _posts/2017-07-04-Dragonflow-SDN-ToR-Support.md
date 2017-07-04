---
layout: post
author: kkxue
title: Dragonflow支持硬件交换机的必要和挑战
date: 2017-07-04 18:34:00 -0700
categories:
- Dragonflow
tags:
- Dragonflow
- SDN ToR
---

### 为什么加入硬件交换机

1.硬件交换机的加入对于Dragonflow形成商业解决方案很重要！ 配图来自链接1
<img src="https://raw.githubusercontent.com/kkxue/kkxue.github.io/master/public/img/tor1.jpg" />
首先是商业层面，客户认可纯软件解决方案还需要一段时间，所以打包硬件是必须的。
然后是性能，把隧道解封装卸载到TOR硬件，性能可以得到可观的提升，相应厂商有专业的测试可以验证。
如下图所示:
<img src="https://raw.githubusercontent.com/kkxue/kkxue.github.io/master/public/img/perf.jpg" />

然后是可以比较容易做到物理机和虚拟机混合组网，对于平滑演进具有一定意义。
还有一些额外的好处，比如虚拟机从物理主机出来的流量就没有封装，就可以做安全性检查了。

### 加入硬件交换机带来的挑战

硬件交换机的加入对开源方案（如Dragonflow）的影响很大！
挑战在于:

a.如何协同管理硬件和软件交换机（目前Dragonflow没有提供北向接口，参考链接2）；
虚拟网络和物理网络统一自动化运维
软件就不提了，硬件的话即Automated underlay network provisioning 可以参考链接4

b.开发测试会变得复杂，尤其是如果需要支持多厂商（可以借鉴neutron的解决方式）；

c.需要提供抽象支持不同硬件厂商，硬件厂商只需实现这些OVSDB/OpenFlow/RPC等接口，支持VXLAN，就能实现上述TOR（白牌机）功能定位；

d.谁来控制TOR? Dragonflow控制ToR是否合理？还是需要另外一个控制器(ODL等)来控制，并与Dragonflow交互？

如果Dragonflow控制ToR，相比后一种方案要更简洁，毕竟不需要涉及Neutron和Dragonflow以及第三方控制器之间的数据库同步等问题。
但是从实用角度来看，dragonflow没有必要重做轮子。
下图（配图来自链接1） 显示的是后一种方式：
<img src="https://raw.githubusercontent.com/kkxue/kkxue.github.io/master/public/img/tor2.jpg" />

e.需要支持拓扑自动发现
硬件规模大了之后，不可避免需要自动发现功能来简化运维和提高系统稳定性。参考链接4


参考资料:

1.http://www.slideshare.net/gampel/dragonflow-01-2016-tlv-meetup
2.https://zhuanlan.zhihu.com/p/25996102
3.https://www.ustack.com/blog/neutron-dragonflow/
4.http://www.h3c.com.hk/Technical_Support___Documents/Technical_Documents/Switches/H3C_S10500/H3C_S10500_Series_Switches/Configure/Configuration_Guide/H3C_S10500_CG-R7523P01-6W100/12/201609/951138_1285_0.htm

