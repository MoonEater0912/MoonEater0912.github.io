---
title: "Scaling Bias: How Team Size and Network Structure Amplify Gender Disparity in Research"
date: 2026-01-26
layout: post
category: research
tags: [Python, Practice, Network Science]
image: "/images/f_by_s_r.png"
---

This is the research I am currently working on as a visiting student at Aalto University, with Keller Barbara and Anh Duong Nguyen. The idea is motivated by our [previous work](https://mooneater0912.github.io/post/2025/04/07/LargeTeamCollaboration) published on CHI.

The aim is to introduce team-level dynamics, which is largely ignored before, into the analysis of scientific collaboration network. Currently we have found (details in this [working file](/files/teamsize_workingfile.pdf)) that gender homophily under existing imbalances leads to a persistent over-representation of men in team assemblage, a disparity that scales positively with team size. 

Next, we developed a mean-field analysis model to incorporate the team assembly mechanism into the network evolution process, using choice homophily and unbiased triad closure as the edge formation mechanism. We analysed the fixed point of the rate equation under different parametric settings and found that team size could exacerbate gender inequality (with regard to degree distribution) and segregation, while triad closure could mitigate these outcomes (although it might exacerbate within-group inequality, measured by Gini index). Specifically, with the same degree of choice homophily, males demonstrate higher levels of segregation, while females rely more heavily on collaborating with males to obtain degrees. We believe this explains why real-world data typically shows females exhibiting lower homophily tendencies. We also preliminarily validated these mathematical results using simulated networks. The working paper is being prepared.

In the next step, we plan to apply the model on real-world collaboration network, incorporating Bayesian models to estimate the parameters.
