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
缺点：（1）该方案主要面向 cross-divce 问题。（2）大规模的使用Shamir's秘密分享带来的计算和通信开销。（3）需要客户端与服务器之间多轮通信，而且只支持加法聚合。  
适用范围：更适合轻量级客户端的安全聚合，只需要一个服务器，而且允许部分客户端与服务器合谋，安全性好。