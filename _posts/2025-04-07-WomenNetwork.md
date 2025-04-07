---
title: "One of Women's Opportunity Constraints in Academic Collaboration Networks"
date: 2025-04-07
layout: post
category: project
tags: [Python, Practice, Network Science]
---

The conclusion is - I believe - quite intuitive: in academia, women scholars are less likely to be admitted into a "large lab / group", while men are more likely to be able to publish papers with many other co-authors (i.e., in a large lab or research group, typically including 6 or even more researchers).

I used [SciSciNet](https://www.nature.com/articles/s41597-023-02198-9) to test this assumption. To save time and memory, I used only the data in the field of computer science, in which I think the assumption above holds most. The information of gender is provided by SciSciNet itself. Basically, I constructed two un-directed graphs, one is un-weighted, the other is weighted. For the un-weighted graph, the edge indicates collaboration \(no matter how many times of collaboration, there's only one edge between two nodes, in which case the degree only means the number of collaborators\). For the weighted graph, the edges are weighted by the number of co-authors for one paper:

$$
\omega_{u, v} = \sum_{i=1}^{num\_ papers}{\frac{1}{\text{number of co-authors}}}
$$

Then I calculated four distributions \(by permutation test, and the distributions are all normalized\) of E-I index - two for male, two for female, in these two graphs. But for comparison over time, I constructed two sets of them, in 2000 and 2009 respectively. So actually I created 8 distributions. The findings are interesting:
- Both male and female scholars show significant homophily \(with at least 4 standard deviations\).
- Male scholars show far more extreme homophily than female scholars do.
- Female scholars show less homophily in 2009 than in 2000 in both weighted and un-weighted graphs, while male scholars show more homophily in 2009 than in 2000 in weighted graph. 
- In weighted graph, the homophily of male is far more extreme than that in un-weighted graph, while the homophily of female scholars remains roughly the same after weighting the edges.

Basically there are two possibilities:
1. The edges between male nodes are in average more highly weighted \(which further means more frequent and less co-authors when collaborating with males\).
2. The edges between male nodes and female nodes are in average less highly weighted \(which further means less frequent and more co-authors when collaborating with females\).

To see which one is right, I computed the empirical cumulative distributions \(ECDF\) of the weights of male-male, male-female and female-female egdes respectively, in 2000 and 2009. The plots \(I only put 2000-year plots here\) show that the possibility 2 is more likely to be correct:
- When the weights are lower \(smaller than 0.5\), the number of male-male and male-female edges are higher than that of female-female edges.
- When the weights are higher \(higher than 0.5\), the number of female-female edges is the largest one, while the difference between male-female and male-male ECDs is decreasing, meaning that in this upper interval the number of male-female edges are less than that of male-male edges.
- In year of 2009, this pattern can be seen more clearly.


![alt text](/images/2000_low.png)
![alt text](/images/2000_upp.png)

Therefore, the possibility 2 is more supported. In addition, we know from the findings above that the collaboration between males scholars is more likely to happen in a large research group, while the collaboration between female scholars is more likely to happen in a small circle \(e.g., only 2 or 3 researchers\).

If this is true, than we should be able to observe that **a\)** the average degrees of male nodes is higher and **b\)** the average weighted clustering coefficient of male nodes is lower \(the collaboration network is broad and distributed\). These two are both supported by the plots below (again, I only put 2000-year plots here, while the pattern is more clear in 2009-year, implying that such academic collaboration model is more and more popular).

![alt text](/images/clustering_2000.png)

![alt text](/images/degree_kde_2000.png)

An easy explanation of this time trend is that, in 2009, the production model of lab collaboration is more popular than in 2000, and if a scholar is admitted into a large research group, he/she will be more likely to gain more degrees and accumulate power in academia faster. Further consequences might include higher H-index and more papers.

For the next step, we can
- to see if working in a lab can lead to higher influence or power in the academia.
- to see in which stage the likelihood of being admitted into a lab/group of male and female begins to differentiate \(probably in the early career stage\).