---
title: "The Cultural Ratchet of Science: Transmission Fidelity and the Divergent Evolution of Disciplines."
date: 2026-01-25
layout: post
category: research
tags: [Python, Practice]
image: "/images/umap_computerscience.png"
---

This is an ongoing side project that I am currently collaborating with Prof. Ethan Fosse and Prof. Nicholas Spence at UofT. The working paper is now being prepared.

We ask why some disciplines (e.g., Computer Science) exhibit a clear "temporal drift" while others (e.g., Sociology) remain in a static thematic space. We use the notion of **Cultural Ratchet Effect** (from evolutionary biology) to investigate this phenomenon, which indicates the process by which a field builds upon previous innovations without "backsliding". We hypothesize that the difference lies in **Transmission Fidelity**: the extent to which mentees inherit (and extend) the specific research deviations of their mentors (indicating new traits relative to their ancestors).

We developed a pipeline to measure intellectual inheritance across academic lineages and to operationalize the cultural ratchet and the transmission fidelity:

* **Publication Embedding:** Shifted from sparse TF-IDF (used in the original dataset) to **Specter2 Transformer embeddings**, which captures citation-aware semantic nuances, ensuring robustness even for scientific papers with sparse text. We also applied a normalization strategy to the embeddings to remove field-specific common components, thereby amplifying the semantic contrast between individual publications.
* **Weighted Author Vectors:** Instead of simple centroids, author vectors are pooled using a weight of $\frac{1}{n\_{authors}}$ per paper to prioritize individual research preferences over large-scale collaborations.
* **Decoupling Kinship from Cohort:** We introduced **Genealogical Distance** (sum of path length to a pair's Least Common Ancestor). This removed the collinearity between lineage proximity and publication year (Spearman's $\rho \approx 0$).
* **The Fidelity Metric:** We modeled inheritance using $Ancestor \to Parent \to Child$ triples:
    1.  **Parental Innovation ($\vec{v}_1$):** The component of the Parent’s vector orthogonal to the Ancestor:
        $$\vec{v}_1 = \vec{v}_{par} - \frac{\vec{v}_{par} \cdot \vec{v}_{anc}}{\|\vec{v}_{anc}\|^2} \vec{v}_{anc}$$
    2.  **Child’s Alignment ($P$):** The scalar projection of the Child’s vector $\vec{v}_2$ onto the Parental innovation $\vec{v}_1$:
        $$P = \frac{\vec{v}_1 \cdot \vec{v}_2}{\|\vec{v}_1\|^2}$$
        As a robustness check, we also calculated the cosine similarity between $\vec{v}_2$ and $\vec{v}_1$ to neutralize the impact of $\vec{v}_2$'s magnitude.


