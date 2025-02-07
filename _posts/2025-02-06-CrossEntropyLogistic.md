---
title: "Cross Entropy vs. MSE in Logistic Regression"
date: 2025-02-06
layout: post
category: blog
---


In logistic regression's optimization problem, we use the cross entropy (CE) function as the cost function:

$$
L = -\sum_{i = 1}^{n}(y_i\ln{\frac{1}{1+e^{z}}} + (1-y)\ln{(1-\frac{1}{1+e^{z}}}))
$$

where

$$
z = \Theta x + b
$$

instead of MSE, which is commonly used in optimizing linear regression (OLS):

$$
L = \sum_{i = 1}^{n}(y_i - \frac{1}{1 + e^{\Theta x_i + b}})^2
$$

There are two reasons behind this difference. First, the practical meaning of CE in logistic regression is more intuitive. We use $u(z) = {\frac{1}{1+e^{z}}}$ to indicate the probability (explained later), and thus $\ln{\frac{1}{1+e^{z}}}$ in the cost function will force the probability of $z_i$ being 1 closer to 1 (so that $-y_i \ln{\frac{1}{1+e^{z}}}$ will be smaller). 

The motivation of $u(z)$ is that for probability $P = P(y = 1 | x)$, we can transform it into $\frac{P}{1-P}$, the logarithm of which is close to a linear line. So we have:

$$
\ln \frac{P}{1-P} = \Theta x + b
$$

which will lead us to:

$$
P = \frac{1}{1 + e^{\Theta x + b}}
$$

Therefore, the cross entropy function in logistic regression can be understood as the probability of the predicted distribution being equal to the observed distribution. However, MSE doesn't have such intuitive meaning when doing logistic regression, as it calculates the difference between $y_i$ and a probability, which certainly makes no sense.

The second reason to employ CE is that it is easier to be optimized. If we are gonna use gradient descent, the cost function needs to be convex (approximately at least) so that we can reach a generally global optimization point. In linear regression, it has been proved that MSE is a convex function, while this is not the case in logistic regression. To show this, we can calculate the partial derivative of $L_i$:

$$
L_i = (y_i - \frac{1}{1 + e^{\Theta x_i + b}})^2 
= (y_i - \phi(\Theta))^2
$$

where $\phi (\Theta) = \frac{1}{1 + e^{\Theta x_i + b}}$.

Thus:

$$
\begin{align*}
\frac{\delta L_i}{\delta \Theta} &= 
2\cdot (\phi(\Theta) - y_i) \cdot \frac{\delta \phi(\Theta)}{\delta \Theta}\\
&=
2\cdot (\phi(\Theta) - y_i) \cdot x_i \cdot {\phi^2(\Theta)} \cdot (1 - \frac{1}{\phi(\Theta)})
\end{align*}
$$
To determine whether $L$ is convex, we just need to check the sign of its 2nd-order derivative. So we ingnore the constant $2$ and $x_i$, and continue to calculate derivation:

$$
\begin{align*}
\frac{\delta^2 L_i}{\delta \Theta^2} & \propto
\frac{\delta (\phi(\Theta) - y_i) \cdot (\phi^2(\Theta) - \phi(\Theta))}{\delta \Theta}\\ &=
\phi'(\Theta)\cdot(\phi^2(\Theta) - \phi(\Theta)) + (\phi(\Theta) - y_i) \cdot \phi'(\Theta)\cdot (2\phi(\Theta) - 1) \\ &=
\phi'(\Theta)\cdot (3\phi^2(\Theta) - (3+2y_i)\phi(\Theta) + y_i) \\ &\propto
3\phi^2(\Theta) - (3+2y_i)\phi(\Theta) + y_i

\end{align*}
$$

For this final polynomial function about $\phi(\Theta)$, when $y_i = 0$, it is constantly negative, as $\phi(\Theta) \in (0, 1)$; while $y_i = 1$, its sign is not constant. Thus the lost function for MSE in logistic regression is not convex, making the usage of gradient descent unjustified anymore.

It is not difficult to prove that for CE, its lost function is constantly convex for every $i$. The cost function will thus has only one minimum. 
