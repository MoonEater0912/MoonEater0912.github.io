---
title: "Bootstrapping and Parameter Estimation"
date: 2025-01-10
layout: post
category: blog
tags: [Statistics]
---

在[Statistics Made Simple](https://podcasts.apple.com/us/podcast/statistics-made-simple/id597583061)这个播客（一个定量方法课的课程录音）里，Fulton把Bootstrapping作为一种参数估计的手段。具体来说，当样本量和抽样次数都受限时，研究者可以通过对单个sample的重复有放回采样来生成一系列新的samples，称为bootstrapping samples。参数区间估计的一个思路是获得一系列samples，计算它们各自的sample statistics，进而获得一个由sample statistics构成的sampling distribution。因此，Bootstrapping技术可以为实际上只能获得一个sample的情况，提供了一种替代性的方案，即使用bootstrapping samples来代替samples以获得sampling distribution，进而得到置信区间。

但乍一看这个思路是很反直觉的。参数估计是基于样本信息来获得对于总体参数的一个估计，估计的准确性（置信区间）应该只被a）我们对总体的先验知识，b）样本自身的规模来决定。而在进行Bootstrapping时，我们既没有获得关于总体的新的知识，也没有获得任何新的样本单位，那么采用这个方法去进行估计就显得很没有道理。甚至Bootstrapping方法可能还会引入更大的误差，因为它假设了这个唯一的sample能够well represent the population，换言之，我们必须假设我们所估计的这个参数就是几乎等于对应的样本统计量，这样才能生成可信的sampling distribution。但进行区间估计的目标恰恰就是为了一定程度上判断参数和统计量之间的差异。于是Bootstrapping在某种意义上似乎又是乞题的。

然而这个估计方法和参数估计在估计均值时是基本等价的。实际上，在总体分布和方差均未知的时候，我们使用样本标准差来计算标准误的这一步已经相当于进行了Bootstrapping。我用R语言模拟了总体为Gamma分布、样本量为50的一次1000-time Bootstrapping区间估计，用参数估计计算出的标准误SE和Bootstrapping sampling distribution的标准差之间的差异不到0.01，自然计算出的置信区间也相差无几。与此同时，假设样本统计量很好地代表了总体参数在这里并不会引入更多误差，因为样本均值本就是单样本估计时的最优估计手段，Bootstrapping所作的只是在计算置信区间。

另一方面，Bootstrapping的特殊优势在于其作为非参数估计方法，可以灵活地应对极端的非正态分布，或是其他统计量的估计（如中位数或方差）。我用R语言重复了一次对相同总体和样本的中位数估计，使用5000-time Bootstrapping，从结果图中可以看到，Bootstrapping给出了比较合理的置信区间。

![alt text](/images/Bootstrapping_median.png)

代码如下：

```R
library(boot)

population <- rgamma(100000, shape = 2, scale = 2)

sample_data <- sample(population, size = 50, replace = FALSE)

mean_function <- function(data, indices) {
  return(median(data[indices])) 
}

boot_results <- boot(data = sample_data, statistic = mean_function, R = 5000)

boot_ci <- boot.ci(boot_results, type = c("basic", "perc"))

hist(boot_results$t, main = "Bootstrapping 中位数分布", xlab = "样本中位数", breaks = 30, col = "lightblue")
abline(v = median(sample_data), col = "red", lwd = 2, lty = 2) 
abline(v = median(population), col = "green", lwd = 2, lty = 2) 
abline(v = boot_ci$percent[4:5], col = "grey", lwd = 2, lty = 2)
legend("topright", legend = c("样本中位数", "95% CI", "总体中位数"), col = c("red", "grey", "green"), lty = c(2, 2, 2))

```