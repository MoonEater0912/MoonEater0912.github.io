---
title: "Bayes Estimate and Maximum-likelihood Estimate (with a small erratum for Hundred-page ML Book)"
date: 2025-01-15
layout: post
category: blog
tags: [Statistics, Machine Learning]
---

In page 24 (page 11 of Chap 2) of *The Hundred-page Book of Machine Learning* by Burkov, there is a formula combining the Bayes theorom and the full-probability formula to run maximum-likelihood algorithm of parameter estimation (by calculating the MAP - Maximum a posteriori Probability). The formula in the book is below:

$$
\Pr(\theta = \hat{\theta} \mid X = x) = \frac{\Pr(X = x \mid \theta = \hat{\theta}) \Pr(\theta = \hat{\theta})}{\sum_{\tilde{\theta}} \Pr(X = x \mid \theta = \tilde{\theta}) }
$$

Where the $\hat{\theta}$ indicates the sample statistics, $\tilde{\theta}$ indicates all the possible values of the parameter $\theta$, and $x$ indicates the unit. In a sample set $X = \{x_i\}_{i=1}^n$, we can compute the MAP for every $x_i (i \in \{1,2,...,n\})$.

However, the denominator of this formula is wrong. If we use the full-probability formula, there should be:

$$
\Pr(X = x) = \sum_{\tilde{\theta}}\Pr(X = x \mid \theta = \tilde{\theta}) \Pr(\theta = \tilde{\theta})
$$

Thus, we have a function of $\theta$:

$$
\text{AP}_i = \Pr(\theta = \hat{\theta} \mid X = x_i) = \frac{\Pr(X = x_i \mid \theta = \hat{\theta}) \Pr(\theta = \hat{\theta})}{\sum_{\tilde{\theta}} \Pr(X = x_i \mid \theta = \tilde{\theta}) \Pr(\theta = \tilde{\theta})}
$$

The reason we need AP is that, we believe the distribution of the parameter $\theta$ can be impacted by the observations (sample), which make it possible to adjust our knowledge about $\theta$ according to the $X$ or $x_i$. So let's say, before the observation, we held an a priori belief about $\theta$'s distribution (e.g., $\theta \sim \mathcal{N} (0, 10^2)$). Then, using the $\text{AP}_i$'s formula, we can get a function with the $\theta$ as its variable. By maximizing this function with the first observation $x_1$, we should be able to get a $\theta_1$ which makes the $\text{AP}_1$ reach its maximum ($\text{MAP}_1$). Next, for the second observation $x_2$, we can use the $\text{MAP}_1$ computed before as the new a priori knowledge about the parameter $\theta$, and then calculate the $\text{MAP}_2$. 

However, such a way which dynamically updates the a posteriori distribution of $\theta$ is only suitable when the possible value set of $\theta$ is finite, which makes the denominator of the formula computable. Otherwise, when the $\theta$ has an infinite value set, we need to do an one-time maximization on the following formula, which is called the Bayes estimate (although Burkov calls it Maximum-likelihood estimate):

$$
\text{BE} = \max \prod_{i = 1}^n \Pr (\theta = \hat{\theta} \mid X = x_i)
$$

as the denominator of $\text{AP}_i$ is independent with $\theta$, so we have:

$$
\begin{align*}
\theta^* & = \arg_{\theta} \max \prod_{i = 1}^n \Pr (\theta = \hat{\theta} \mid X = x_i)\\
& = \arg_{\theta} \max \prod_{i = 1}^n \Pr(X = x_i \mid \theta = \hat{\theta}) \Pr(\theta = \hat{\theta})
\end{align*}
$$
where $\theta^*$ is the estimated parameter(s).

It is clear that, because of the lack of dynamically updating, we only use the a priori distribution of the parameter once, which means that if the a priori distribution of $\theta$ is an uniform distribution, we will have:

$$
\begin{align*}
\theta^*
&=
\arg_{\theta} \max \prod_{i = 1}^n \Pr(X = x_i \mid \theta = \hat{\theta}) \Pr(\theta = \hat{\theta})\\
&=
\arg_{\theta} \max \prod_{i = 1}^n \Pr(X = x_i \mid \theta = \hat{\theta})
\end{align*}
$$

The latter is the formula of maximum-likelihood estimate. Therefore, if we don't have any idea about $\theta$'s value set and distribution, the Bayes estimation will return the same value with Maximum-likelihood estimation.
