---
layout: mypost
title: Meta Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Meta Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>元联邦学习</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Omid Aramoon, Pin-Yu Chen, Gang Qu, Yuan Tian</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>CoRR, February 2021</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2021 年 2 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>当安全聚合到位时，是否可以防御后门攻击？</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>将客户端进行分组聚合之后进行防御</td>
    </tr>
</table>

# 内容总结

# 主要贡献

1. 提出了元联邦学习（Meta Federated Learning），这是一种新颖的联邦学习框架，有助于防御后门攻击，同时保护参与者的隐私。
2. 将防御执行点从个人更新级别移动到聚合级别可以在不损害隐私的情况下有效地缓解后门攻击。
3. 作者对标准联邦学习和 Meta-FL 中的当代后门攻击防御进行了系统评估,表明 Meta-FL 在对抗性攻击的鲁棒性和实用性方面增强了当代防御的性能。

# 问题描述和威胁模型

作者提出的元联邦学习框架没有做任何额外的假设。

### 攻击者目标

1. 对嵌入攻击者选择的触发器的输入的目标标签 `$T$` 进行错误分类；
2. 确保联合全局模型在后门子任务和手头的主要学习任务上都达到高精度。

### 攻击者能力

1. 假设攻击者控制了许多参与者，这些参与者在分布式学习的文献中被称为 Sybil。Sybil 要么是注入联邦学习系统的恶意客户端，要么是 FL 训练软件被对手破坏的良性客户端；
2. 根据柯克霍夫（Kerckhoffs）的理论，我们假设一个强大的攻击者能够完全控制其所有 Sybil 的本地数据和训练过程。攻击者可以修改训练过程的超参数，并能够在将模型更新提交给中央服务器之前修改模型更新；
3. 对手无法破坏中央服务器或影响其他良性客户端，更重要的是，无法访问良性客户端的本地模型、训练数据和提交的更新。

### 攻击方案

对手使用干净和后门数据的混合来训练其局部模型，并且模型更新计算为后门局部模型和共享全局模型的参数差。

1. 朴素（Naive）：直接提交计算模型更新。
2. 模型替换（Model Replacement）：使用比例因子改变模型更新的大小，以抵消其他良性客户端的贡献，并增加对抗性更新对联合全局模型的影响。（替换全局模型）

# 元联邦学习

### 联邦学习中防御后门攻击的挑战有两个方面：

1. 无论是否进行安全聚合，都不允许检查模型更新。
2. 客户端提交的模型更新显示出很大的变化，这使得中央服务器很难识别更新是否朝着对抗性目标工作。

### 概述

![基线和元联合学习中的模型训练概述](基线和元联合学习中的模型训练概述.png)

在我们的框架中，我们充分利用了参与者的丰富性（多），在每一轮中都有一个以上的训练队列参与模型训练。为了保护参与者的隐私，Meta-FL  引导SECAGG 协议来聚合来自每个训练队列的更新。在 Meta-FL 中，为服务器提供一组队列聚合，而不是单独的模型更新，这些聚合被进一步聚合以生成新的全局模型。

Meta-FL 将防御执行点从更新级别移动到聚合级别，通过提供以下优势，有助于缓解后门攻击：
1. 服务器可以在不侵犯参与者隐私的情况下监视队列聚合。因此，对手被迫注意其提交的内容，并在聚合级别上保持隐蔽，因为统计上与其他聚合不同的聚合可能会被标记和丢弃；
2. 与单个客户端更新相比，队列聚合表现出更少的变化，这使得服务器更容易检测异常；
3. 对手面临来自良性客户端的竞争，以控制队列聚合的价值，这阻碍了他们执行复杂的防御规避技术。

### 步骤

![算法1](算法1.png)

1. 在每一轮训练中，服务器随机选择 `$\pi$` 个队列，每个队列包含 `$c$` 个客户端；
2. 服务器向每个队列中的客户端 `$i$` 发送全局模型 `$G_t$`，每个客户端在其本地训练数据上对模型 `$G_t$` 进行独立训练，以获得新的本地模型 `$L_i^{t+1}$`，并将计算其模型更新 `$\delta_i=L_i^{t+1}-G_t$`；
3. 服务器同时对 `$\pi$` 个队列建立 `$\pi$` 安全聚合协议，分别对每个队列的客户端提交的更新进行聚合，从而得到 `$\pi$` 队列更新（注意：这样得到的队列更新是用明文表示的）；
4. 服务器可以用基于统计的防御方法对每个队列的聚合结果进行检测，在统计上不同于其他良性聚合的对抗聚合会被服务器检测到并丢弃；
5. 最后，服务器对良性的队列更新进行聚合得到全局更新，并用其更新全局模型。

### 将防御执行点从更新级别移动到聚合级别有助于缓解后门攻击，因为它具有以下优点：

1. 允许服务器检查和监控群组聚合。
2. 与帮助服务器检测异常的单个客户端更新相比，队列聚合的散发性较小；
   + ![公式2](公式2.png)
   + ![公式3](公式3.png)
3. 由于对抗性更新与其他更新聚合，Sybil 面临良性客户的竞争，以控制队列聚合的值。

# 实验

+ 数据集：SVHN 和 GTSRB
+ 数据分布：non-IID
+ 训练模型：SGD
+ 评估指标：模型准确率和攻击成功率
+ 攻击模式：像素模式后门攻击，固定频率攻击模型

### 实验结果

+ MFL-i-j：其中 i 和 j 分别表示训练队列的数量和大小。
+ FL-k：k 表示训练队列的大小。
+ Attack-f-k：在 FL 中，k 个 Sybils 在每 f 轮训练中发起攻击；在 Meta-FL 中， 在每 f 轮训练中，k 个训练队列包含一个对抗性客户。


![Meta-FL与基线FL的效用](Meta-FL与基线FL的效用.png)

+ 与基线设置相比，使用 Meta-FL 的联合训练可以产生更精确的模型。所有防御和聚合规则在作者的框架中都提供了更好的实用性。（Krum）

![在GTSRB模型上评估当代防御对朴素和模型替换后门攻击的性能](在GTSRB模型上评估当代防御对朴素和模型替换后门攻击的性能.png)

![在SVHN模型上评估当代防御对朴素和模型替换后门攻击的性能](在SVHN模型上评估当代防御对朴素和模型替换后门攻击的性能.png)

+ 随着我们沿着图 3 和图 4 中横轴所示的攻击场景前进，对手变得越来越强大，并且在每一轮中出现的 SYBIL 越来越多。
+ 在两个框架中具有相同数量的攻击对手
+ Meta-FL 在抵御后门攻击方面将所有防御置于优势地位。
+ 我们的实证评估表明，与基线FL相比，现有防御对 Meta FL 中的后门攻击更具鲁棒性。（Krum）

![训练队列的规模对CWM、Krum和TM对抗后门攻击的效果的影响](训练队列的规模对CWM、Krum和TM对抗后门攻击的效果的影响.png)

+ 增加训练组群的规模可以提高这些技术在所有场景中的鲁棒性，尤其是在对手更频繁地出现更多 Sybils 的场景中
+ 与中毒攻击相比，后门攻击往往更隐蔽，而对中毒攻击表现出弹性的防御可能无法抵抗后门攻击。

# 总结

在本文中，我们证明了在不侵犯参与客户端隐私的情况下防御后门攻击实际上是可能的。我们提出了 Meta-FL，一种新的联合学习框架，它不仅通过安全聚合协议保护参与者的隐私，而且有助于防御后门攻击。我们的实证评估表明，在提供相同或更好的效用的同时，与基线 FL 相比，Meta-FL 中最先进的防御技术往往更有效地抵御后门攻击。我们的结果表明，Meta-FL 不仅保护了参与者的隐私，而且比基线设置更好地优化了鲁棒性-效用权衡。

# 问题

1. 收敛性证明？
2. Non-iid？