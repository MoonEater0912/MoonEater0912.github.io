---
title: "Network of Entries of Stanford Encyclopedia of Philosophy"
date: 2025-02-17
layout: post
category: project
tags: [Python, Practice, Network Science]
---

I have scraped all the entries from the Stanford Encyclopedia of Philosophy, along with their interlinking relationships. The in-degree distribution of the entries roughly follows a power-law distribution (Figure below), with a few entries having extremely high in-degree, which supports the preferential attachment model. Using the PageRank algorithm, I identified the 20 most influential nodes, which can be categorized as follows:

1. Philosophers of Ancient Greece and Modern Europe: aristotle, kant, aquinas, plato (as well as neoplatonism), hegel, locke, descartes, plotinus, hume, leibniz.
2. Analytical philosophers: russell, frege.
3. Concepts of analytical philosophy: consequentialism, functionalism, probability-interpret, freewill, physicalism.
4. Liberalism.

![alt text](/images/SEPindegree.png)

It is clear that the ancient and modern western philosophy, as well as the comtemporary analytical philosophy, are of highest visibility on SEP. In contrast, Eastern philosophy and female philosophers are of lower visibility, or even totally invisible sometimes. Especially, I found some "orphan" entries, which means the in-degree of them are 0:

1. Non-western philosophers: al-baghdadi, al-qudat, etc.
2. Non-western philosophies: chinese-mind, chinese-phil-medicine, qing-philosophy, korean-philosophy, etc.
3. Female philosophers: catharine-macaulay, sophie-de-grouchy, rosa-luxemburg, etc.
4. Continental philosophy: michel-henry, moral-phenomenology, etc.

I am trying to use Bayesian classifier or SVM to identify some attributes of each entry (gender, school, region, etc.), so that a more solid causal identification and inference could be conducted (are these attributes related with pagerank score or the probability of being orphan entry).


