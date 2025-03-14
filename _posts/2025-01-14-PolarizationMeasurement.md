---
title: "E-I Index: a Measurement for Ideology Polarization in a Network"
date: 2025-01-14
layout: post
category: blog
tags: [Statistics, Network Science]
---

*Note: I have written a sample code for E-I Index and rescaled E-I Index, including testing on a real world dataset, which can be seen [here](/htmls/EIIndex_congressman.html).*

E-I Index is a popular measurement for polarization. Naturally, we say a network is polarized, when there are more links between opposed nodes than those between homogenous nodes. Thus, we have the following definition:

$$
\text{E-I Index} = \frac{E-I}{E+I}
$$

where E indicates the number of edges between opposed nodes (external edges for each community), while I refers to the number of edges between homogenous nodes (internal edges for each community). The definition also works for directed graph. The value domain of E-I Index is a closed interval $\[-1, 1\]$. When E-I Index of graph $G$ is -1, then $G$ is extremely polarized (there's no edge between opposed nodes); when it turns out to be 1, then G is a bipartite graph. We can thus determine a network as polarized if its E-I Index is very close to -1.

There are some research using E-I Index to measure the degree of polarization within certain network. For example, [Röcher et al. (2020)](https://www.aup-online.com/content/journals/10.5117/CCR2020.1.004.ROCH) point out that the political discussion on Youtube is not polarized as people might envisage before, rather, users tend to interact more with those holding the opposite political opinions when engaged within an online political discussion. E-I Index is easy to compute, which is critical when analyzing a large dataset. Besides, E-I Index has another unique advantage: it can also be utilized to measure the degree of polarization / differentiation among multiple communities (more than two), as well as comparing the contributions of different communities. Two examples can be seen [here](https://pure.rug.nl/ws/portalfiles/portal/56900693/8406_31285_1_PB.pdf) and [here](https://journals.sagepub.com/doi/full/10.1177/0894439320987569#body-ref-bibr37-0894439320987569-1). The former uses E-I Index to measure the degree of polarization accross the whole network, while the latter uses E-I Index to measure the degree of polarization between each pair of parties.

One of the limitation is that, unless the E-I Index is equal with -1, we cannot determine how much the network is polarized. This is because the value of E-I Index is impacted by the network structure, such as the number of nodes in each community. For example, if the number of democrat MPs is 50, while the number of republican MPs is 100, then theoretically, there could be at most 12350 internal links in this network, while only 5000 external links at the maximum, which cause that if randomly distributed, the expected E-I Index should be around $-0.105$, rather than zero. In this case, if we get an observed E-I Index of $-0.5$, we are not able to determine it is polarized or not. On the other hand, if there's more than two communities in the network, different scales or sizes make it impossible to compare the E-I Index between different pairs of parties.

To address this limitation, the two papers mentioned above both take a strategy to rescale the E-I Index. The authors call it "permutation", but leaving it unexplained. The goals of this permutation strategy include: (a) making the E-I Index comparable; (b) rescaling the E-I Index into $\[-1, 1\]$ (though it already is in this interval). As we know nothing about the distribution of E-I Index in certain network, so the best way to do this is to establish a baseline distribution through randomization. On one hand, we can compute a z-score-like score to determine how much the deviation of the observed E-I Index is from the expectation when randomly distributed; on the other hand, we can use the distribution's quantiles to rescale the observed E-I Index. 

To conduct this randomization, basically we should keep the edge structure untouched, while randomly re-distributing the nodes' characteristics (i.e., which party or community each node belongs to). In this way, we keep the global features, making it possilble to determine the influence of nodes' characteristics. After let's say 5,000 times of randomization, we will hopefully get a distribution of randomized E-I Index, and we calculate the deviation score as follow:

$$
\text{d} = \frac{\text{EI}_{obs} - \mu}{\sigma}
$$

where $\sigma$ is the standard deviation of the baseline distribution, and the $\mu$ indicates the mean value of that distribution.

We calculate the rescaled E-I Index as follow:

$$
\begin{align*}
\text{E-I Index}^* & = \frac{2}{1 + \exp(k\cdot \text{d})} - 1\\
& = \frac{1 - \exp(k\cdot \text{d})}{1 + \exp(k\cdot \text{d})}
\end{align*}
$$

where $k$ refers to the rescaling coefficient. I set $k$ as 0.5 in my sample code. The smaller the $k$ is, the less sensitive the $\text{E-I Index}^*$ is when it is near zero. Thus, we recommend to set a small $k$ if the network is empirically highly polarized, while setting a large $k$ if the network is not likely to be polarized.

I used the [dataset of American congressman](https://voteview.com/data) to test the rescaled E-I Index. The results show that after the 97th Congress, that is, after the Reagan administration came to power, the degree of polarization of U.S. congressmen from both the Democratic and Republican parties (as reflected in congressional voting preferences) has stabilized at a high level, much higher than it had been before. The results are shown in the figure below. The lower the value is, the more polarized it is. Republican contributions to polarization seem to be higher in most Congresses. But after the 90s, Democratic contributions to network polarization regularly outstripped Republican ones.

![alt text](/images/congressman.png)

There is another important limitation of E-I Index as a measurement for polarization. [Hohmann et al. (2023)](https://www.michelecoscia.com/?p=2246) proposed a double definition about ideology polarization: (a) the structure should be polarized (which can be measured through E-I Index); (b) the opinions should be polarized. The E-I Index cannot be used to determine the condition b, as there's no part representing opinion in its formula. One negative consequence brought by this limitation is that, E-I Index needs a pre-determined classification to separate two communities (e.g., the Democrats and the Republicans). However, in the most real scenarios, there's no such classification. Sometimes we need to calculate people's ideology positions ourselves. To handle this problem, [Valle et al. (2018)](https://pure.rug.nl/ws/portalfiles/portal/56900693/8406_31285_1_PB.pdf) calculate two indexes for each pair of parties: (a) the E-I Index between these two parties; (b) the Euclidean distance this pair of parties in the two-dimensional ideology space. Nest, Valle et al. compute the correlational coefficient $r$ of these two indexes. The larger $r$ is, the stonger relation there is between opinion division and structural division in this network.

However, this try cannot calculate an absolute polarization score considering both opinion and structure. Besides, if there're only 2 or 3 parties in the network, the result of $r$ would be not robust. Hohmann et al. have given a more general way to measure the polarization in a two-party network. Assume that we have a series of values $\{o_i\}_{i=1}^n$, representing the ideological opinion position of each node, we can calculate a score using generalized Euclidean distance.