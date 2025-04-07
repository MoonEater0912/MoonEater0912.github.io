---
title: "The Invisible in Philosophy: Network of Entries of Stanford Encyclopedia of Philosophy"
date: 2025-02-17
layout: post
category: research
tags: [Python, Practice, Network Science]
---

\[The **extended abstract**, which was accepted by ICSSI \(2025\) in Norrkoping \(Poster session\), and where I conducted more analyses and visualization, can be found [here](https://mooneater0912.github.io/files/SEP_extended_abstract.pdf).\]

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

I have used Naive Beyesian Classifier to feature the nodes (is_female, is_continental, is_non_western), and developed two regression models (OLS for PageRank score, while Logit for Is_Orphan) to determine these factors' influence on entries' visibility or discoverability in SEP. Detailes can be found in the extended abstract.


