---
layout: mypost
title: Paper Reading Template
categories: [Test]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>联邦学习</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Jack</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>the 12th ACM Workshop</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020年10月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>解决问题</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td>经典阅读（可以详细谈一下）</td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>双掩码</td>
    </tr>
</table>

# 内容总结  
文章主要讲了联邦学习的相关知识。（谈谈自己的理解和想法）
注：评估部分可以简单讲一下，注重评估指标。  
假设各种基本操作的时间复杂度都是$O(1)$，$k=O(\log n)$，$l$ 是指客户端的输入向量长度。  
客户端计算：`\( \log^2 n + l\log n \)`  
客户端通信：`\( \log n + l \)`  
服务器计算：`\( n\log^2 n + nl\log n \)`  
服务器通信：`\( n\log n + nl \)`