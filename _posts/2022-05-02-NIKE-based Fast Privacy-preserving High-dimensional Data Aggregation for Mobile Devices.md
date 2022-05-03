---
layout: mypost
title: NIKE-based Fast Privacy-preserving High-dimensional Data Aggregation for Mobile Devices
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>NIKE-based Fast Privacy-preserving High-dimensional Data Aggregation for Mobile Devices</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>基于 NIKE 的移动设备快速隐私保护高维数据聚合</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Kalikinkar Mandal, Guang Gong, Chuyi Liu</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>CACR Technical Report, CACR 2018-10</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2018年10月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>提高聚合方案的通信和计算效率</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>（1）引入了 NIKE，在线下计算 master key。这种方法比 D-H 协议更加高效；<br>
            （2）对于 one-time pairwise key 的秘密分享采用 2-3 来取代 t-m。
        </td>
    </tr>
</table>

# 内容总结  

# 主要贡献
1. 非交互式密钥建立协议  
2. 基于 NIKE 的安全聚合协议  
3. 实验评估和比较  

# 预备知识
1. KDF  
（1）在密码学中，密钥派生函数( KDF ) 是一种加密散列函数，它使用伪随机函数从一个秘密值（如主密钥、密码或密码短语）中派生出一个或多个秘密密钥。  
（2）KDF 可用于将密钥扩展为更长的密钥或获取所需格式的密钥，例如将作为Diffie-Hellman秘钥交换结果的组元素转换为用于AES的对称密钥.  
2. 单向函数  
单向函数 `$F:{\{0, 1\}}^k \rightarrow {\{0, 1\}}^n$` 是一个易于计算且难以求逆的函数。

# 系统模型概述  
![系统模型概述](系统模型概述.png)

# 非交互式成对密钥建立方案  

# 安全聚合方案  
![安全聚合和协议](Protocol 2-1.png)
![安全聚合和协议](Protocol 2-2.png)
![安全聚合和协议](Protocol 2-3.png)