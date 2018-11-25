---
layout: post
title: You're up and running!
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).
$$\sum_{n=1}^\infty 1/n^2 = \frac{\pi^2}{6}$$

This is edited.
**Figure**: Perceptron Model. [Source](http://neuralnetworksanddeeplearning.com/chap1.html).

**Algorithm**: Stochastic Gradient Descent

Here $\eta$ is called learning rate. 

**Figure**: ReLU. [Source](http://neuralnetworksanddeeplearning.com/chap3.html).


![alt text](https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Fig2.3.png?raw=true "Fig2.3")


///

We are given training pairs $(x^1, y^1), (x^2, y^2), \ldots, (x^n, y^n)$.
$$ v \rightarrow v' = v -\eta \nabla C = v -\frac{\eta}{n} \sum_{i = 1}^{n} \nabla C_i $$

<span class="marginnote">
    **Algorithm**: Stochastic Gradient Descent
</span>

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Fig2.3.png?raw=true" width="200" height="200" />



<img src='/images/config.png' height="138">

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).


**The Single Perceptron:**

A single perceptron is just a weighted linear combination of input features. Suppose we have inputs $$x_{1}, x_{2}......x_{n}$$ and corrosponding weights $$w_{1}, w_{2}......w_{n}$$. Then the dot product of these two vectors represented by: 
$$\sum\limits_{i=0}^{n}{x_{i}w_{i}}+b$$ 

We can think of the weights as the degrees of importance attached to each input feature. If more favourable features are present then the dot product will be higher. Therefore the linear combination gives us a score for what we are looking for. The bias term acts as a threshold, we shall see this more further.

The common symbol for this linear weighted sum in network diagrams is:
<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/linearsymbol.png?raw=true" >

**Representation Power**
We can show that a single perceptron, or less formally, a single weighted linear combination can act as a logical gate. In order to do this we include an activation function which in this case is a step function: 
$$ 
\begin{eqnarray}
  \sigma(z) & = & \left\{ \begin{array}{ll}
      0 & \mbox{if } z \leq 0 \\
      1 & \mbox{if } z > 0
      \end{array} \right.
\end{eqnarray}
$$

So our perceptron can now be written as:
$$Output=\sigma (\sum\limits_{i=0}^{n}{x_{i}w_{i}}+b )$$

(and table)
Let us consider two inputs features $$x_{1}, x_{2}$$ which can either be 0 or 1 indicating absense or presence. The AND gate outputs a 1 if both inputs are 1 and 0 in all other cases. Our job is to find $$w_{1}, w_{2}$$ and b so that our perceptron behaves the same way. As $$x_{1}, x_{2}$$ are desireable features we start by giving them positive weights of $$w_{1}, w_{2}$$=1.By playing around a bit we observe:

1. $$x_{1}, x_{2}$$=1 $$\Rightarrow $$ Output = 2
2. Either if $$x_{1}, x_{2}$$=1 $$\Rightarrow $$ Output = 1

But since we want the second sum to be negative so that our step function can reduce it to 0, we make use of the perceptrons's thresholding factor and set b = -1.5

So now our outputs are all exactly as the AND table. The bias is effectively saying "Some of the features I am looking for are present but not enough". The whole concept of thresholding can be summed up by the previous line. 

Now consider the OR gate. The OR gate activates when atleast of the features is present. Since the OR gate just has less feature requirement, we can construct an OR gate by reducing the bias. We set b = -0.5.

For a NOT gate, $$x_{1}, x_{2}$$ are negative features as we don't want them, so we give them negative weights of -1 each. Then as we want the case of $$x_{1}, x_{2}$$ = 0 to output 1 , we can set b = +0.5 or any tiny postitive number and it behaves in the same way.
