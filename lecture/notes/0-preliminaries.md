# Notice

本笔记来自Berkeley的课程[CS285](http://rail.eecs.berkeley.edu/deeprlcourse/)。

笔记文件可以在[这里](./lecture/notes)找到

本笔记的架构：每一讲有一个单独的笔记。此外，[takeaway](./lecture/notes/takeaway.md)总结了所有讲的要点，类似于一个的“cheatsteet”。

# Preliminaries

学习RL，我们需要什么？

1. 一些DL的基本知识。 这个介绍DL的[repo](https://github.com/szjzc2018/dl)是一个非常好的仓库，欢迎给它点star。

2. 做好**记号混乱**的心理准备。如果学习过DL，就应该发现以下的场景是十分常见的：
    - 一个符号有多个完全不同的含义；
    - 多个符号代表完全相同的含义；
    - 前一页的符号在后一页变了；
    - 期待值不说明从哪个分布采样；
    - 还有最常见的：公式存在重要的typo。比如，在某些地方，$p^\star$和$p_\star$代表两个完全不同的意思，但又混用了。

我们会尽量避免这些现象发生，但必须先打好这一预防针。这也不是任何人的问题——如果你自己尝试把这些记号变得清楚整洁，你会发现你的公式（大概率）会变得长的离谱，令人无法忍受。所以，放弃吧——转而学习在混乱的记号中生存的能力：）

# What is Reinforcement Learning?

什么是RL？我们先用一个简单的问题来引入。

> Q: DL和RL有什么差别？
>
> A: 有一句话说的很好，“Generative models are impressive because the images look like something a person might draw; RL models are impressive because no person had thought of their strategies before.”
>
> 也就是说，DL的核心目标是给定一组固定的数据，我们的模型要学习这些数据里的规律，进而模仿它们。而RL则是对于一个动态的、随机的环境，我们的模型要学会在这个环境中做出最优的决策。
>
> DL的目标是有“标准答案”的，比如生成模型的目标就是使得它们的概率分布和原始数据集尽量地像；而RL的目标没有标准答案，或者说对于一个问题没有一个最“正确”的策略，人们只观察策略最终是否达到某种预期。
>
> 正是如此，RL的模型才如此令人惊艳——比如，在AlphaGo对战李世石的时候，RL模型给出了著名的"Move 37"，当时所有的围棋专家都无法理解这一步的意义。

总而言之，DL是一个**data**主导的过程，我们所需要做的一切就是拟合，不需要考虑任何其他因素；而RL是一个**optimization**主导的过程，我们关心的是优化最终的目标，中间的过程并不重要。这也就是为什么我们需要Deep Reinforcement Learning：DL的部分用来提取我们见到的数据的特征，而RL的部分用来做出最优的决策。

那么，RL的基本思想和核心问题是什么呢？这就说来话长了——让我们随着笔记的深入来一点点揭开这个神秘面纱吧。