---
layout: post
title: You're up and running!
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

This is edited.
**Figure**: Perceptron Model. [Source](http://neuralnetworksanddeeplearning.com/chap1.html).
 

**Figure**: ReLU. [Source](http://neuralnetworksanddeeplearning.com/chap3.html).



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
2. Either $$x_{1}, x_{2}$$=1 $$\Rightarrow $$ Output = 1

But since we want the second sum to be negative so that our step function can reduce it to 0, we make use of the perceptrons's thresholding factor and set b = -1.5

So now our outputs are all exactly as the AND table. The bias is effectively saying "Some of the features I am looking for are present but not enough". The whole concept of thresholding can be summed up by the previous line. 

Now consider the OR gate. The OR gate activates when atleast of the features is present. Since the OR gate just has less feature requirement, we can construct an OR gate by reducing the bias. We set b = -0.5.

For a NOT gate, $$x_{1}, x_{2}$$ are negative features as we don't want them, so we give them negative weights of -1 each. Then as we want the case of $$x_{1}, x_{2}$$ = 0 to output 1 , we can set b = +0.5 or any tiny postitive number and it behaves in the same way.

If we pass our outputs from an AND gate to a NOT gate we have effectively created a NAND gate. A NAND gate is considered a universal gate i.e any computation can be computed only using a combination of NAND gates. Hence our single perceptrons can be combined for exactly the same behaviour. (You can playaround with logic gates a bit more at Lesson 2.8 of Udacity's Intro to Deep Learning with Pytorch course for free. ) We considered a simple case of two input features, but with many more features, a combination of perceptrons can form intricate logic conditions for the task at hand. We can construct multiple layers of perceptrons to make more and more elaborate compositions of logical operations in between the inputs. That network would look like: 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/hiddendiag.jpg?raw=true" width="800" height="400">

A perceptron in the $$N^{th}$$ layer acts upon all the outputs of the $$N-1^{th}$$ layer. It computes another logical operation on all the operations already computed by the $$N-1^{th}$$ layer, therefore it is able to form a deeper operation with respect to the inputs.

Logical gates are a powerful abstraction to understand the representation power of perceptrons. We shall see more examples of it below. But as we move to continuous inputs and outputs we can more fully understand how MLPs are used for a range of modern tasks through the lense two important functions: ReLU and Sigmoid. In modern architectures ReLU's are used inplace of step functions and Sigmoid is used on the output of the MLP.


**Relu**

Usually in MLP's, ReLU's are used instead of the step function. A ReLU is defined as :


$$ 
\begin{eqnarray}
  \sigma(z) & = & \left\{ \begin{array}{ll}
      0 & \mbox{if } z \leq 0 \\
      z & \mbox{if } z > 0
      \end{array} \right.
\end{eqnarray}
$$

Or more compactly: $$\sigma (z)=max(z,0)$$

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/relu2.png?raw=true" >

Only different from the step function is that it lets positive values remain as themselves. Let us say we have the task of estimation some value, maybe the house price based on various inputs. In this case our output cannot just be 0 or 1 but some number. This regression problem can be solved by finding an appropriate function $$h(x_{1}, x_{2}......x_{n})$$ which outputs the price based on the inputs.

Consider a MLP with one hidden layer with two perceptrons and one output node. Each perceptron will output a ReLU function as : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Reluhidden.png?raw=true" >

The output node will then take a weighted sum of these two functions as suppose : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/relusum.png?raw=true" >

By the next short example I hope you will be able to see the power of ReLU in approximating any function : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/x**2.png?raw=true" >

This looks alot like $$x^{2}$$ doesnt it? The Universal Approximation Theorem(1) says an MLP with enough ReLU's in one hidden layer can approximate any function to an arbitary degree of accuracy within a bounded region. Boundedness is a very important concept for any machine learning model but we look over it for now. Because we can pick up and place a ReLU anywhere by adjusting the thresholding factor or bias in each perceptron so we can simply stack ReLU functions side by side. In essence, using ReLU gives us the total power to change the gradient of our function at any point by adding a ReLU with the appropriate increase or decrease slope. If we have total control on the gradient, we have total control over what we want our function to look like as we can effectively steer it in any direction at any speed we like. 

**Sigmoid**



