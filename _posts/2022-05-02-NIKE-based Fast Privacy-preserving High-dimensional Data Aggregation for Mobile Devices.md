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
        <td>提高聚合方案的通信和计算效率，（1）密钥协商阶段的开销巨大，（2）秘密分享和恢复也很消耗时间。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>（1）引入了 NIKE，在离线阶段计算 master key。这种方法比 D-H 协议更加高效；<br>
            （2）对于 one-time pairwise key 的秘密分享采用 2-3 来取代 t-m。（正则图）
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
（1）在密码学中，密钥派生函数 (KDF) 是一种加密散列函数，它使用伪随机函数从一个秘密值（如主密钥、密码或密码短语）中派生出一个或多个秘密密钥。  
（2）KDF 可用于将密钥扩展为更长的密钥或获取所需格式的密钥，例如将作为 Diffie-Hellman 秘钥交换结果的组元素转换为用于 AES 的对称密钥。  
2. 单向函数  
单向函数 `$F:{\{0, 1\}}^k \rightarrow {\{0, 1\}}^n$` 是一个易于计算且难以求逆的函数。

# 系统模型概述  
+ 系统中有 1 个服务器，用于聚合结果。  
+ 系统中有 m 个用户，每个用户有一个 r 维的数据 `$x_i$`。该系统的目标是让服务器只学习当前用户输入的总和 `$\sum_ix_i$`，而不是其他任何东西。  
+ 系统中有 2 个密钥服务提供商（SSP），组成分布式 SSP。  

![系统模型概述](系统模型概述.png)

# 非交互式成对密钥建立方案  
**基本想法**：使用双变量多项式以非交互方式在用户之间导出成对密钥，其中单变量多项式在两个SSP（即 SSP1 和 SSP2）之间秘密共享。我们使用一个特殊的二元多项式，它是一个单变量多项式与两个自变量的乘积。  
   + 非交互式成对密钥计算 (NPKC) 方案由三个算法的元组组成：  
   ![NPKC](NPKC算法组成.png)
   + 具体实现  
   ![NPKC](NPKC具体实现.png)  
   其中，子协议 `$\pi_{EXP}$` 的细节如下所示：  
   ![EXP](EXP.png)


# 安全聚合方案  
**基本思路**：在我们的设置中，聚合协议由两个阶段组成。在离线阶段，每个用户从两个 SSP 接收两对秘密共享多项式，用于导出将在聚合和协议中使用的密钥材料。每个用户还从服务器接收有关其 `$l$` 正则通信网络邻居的信息。在在线阶段，服务器 S 与所有用户 U 运行聚合和协议，其中唯一的服务器接收聚合和作为输出。  

![安全聚合和协议](Protocol 2-1.png)
![安全聚合和协议](Protocol 2-2.png)
![安全聚合和协议](Protocol 2-3.png)

+ Round 0：非交互式成对密钥计算（NIKE）
  + 每个用户从 SSPs 接收两对秘密共享多项式
  + 每个用户计算 `$g_i(x)$` 和 `$h_i(x)$`
  + 每个用户计算自己和邻居节点的成对密钥 `$MK_{i,j}$` 和 `$EK_{i,j}$`
+ Round 1：由服务器发起聚合和计算
  + 服务器在 `$[T_l,T_{l+1}]$` 发起聚合，并通知用户，活跃的用户 `$U_0$` 响应服务器并参与聚合
  + 服务器广播 `$(\mathcal{U}_0, \tau, T_l, TS_l)$` 和签名 `${\sigma}_s$`
+ Round 2：基于单向密钥链的成对密钥掩码然后加密输入
  + 验证签名和邻居节点数量
  + 计算自掩码的密钥
  + 计算其与邻居节点的成对密钥
  + 秘密分享 `$MK$`
  + 计算并秘密分享 `${\kappa}_i$`
  + 计算成对掩码 `$q_{i,j}$`
  + 计算加双掩码后的输入 `${\alpha}_i$` 并发送给服务器
+ Round 3：故障恢复信息交换
  + 用户收到加密的 shares 后解密并保存，一旦任何解密过程失败就中止
  + 服务器收到用户发送的 `${\alpha}_i$`，用户记为 `$\mathcal{U}_1$` 判断 `$\mathcal{U}_1$` 中用户的数量是否大于 t，并发送给所有用户
  + 每个用户检查 `$U_i\in\mathcal{U}_1$`, `$|\mathcal{U}_1| \geq t$`, `$\mathcal{U}_1 \subseteq \mathcal{U}_0$`
  + 用户对 `$\mathcal{U}_1$` 签名发给服务器
  + 服务器将收到签名的用户记为 `$\mathcal{U}_2$` 并将签名发给 `$\mathcal{U}_2$` 中的用户
  + 用户检查用户数量和邻居数量
  + 用户验证 `$\mathcal{U}_2$` 中的所有用户的签名
  + 对于所有掉线的邻居用户，上传对应的 one-time pairwise key 的 shares；对于非邻居的掉线用户，上传 `$\perp$`；对于所有的在线用户，包括自己，上传关于 `${\kappa}_i$` 的 shares；
+ Round 4：通过服务器计算聚合和（解密然后取消掩码）
  + 将收到消息的客户端记为 `$\mathcal{U}_3$`
  + `$\mathcal{U}_0 = \mathcal{U}_3$` 没有用户掉线  
    （1）验证 shares  
    （2）重构 `${\kappa}_i$`  
    （3）计算聚合结果  
  + `$\mathcal{U}_3 < \mathcal{U}_3$` 有用户掉线
    （1）验证 shares  
    （2）重构 `${\kappa}_i$`  
    （3）重构 one-time pairwise key  
    （4）计算聚合结果  