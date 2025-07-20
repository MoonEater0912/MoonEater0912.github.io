---
title: "The Invisible in Philosophy: Network of Entries of Stanford Encyclopedia of Philosophy"
date: 2025-02-17
layout: post
category: research
tags: [Python, Practice, Network Science]
image: "/images/henry_lukacs.png"
---

The extended abstract, which was accepted by ICSSI \(2025\) in Copenhagen \(Poster session\), as well as by IC2S2 \(2025\) in Norrkoping \(Parallel Session\), can be found [here](https://mooneater0912.github.io/files/SEP_extended_abstract.pdf).

I added a part, which proposed a new, content-driven approach for navigating in the SEP network, mitigating the inequality of visibility and able to discover more nuanced entries connections. This part can be found in the [slides](https://mooneater0912.github.io/files/IC2S2_slides_SEP.pptx) for IC2S2 presentation.

I have scraped all the entries from the Stanford Encyclopedia of Philosophy, along with their interlinking relationships. The in-degree distribution of the entries roughly follows a power-law-like distribution, with a few entries having extremely high in-degree, which supports the preferential attachment model. 

It is clear that the ancient and modern western philosophy, as well as the comtemporary analytical philosophy, are of highest visibility on SEP. In contrast, Eastern philosophy and female philosophers are of lower visibility, or even totally invisible sometimes. Especially, I found some "orphan" entries, which means the in-degree of them are 0:

1. Non-western philosophers: al-baghdadi, al-qudat, etc.
2. Non-western philosophies: chinese-mind, chinese-phil-medicine, qing-philosophy, korean-philosophy, etc.
3. Female philosophers: catharine-macaulay, sophie-de-grouchy, rosa-luxemburg, etc.
4. Continental philosophy: michel-henry, moral-phenomenology, etc.

I have used Naive Beyesian Classifier to feature the nodes (is_female, is_continental, is_non_western), and developed two regression models (OLS for PageRank score, while Logit for Is_Orphan) to determine these factors' influence on entries' visibility or discoverability in SEP, controlling for the publication years. Detailes can be found in the extended abstract and the slides.

I developed a highly explainable new appoach to re-construct the SEP network. First, I used TF-IDF to transfer entries documents into vectors; Second, I calculate the pairwise cosine similarities. For any entry, if its similarity with the focal entry is higher than the 98\% percentile, then we assign a directed connection from the focal entry to it. This appoach can:
- Discover relevant and widely-recognized connection, such as Deleuze vs. Post-modernism.
- Discover cross-field but also reasonable connection, such as Michel Henry and Lukacs \(Michel Henry is previously an orphan\).
- Explain why the connection is there, for example, Michel Henry and Lukacs are similar as they both have strong focus on the concepts of life, form and immanence, although in different contexts. Deleuze and Postmodernism are similar as they are both related with Nietzsche, and both are concerned with empiricism \(Sensibility, Faculties, Experience, etc.\).
