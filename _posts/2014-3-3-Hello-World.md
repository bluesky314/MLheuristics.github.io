---
layout: post
title: The Perception of the Perceptron
---



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


Let us consider two inputs features $$x_{1}, x_{2}$$ which can either be 0 or 1 indicating absense or presence. The AND gate outputs a 1 if both inputs are 1 and 0 in all other cases. Our job is to find $$w_{1}, w_{2}$$ and b so that our perceptron behaves the same way. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/AND.png?raw=true" width="200" height="200">

The perceptron looks like ; $$w_{1}x_{1}+w_{2}x_{2}+b$$

As $$x_{1}, x_{2}$$ are desireable features we start by giving them positive weights of $$w_{1}, w_{2}$$=1.By playing around a bit we observe:

1. $$x_{1}, x_{2}$$=1 $$\Rightarrow $$ Output = 2
2. Either $$x_{1}, x_{2}$$=1 $$\Rightarrow $$ Output = 1

But since we want the second sum to be negative so that our step function can reduce it to 0, we make use of the perceptrons's thresholding factor and set b = -1.5

So now our outputs are all exactly as the AND table. The bias is effectively saying "Some of the features I am looking for are present but not enough". The whole concept of thresholding can be summed up by the previous line. 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/OR.png?raw=true" width="200" height="200">

Now consider the OR gate. The OR gate activates when atleast of the features is present. Since the OR gate just has less feature requirement, we can construct an OR gate by reducing the bias. We set b = -0.5.

A NOT gate simply takes an input, $$x_{1}$$ and inverses it. 0 become 1 and 1 becomes 0. This can be done as $$-x_{1}+1$$

If we pass our outputs from an AND gate to a NOT gate we have effectively created a NAND gate. A NAND gate is considered a universal gate i.e any computation can be computed only using a combination of NAND gates. Hence our single perceptrons can be combined for exactly the same behaviour. (You can playaround with logic gates a bit more at Lesson 2.8 of Udacity's Intro to Deep Learning with Pytorch course for free. ) We considered a simple case of two input features, but with many more features, a combination of perceptrons can form intricate logic conditions for the task at hand. We can construct multiple layers of perceptrons to make more and more elaborate compositions of logical operations in between the inputs. That network would look like: 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/hiddendiag.jpg?raw=true" width="400" height="200">

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

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Relu2.png?raw=true" >


Only difference from the step function is that it lets positive values remain as themselves. Let us say we have the task of estimation some value, maybe the house price based on various inputs. In this case our output cannot just be 0 or 1 but some number. This regression problem can be solved by finding an appropriate function $$h(x_{1}, x_{2}......x_{n})$$ which outputs the price based on the inputs.

Consider a MLP with one hidden layer with two perceptrons and one output node. Each perceptron will output a ReLU function as : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Reluhidden.png?raw=true" >

The output node will then take a weighted sum of these two functions as suppose : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/relusum.png?raw=true" width="500" height="366" >

By the next plot I hope you will be able to see the power of ReLU in approximating any function : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/x**2.png?raw=true" width="500" height="366" >

This looks alot like $$x^{2}$$ doesnt it? The Universal Approximation Theorem(1) says an MLP with enough ReLU's in one hidden layer can approximate any function to an arbitary degree of accuracy within a bounded region. Boundedness is a very important concept for any machine learning model but we look over it for now. Because we can pick up and place a ReLU anywhere by adjusting the thresholding factor or bias in each perceptron, we can simply stack ReLU functions side by side(you may be able to notice the dents in the $$x^{2}$$ plot above where one ReLU just began). In essence, using ReLU gives us the total power to change the gradient of our function at any point by adding a ReLU with the appropriate increase or decrease slope. If we have total control on the gradient, we have total control over what we want our function to look like as we can effectively steer it in any direction at any speed we like from any point onwards.(Quora link)

Suppose we have one hidden units with 4 perceptrons. How could we solve : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Fig2.png?raw=true" width="500" height="366 >

Pause to figure it out. You know enough! Or scroll down just a bit for a hint.

2 pair of neurons each would combine to form : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/ORplots.png?raw=true" >

And then ? Pause again to figure it out....

Then we simply pass this into an OR gate at the final node and our classes have been distinguised!

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Fig2.1.png?raw=true" width="500" height="366" >

Lets look at two more examples: 

Have a look at this example from [TensorFlow Playground](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=3&seed=0.69844&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false). 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/TFplaygroundc.png?raw=true" width="500" height="366 >
                                                                                                                                
 Just click play and you'll see a solution being formed. Running it twice yields two different solutions. In the first one, it cornered the Blue region from three sides and applied an AND gate to all three perceptrons. In the sencond it did something a bit different, and found an inverse region to apply a NOT gate to.
 
 In [this example] ( https://playground.tensorflow.org/#activation=relu&batchSize=10&dataset=spiral&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=7,7&seed=0.22727&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false).
 
 <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/TFsprial.png?raw=true" width="500" height="366" >
 
Here we see the power of more than one layer. The first layer, as it is only appling a single ReLU function, is able to spereate the space with only one line at each perceptron. But the next perceptrons takes all the inputs of the first layer each to form more intricate patterns( hover over the perceptrons to see). The first layer is optimized to give the best inputs into the next layer. 

Using the abstraction of logic gates in these examples made it extremely easy to see how our model could divide the data and what it would do in the end. We can apply this same abstraction to senerios where we have many more features to reason what our network is doing. For example, in a CNN the decision node in a dog detector may look something like: Nose AND (Pointy Ears OR Sharp Ears) AND Eyes AND Tail NOT (Glasses OR Clothes). In fact, these decisions are not stricty binary, but continous as each sub-operation in a single logical operator contributes some score(based on its weights) to the logical operator. So we get an output of how much the pattern being looked for is persent or absent. If it is present in enough amounts we say the perceptron is 'firing'.

Think about any such intricate logic, no matter how convoluted, and MLP's can mimick it. Each layer will create operations which will help the next layer create better operations in a pyramid like fasion to solve any intricate problem. Thats pretty powerful ! But what makes MLPs even more powerful is that not only can they apply these logical operations on features but they can construct their own features in the hidden layers on which to apply their operations on!  Woof ! Let that sink in for a bit.  


<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Fig2.1.png?raw=true" width="500" height="366" >



**Sigmoid**

Sigmoid functions are used on the outputs of MLP's in binary classification problems where we have two possible classes; telling whether an image is of a lion or giraff is such a problem. Sigmoid outputs a value between 0-1 that can be interpreted as the score or probability of one of the classes.

The sigmoid function is defined as:
$$ \begin{eqnarray} 
  \sigma(z) = \frac{1}{1+e^{-z}}.
\end{eqnarray}
$$

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/sigmoid.png?raw=true" >

We use the sigmoid in place of our step function at the end as instead of just outputting a 0 or 1 it gives us a score for how favorable our desired event is. If we are a little favorable, then we may get 0.55 and very then 0.95. Another great property is the sigmoid is differentiable, this will be useful for backpropagation(2).

If a class has a probability higher than 0.5 we pick that class. For our desired class : 

$$\frac{1}{1+e^{-z}} >0.5$$

$$e^{-z}>1$$

$$z>0$$

i.e z=0 is the equation of the decision boundary line/curve where input features show equal evidence of either class. 
**Proof**: 

Say, we are camping in the jungle and hear some footsteps at night. We want to classify if its a bear or a lion. By the sounds on the floor we estimate the weight of the animal and once we see it's silhouette we can estimate the height.  So we have features weight and height as $$x_{1}, x_{2}$$. For a given weight bears are taller than lions. Our model will give us the probability of being a lion since we will have to run much faster if it is. 

*Onto the math:* Suppose the decision boundry seperating the classes can be given by some linear function : 

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/lineaerdecision.png?raw=true" >

$$2x_{1}-5=x_{2}$$ is the boundry function i.e $$2x_{1}-5-x_{2}=0$$. Our model must output 0.5 for the entire line. 
For this to be true:

$$\frac{1}{1+e^{-z}} = 0.5$$

$$e^{-z}=1$$

$$z=0$$

$$z=2x_{1}-5-x_{2}$$


Consider a point on the line as shown in the right hand side image. If we enter $$x_{1}, x_{2}$$ at the point then our boundry equation will output zero and hence our decision function will output 0.5 - inconclusive

If we go upwards, as $$x_{2}$$ has a negative weight in the boundry equation, our boundry equation will become smaller causing the sigmoid function to fall below 0.5 indicating its probably not a lion therefore its a bear;  and the opposite will happen in case we move downwards. 

Generally speaking, moving in either direction from the decision boundry with respect to a variable will cause the boundary equation to either increase or decrease from zero depending on the sign of the variable. This will cause the decision function to no longer be indecisive. The sigmoid function searches for what combination of the input features display equal evidence to  both classes, by that it knows which are the positive and negative features towards any class, and then when features tilt in a direction it knows which class to pick. This same thing will apply if we had stacked a bunch of relu functions like in our $$x_{2}$$ example with $$relu(x_{1}-1)+relu(2x_{1}-2)+......-x_{2}=0$$ now being the boundary function. 

**Key point:** Arbitrarily complex functions can be created by stacking ReLUs side by side. Then the sigmoid turns these into a decision boundry and gives scores/probabilites for how close or far away points are from the boundry. To map more and more complex functions, we would need to have more terms in our boundary equation to create very non-linear functions with the ReLU's. Hence, easily separable data requires less perceptrons than more complicated data. 

This decision boundary is usually a non-linear boundary. What is and why is it non-linear?  [take e.g x-y>0, others]




