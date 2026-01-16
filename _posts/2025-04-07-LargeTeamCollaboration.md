---
title: "Race to the Big Lab: Gender Disparities in Large Team Collaboration and Its Impact on Early Academic Careers"
date: 2025-04-07
layout: post
category: research
tags: [Python, Practice, Network Science]
image: "/images/centrality.png"
---

This is the research I worked on as a research assistant at Aalto University, supervised by Keller Barbara. The paper is accpeted to CHI 2026 in Barcelona.

This study investigates the role of large-team collaboration in shaping early-career scholars’ academic capital, with a focus on gender disparities. Using longitudinal publication and collaboration data from [SciSciNet](https://www.nature.com/articles/s41597-023-02198-9) in Computer Science, we construct collaboration networks and define centrality to capture social capital. Large-team collaboration is defined based on coauthor counts and we apply synthetic difference-in-differences (SDID) models to estimate its effects. The results show that participation in large teams significantly enhances early-career scholars’ network centrality and publication productivity, suggesting that such collaborations provide academic capital that reinforce long-term career advantages. Meanwhile, we also document persistent gender gaps: women are less likely to access large-team collaborations. These findings highlight large-team collaboration as both a source of career acceleration and a mechanism of inequality. We conclude by highlighting implications for promoting equity and for designing strategies that foster more inclusive collaboration practices.

These findings provide a new perspective of the constraints faced by women in the academia - the collaboration pattern isn't simply determined by individual preference, and large team collaboration is also a kind of competetive resource, participating in the reproduction of gender inequality. This also introduces insights on how to understand preferential attachment model in the collaboration network, and helps to explain the "leaky pipeline" or "glass ceiling" phenomenon in the academia. Furthermore, we also make exploration on why large-team collaboration fosters scholars' career development: we found that after publishing in a large team, junior sholars are more likely to expand their collaboration network based on their previous neighborhood (a hint of organic and stable research relationship).

Here are the SDID results for publication counts and network centrality (dynamic effects with 3-year placebo tests of first-time large-team collaboration on these two metrics):

![alt text](/images/numpub.png)
![alt text](/images/centrality.png)

Survival curve accross five cohorts shows that female scholars are generally less likely to get into large group collaboration:

![alt text](/images/survival_overall.png)

Specifically, we constructed an un-directed collaboration graph, where the edges are weighted by the number of co-authors for one paper (if two authors collaborated more than once, we sum all the weights up):

$$
e_{u, v} = \sum_{i=1}^{num\_ papers}{\frac{1}{\text{number of co-authors}}}
$$

To better capture authors' social capital in academia, we defined a metric for measuring centrality (which is easy to compute and has intuitive sociological meaning):

$$
C_i = \sum_{j\in N(i)}e_{i,j}\text{WD}_j = \sum_{j\in N(i)}e_{i,j}\left(\sum_{k\in N(j)}e_{j,k}\right)
$$

The RQs are built, inspired by the distribution of edge weights: 

![alt text](/images/2000_low.png)
![alt text](/images/2000_upp.png)
