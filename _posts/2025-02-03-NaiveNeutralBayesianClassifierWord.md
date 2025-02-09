---
title: "Some Notes on Naive Bayesian Classifier"
date: 2025-02-03
layout: post
category: blog
tags: [Statistics, Machine Learning, R]
---

[Naive Bayesian Classifier (NBC)](https://github.com/familyld/Machine_Learning/blob/master/07Bayes_classifier.md) is a kind of **generative models**. For classification task, we call these models as **discriminative models**: they directly model the a posteriori probability (or the decision boundary, i.e., given certain features, what is the probability of this sample being classified as class $C_i$), without considering the a priori probability of each class, nor the conditional probabilities of feature (features' probability distributions) given certain class. Examples include logistic regression (modelling the a posteriori probability) and SVM (modelling the decision boundary). While for generative models, we first focus on a) the a pripori probability distribution of classes; b) the conditional probability distribution of features (or the likelihood of observed features), and second calculate the a posteriori probability based on these information:

$$
P(C_i | x) = \frac{P(x | C_i)P(C_i)}{P(x)}
$$

where $x = (x_1, x_2, ..., x_n)$ is the feature vector.

The reason why we focus on the a posteriori probability is that, in classification tasks, it is related with the lost/cost function. When predicting a new sample using a model, we usually care about how much is the risk of predict error. Such risk can be analyzed as two parts: a) the probability that the model gives a wrong answer; b) the weights, i.e., the lost of each wrong answer. So we can define a risk function as follow:

$$
R_i = \sum_{j = 1}^{N}L_{ij}\cdot P(c_j | x_i)
$$

where $N$ is the number of all the possible results. Specifically, when conducting a binary-class classifying, $N$ is equal to the number of classes, which is $2$. $C_j$ is the predict result. $L_{ij}$ is set as 0 when $c_j = y_j$.

For classification task, the only thing we care about is whether the model predict the right class, so $L_{ij}$ is constantly $1$ when the prediction is wrong. Therefore, we have (a little bit confusion as $c_j$ means the j-th class while $c_i$ means the observed class of $x_i$ ):

$$
\begin{align*}
R_i &= \sum_{j for c_j != c_i }\cdot P(c_j | x_i)\\
&= 1 - P(c_i | x_i)
\end{align*}
$$

As the number of wrong prediction, as a matrix of model accuracy, is not good and smooth enough, we directly use $R_i$ (or its variation) to replace the cost function. In this way we will reach a discriminative model, such as logistic regression ($R_i$ is very closed to cross entropy). But if we use the Bayesian theorom first, we will get a Bayesian classifier, by analyzing the a posteriori into a priori and likelihood.

But here we encounter the two weaknesses of Bayesian classifier. The first one is about the calculation of likelihood, the second one is about the calculation of the a priori.

It is obviously very hard to compute $P(x \mid C_i) = P(x_i, x_2, ..., x_n \mid c_i)$ when $n$ is large and sample size is small. Commonly, not all the combinations of features will appear in the train dataset (Laplace smoothing could be used when it happens). To make our lives better, we usually have to introduce the conditional independency assumption, making Bayesian classifer naive:

$$
P(x_i, x_2, ..., x_n | c_i) = \prod{i = 1}{n}P(x_i | c_i)
$$

We can also use logarithm to make computation easier. However, this naive assumption is not always a reasonable assumption, in many cases different features are interdependent, even the class is given. For example, if we are developing a model to predict whether Bob likes certain movie (binary classes classification, *Like* and *Not Like*), and we know that Bob likes the movies acted by Chris Evans and those acted by Robert Downey Jr., while he doesn't like the movies acted by both these two superheroes (which clearly excludes all the Marvel movies). In such case, given the class *like*, the feature *Chris Evans* and the feature *Robert Downey Jr.* are negatively correlated; given the class *not like*, these two features are then positively correlated. Therefore, after introducing the naive assumption, NBC will not learn this knowledge, meaning it loses some important information, thus losing accuracy.

The problem with the a priori is not inevitable. If the sizes of positive set and negative set in the train dataset are significantly different (e.g., there are 1000 negative cases while only 50 positive cases), such unbalancy will mislead the model to predict all the unknown cases as negative, making the recall rate close to zero. To address this, undersampling or oversampling can be employed.

Another concern, usually for the text classification, is if there are many words indicating neutrality, the efficiency of predicting could be very low. In this case, as neutrality is not helpful for determine whether the case is positive or negative (it will add similar values to all the likelihood), we can ignore those neutral words, as well as ignoring those unpopular words (whose frequencies are not large enough to provide valuable information). Neutrality can be defined as:

$$
P(Word \mid Pos) \approx P(Word\mid Neg)
$$

However, such operation will not increase the accuracy, as it substracts nearly same values from all the likelihood ($P(\text{neutral word} \mid Pos)$, $P(\text{neutral word} \mid Neg)$, $P(\text{not neutral word} \mid Pos)$, $P(\text{not neutral word} \mid Neg)$, these four are nearly the same value). I've try to run such NBC ignoring neutral words, and there's just a very slight and random difference with the original result.

![alt text](/images/NBC_ignoring_neutral.png)

The code is attatched:

```Python
def tweet_classifier_ignoring_neutral(tweet, classifier_dict, threshold = 0.85):
    """ param tweet: string containing tweet message
        param classifier: dict containing 'basis' - training words
                                          'P(pos)' - class probabilities
                                          'P(neg)' - class probabilities
                                          'P(w|pos)' - conditional probabilities
                                          'P(w|neg)' - conditional probabilities
        param threshold: a float smaller than 1. The closer it is to 1, the harder to determine a word as neutral
        return: either 'Pos' or 'Neg'
    """
    words = tweet.lower().split(" ")
    P_likelihood_pos, P_likelihood_neg = 1, 1
    for word in popular_words:
        P_word_pos = classifier_dict['P(w|pos)'][word]
        P_word_neg = classifier_dict['P(w|neg)'][word]
        if P_word_pos/P_word_neg > threshold and P_word_pos/P_word_neg < (1/threshold):
            continue
        P_likelihood_pos *= P_word_pos if (word in words) else (1-P_word_pos)
        P_likelihood_neg *= P_word_neg if (word in words) else (1-P_word_neg)
    
    determine_pos = P_likelihood_pos * classifier_dict['P(pos)']
    determine_neg = P_likelihood_neg * classifier_dict['P(neg)']

    if determine_pos > determine_neg:
        return "Pos"
    elif determine_pos < determine_neg:
        return "Neg"
    else:
        return False

def test_classifier_ignoring_neutral(classifier, test_tweets, test_labels, threshold):
    total = len(test_tweets)
    correct = 0
    for (tweet,label) in zip(test_tweets, test_labels):
        predicted = tweet_classifier_ignoring_neutral(tweet,classifier, threshold)
        if predicted == label:
            correct = correct + 1
    return(correct/total)



import matplotlib.pyplot as plt

accs = []
thresholds = np.arange(0.65, 0.98, 0.01)
for threshold in thresholds:
    accs.append(test_classifier_ignoring_neutral(classifier, test_tweets, final_test_labels, threshold))

plt.plot(thresholds, accs)
plt.xlabel("Thresholds")
plt.ylabel("Accuracy")
plt.axhline(y=0.7194, color='r', linestyle='--', label="baseline")
plt.legend()
plt.show()
```

