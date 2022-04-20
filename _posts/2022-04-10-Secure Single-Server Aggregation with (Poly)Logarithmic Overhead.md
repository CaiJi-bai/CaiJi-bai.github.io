---
layout: mypost
title: Secure Single-Server Aggregation with (Poly)Logarithmic Overhead
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Secure Single-Server Aggregation with (Poly)Logarithmic Overhead</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>具有（多）对数开销的安全单服务器聚合</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>James Henry Bell, Kallista A. Bonawitz, Adrià Gascón, Tancrède Lepoint, Mariana Raykova</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>27th CCS 2020: Virtual Event, USA</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020年10月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>（1）secure aggregation效率太低，如何在保证安全的情况下去提升效率？（2）shuffle model 开销大，如何去降低开销？</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>图生成算法</td>
    </tr>
</table>

# 内容总结  

# 概念  
- **k-连通图**：对于连通图G，其连通度K(G)>=k。换言之，对于k-连通图G，不存在大小为k-1的点集S，使得G-S不连通。（没有孤立点，任意两个顶点间有至少一条通路）
- **简单图**：不含平行边也不包含自环的图称为简单图。
- **完全图**：完全图是一个简单的无向图，其中每对不同的顶点之间都恰连有一条边相连。
- **正则图**：各顶点的度均相同的无向简单图。

# the semi-honest protocol  
**半诚实（诚实但好奇，被动的）**：敌手诚实的遵守协议，但也会试图从接收到的信息中学习更多除输出以外的信息。  
**整体思路**：先生成符合要求的无向图，再基于该无向图执行summation算法  
- **无向图生成算法**  
每个客户端要与其他k个客户端相连，相当于要构建一个有n个顶点的k连通无向图。在这个无向图里，顶点相当于一个客户端；每条边连接着的2个顶点意味着这2个客户端可以通过服务器进行秘密通信（服务器无法获知通信内容）。  
**该无向图应该同时满足3个性质：**  
（1）E1：不能有太多腐败的（即被黑客控制的）邻居节点  
（2）E2：当一些客户端掉线以后，依然可以保证整个图的连通性，也就是没有被孤立的节点  
（3）E3：不能有太多掉线的邻居节点，否则没有足够多的邻居节点来进行秘密重建(1 ≤ t ≤ k)  
![图生成算法](GenerateGraph.png)  

- **聚合协议**  
![聚合协议](abstract summation protocol.png)  

- **性能开销**  
客户端计算：$\log^2 n + l\log n$  
客户端通信：$\log n + l$  
服务器计算：$n\log^2 n + nl\log n$  
服务器通信：$n\log n + nl$  

# the malicious protocol
**恶意（主动的）**：敌手不遵守协议，可以执行任意的攻击行为。  
**整体思路**：先帮各个客户端交换密钥，再生成有向图，最后执行summation算法
- 交换密钥  

- 有向图生成算法  
E4：在每个客户端单方面信任的客户端集合里，corrupt客户端数量不能太多。  
E5：每个客户端的“交际圈”不能小于一定的比例 $\alpha$，不然容易被骗.  
E6：确保有足够多的邻居节点来接收秘密分享的内容。
- 聚合协议
![聚合协议](summation protocol in the malicious setting.png) 