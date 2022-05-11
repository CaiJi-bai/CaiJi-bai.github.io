---
layout: mypost
title: PrivFL_Practical Privacy-preserving Federated Regressions on High-dimensional Data over Mobile Networks
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>PrivFL: Practical Privacy-preserving Federated Regressions on High-dimensional Data over Mobile Networks</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>PrivFL：移动网络上高维数据的实用隐私保护联合回归</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Kalikinkar Mandal, Guang Gong</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>CCSW@CCS 2019: London, UK</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2019年11月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>解决联邦学习中的模型隐私保护问题</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td></td>
    </tr>
</table>

# 内容总结

# 主要贡献

1. 提出了 Dropout-robust 回归训练协议
2. 在三种不同的威胁模型中证明了训练协议的安全性，以对抗模拟范式中的半诚实对手
3. 实验评估

# 预备知识

**加法同态加密**：一个加法同态加密（HE）方案由一个四元组组成, `$HE=(KeyGen,Enc,Eval,Dec)$`。同态加密（Homomorphic Encryption,HE）指将原始数据经过同态加密后，对密文进行特定的运算，得到的密文计算结果在进行同态解密后的得到的明文等价于原始明文数据直接进行相同计算所得到的数据结果。

![同态加密](HE.png)

# 系统模型和目标

+ 系统模型

  系统中有 m 个用户和 1 个服务器，每个用户有一个数据集。

+ 系统目标
  + Dropout-robust 安全回归训练：使服务器能够在组合数据集上训练回归模型 `$\theta$`，同时允许用户在系统中随时退出，并确保移动用户的输入隐私和服务器的模型隐私。
  + 不经意预测：使移动用户学习在其私有输入上的预测输出 `$y$`，对应于回归模型 `$\theta$`，而不向服务器泄露 `$x$` 和不向用户泄露关于 `$\theta$` 的任何信息。

# 回归协议

**主要目标**：为基于适合移动设备的加密原语的回归模型开发安全的训练协议，并且对用户掉线场景具有鲁棒性。

+ Dropout-robust 安全缩放操作

  对于给定大小为 m 的集合 `$\{x_i\}$` 进行 scaling 操作，简单来说就是
  ![一维数据缩放](一维数据缩放.png)
  而对于高维的数据来说，例如数据集 `$D=D_1 \cup D_2\cup\ldots \cup D_m$`，scaling 便是对于每一个数据点进行操作。
  
  ![高维数据缩放](高维数据缩放.png)
  
  安全缩放操作
  
  ![安全聚合缩放](安全聚合缩放.png)
  
+ 整体思路