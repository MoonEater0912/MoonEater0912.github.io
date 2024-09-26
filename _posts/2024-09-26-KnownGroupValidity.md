---
title: "Known-Group-Validity"
date: 2024-09-26
layout: post
category: blog
tags: [Statistics, R, Methodology]
---

给导师打工的时候见到的一个方法，名字起的很高大上，又是validity又是RE又是effect size（cohen.d）的给导师也唬住了，遂命我研究研究怎么实现。看了一篇论文发现其实就是t检验的一个翻版。

在社会科学研究中一般使用t检验来检测两个组间的差异显著性，一类经典场景是处理组和控制组，在药物类实验中我们通常期望处理组的健康状况比控制组要好，这时就可用t检验来看组间差异是不是具有统计显著性。当然有时候也没有处理组和控制组的差别，比如个体的幸福指数，或者其他什么量表里的连续型变量，此时可以考虑用其均值作为cut-off value来定义组，进而比较组间差异。

但t检验的局限性在于它只能给出显著性水平，即差异具有统计显著性的概率，但并不能给出组间差异的一个可比较的度量。举例我们现在有四个组，A组和B组之间应该存在差异，C组和D组之间也应该存在差异，希望比较这两组“组”的差异之间孰大孰小，t检验就无法胜任，因为样本量是可能不一致的，算出来的t-statistics也就没有可比较的意义。另一个与之相关的场景是，我们已经知道了两个组之间应当存在差异，比如高教育投资的人具有高的收入水平，这一收入水平多半是显著高于低教育投资者，但研究者可能想具体地看看这个“高于”究竟是高了多少。这也就是发明 known group validity test 的主要动机，就是发明一个通用的度量衡，来测量组间差异的相对大小。

然而构造统计量的思路是很简单的，直观想过去无非用 组间均值差 除 合并标准差，就可以获得一个无量纲的差异度。这也就是 effect size 的计算方式，在R语言里可以使用cohen.d()函数来实现：

```R
# Assume there's a data frame called dt, where the column "value" is the dependent variable, and the column "group" defines whether the sample is in treatgroup or controlgroup.
# Now we can calculate the effect size of these two groups.

effect_size <- cohen.d(value ~ group, data = dt)
summary(effect_size)

```

在输出结果中，cohen.d这个函数会很贴心地把effect size的置信区间也给出来。[Thom Baguley](https://core.ac.uk/reader/30647780?utm_source=linkout)告诉我们 effect size 的最佳实践要求总是报告置信区间，同时尽可能详细地报告和两个组有关的描述性统计信息。除此之外，Thom Baguley也提醒我们注意组间的方差差异，因为比方说研究者想看两个处理组相对于同一个控制组，谁的处理效应更强，那么很明显的是即便两个处理组的均值相同，有更高方差的那个组也总是会报告更低的 effect size（更高方差的组，它和控制组的合并标准差也会更大）。

关于cohen.d也还有一个迷思，和p值的0.05一样，[Sawilowsky](https://jmasm.com/index.php/jmasm/article/view/452)也为这个统计量规定了一些特殊值，包括0.2代表small，0.5是medium，0.8以上就是large乃至very large。这一规定的局限性，除了忽略了方差因素和置信区间以外，也在于没能看到它的本质也就是个概率值。[Yihui Xie](https://yihui.org/cn/2018/02/cohen-s-d/)已经做了相关的批评。实际上观察公式，cohen.d就是t统计量多除了一个自由度的开方（t统计量的分母是标准误，也就是合并标准差的分母平方后的结果），因此cohen.d的密度函数本质上也就是t分布的密度函数的一个拉伸变换。

```R

n <- 30 # n refers to the degree of frredom, usually is n1+n2-2
x <- seq(0, 12, 0.01) 
plot(x / sqrt(n), 2 * ( 1 - pt(x, n-1))) 

```

![alt text](/images/cohend.png)

借助这张图可以得到在特定的自由度下，cohen.d值对应的概率值是多少（双尾检验，x允许非正的话就不需要乘2）。这个概率值就是t检验所获得的p值。

另一个做 Known group analysis 时常见的统计量是RE，也就是 relative effect 的缩写。这个原理就非常简单了，一般运用在两个场景下：1）比较两个处理组分别和一个控制组的差异的大小，也就是看哪种处理更强；2）比较两种量表（两种因变量）谁比较能够区分出处理组和控制组的差异。明显cohen.d都可以胜任这两个场景，cohen.d能够返回一个无量纲因而可比较的统计量。而RE的动机会更简单：只需要看这特定的两个差异值谁更强。

因此，对RE来说，首先存在两个差异（比方说处理组a和控制组的差异 vs 处理组b和控制组的差异，或者量表a下处理组和控制组的差异 vs 量表b下处理组和控制组的差异），接下来使用ANOVA计算出两个差异对应的F-statistics，再把这两个F统计量相除，就获得了RE。一般我们在论文里报告RE时会规定一个差异对应的RE是1，另一个差异对应的RE就是这个 ratio of F-statistics。F统计量是组间均方（离差平方和 / 自由度）和组内均方的比，对于方差齐性同样有要求，否则算出来的统计量不服从F分布。同时如果某个处理组的方差较大，会降低它的F值。不过RE毕竟是一个相对值，某种程度上说其误导程度会低于cohen.d。