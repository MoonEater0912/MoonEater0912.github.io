---
title: "Race to the Big Lab: Gender Disparities in Large Team Collaboration and Its Impact on Early Academic Careers"
date: 2025-04-07
layout: post
category: research
tags: [Python, Practice, Network Science]
image: "/images/2000_low.png"
---

This is the ongoing research I am working on as a research assistant at Aalto University, supervised by Keller Barbara. The manuscript is still under preparation.

The findings are - I believe - quite intuitive: 
- In academia, women scholars are less likely to be admitted into a "large lab / group", while men are more likely to be able to publish papers with many other co-authors (i.e., in a large lab or research group, typically including 8 or even more researchers). (Assumption 1)
- Such large team collaboration will impact the productivity (Assumption 2) and centrality / social capital (Assumption 3) of the scholars, especially in the early-career stage (first 10 years).

These findings provide a new perspective of the constraints faced by women in the academia - the collaboration pattern isn't simply determined by individual preference. Large team collaboration is also a kind of competetive resource. This introduces insights on how to understand preferential attachment model in the collaboration network, and helps to explain the "leaky pipeline" or "glass ceiling" phenomenon in the academia.

I used [SciSciNet](https://www.nature.com/articles/s41597-023-02198-9) to test these assumptions. To save time and memory, I used only the data in the field of computer science, in which I think the assumption above holds most. I constructed an un-directed collaboration graph, where the edges are weighted by the number of co-authors for one paper (if two authors collaborated more than once, we sum all the weights up):

$$
\omega_{u, v} = \sum_{i=1}^{num\_ papers}{\frac{1}{\text{number of co-authors}}}
$$

The assumptions are built, inspired by the distribution of edge weights: 

![alt text](/images/2000_low.png)
![alt text](/images/2000_upp.png)

For the assumption 1, survival analysis is conducted. For the assumption 2 and 3, to mitigate the problem of pre-treatment effect, Synthetic DID is utilized. Specifically, for the assumption 3, we develop a metric especially for measuring the centrality in the collaboration network as the outcome variable. First-time large-team collaboration is defined as the event indicator.