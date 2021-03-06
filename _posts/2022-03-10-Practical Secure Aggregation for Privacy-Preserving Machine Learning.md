---
layout: mypost
title: Practical Secure Aggregation for Privacy-Preserving Machine Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Practical Secure Aggregation for Privacy-Preserving Machine Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>隐私保护机器学习的实用安全聚合</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Kallista A. Bonawitz, Vladimir Ivanov, Ben Kreuter, Antonio Marcedone, H. Brendan McMahan, Sarvar Patel, Daniel Ramage, Aaron Segal, Karn Seth</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>24th CCS 2017: Dallas, TX, USA</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2017年</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>解决安全聚合问题</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td>经典阅读</td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>双掩码安全聚合</td>
    </tr>
</table>

# 内容总结  
# 协议流程  
+ 第 0 轮：客户端初始化相关安全参数，生成公私钥对用于后续流程，并发送公钥给服务器。服务器收集足够客户端的公钥数据，并记录这一阶段的存活客户端为 u1。  
+ 第 1 轮：服务器广播收到的公钥给所有客户端。客户端拿到其他客户端的公钥,并随机生成生成混淆项 bu；将自己的私钥su以及bu通过秘密分享生成客户端总数量的碎片，并使用碎片对应客户端的的公钥 cu 加密，返回给服务器。服务器收集足够客户端加密的碎片数据，并记录这一阶段的存活客户端为 u2。
+ 第 2 轮：服务器将收集到的客户端加密的碎片数据转发到对应的客户端。客户端收到后根据混淆公式对自己的数据进行混淆，并将混淆后的数据发送给服务器。服务器将 u3 广播给每个客户端，并记录这一阶段的存活客户端为 u3。  
+ 第 3 轮：客户端收到 u3，检查客户端个数是否大于等于安全参数 t，小于则终止协议。若大于等于 t 则对 u3 进行签名将签名发送给服务器。服务器收集到足够客户端的签名，并记录这一阶段的存活客户端为 u4。  
+ 第 4 轮：服务器向客户端广播收集到的签名列表。客户端收到签名列表，验证签名列表大于等于安全参数 t，否则中止协议。如果大于等于安全参数t则进行验签。验签出错则中止协议。验签结束后，对于 u2 和 u3 的差集中的客户端，即离线客户端，向服务器发送离线客户端的私钥 su 的碎片，对于 u2 中的客户端，即在线客户端，向服务器发送在线客户端 bu 的碎片。服务器将收集到每个客户端的 bu 碎片进行还原，将收集到的离线客户端的 su 碎片进行还原，然后将收到的所有混淆数据根据聚合公式进行聚合，并使用恢复 su 减去离线客户端的混淆项，最终消去所有混淆项获得真实的聚合结果。具体的方式可参看原论文的详细协议流程。  

缺点：（1）该方案主要面向 cross-divce 问题。（2）大规模的使用Shamir's秘密分享带来的计算和通信开销。（3）需要客户端与服务器之间多轮通信，而且只支持加法聚合。  
适用范围：更适合轻量级客户端的安全聚合，只需要一个服务器，而且允许部分客户端与服务器合谋，安全性好。  

总结：Google 在 CCS2017 上提出了一种协议用来解决梯度聚合的安全问题，其核心思想是对于每一个客户端的梯度加上混淆项，由于混淆项是和其他客户端共同协商特殊构造的且只有自己知道，在聚合时，每个客户端传给服务器的梯度中的混淆项都可以消除掉，使得服务器可以在拿到真实的梯度聚合结果的前提下无法攻击到各客户端的真实梯度值。由于每一个客户端发来的都是混淆过的梯度，且梯度中的混淆项只有客户端自己知道，在其他客户端和服务器不合谋的前提下，可以保证各客户端梯度的隐私性。  

基于上述协议解决了MPC中的多方加减法运算，但其实借鉴上述协议思路，可以改造出适用于乘法和除法运算的协议，即项协议中的混淆公式和聚合公式中的加减依次替换为乘除就可以解决MPC中的多方乘除运算，但由于对多个混淆项交替进行了乘除运算，在最终聚合时会产生一定的精度损失，针对精度损失的问题则可以修改混淆公式，避免直接做除法运算，而在最终聚合时进行除法计算抵消混淆项。

# 参考

1. [Secure Aggregation](https://zhuanlan.zhihu.com/p/83786131){:target="_blank"}