---
layout: post
title: Coming Soon
---
Blogpost on 3 recent continual learning covering :

Overcoming catastrophic forgetting problem by weight consolidation and long-term memory : https://arxiv.org/abs/1805.07441

Memory Aware Synapses - Learning what (not) to forget : https://arxiv.org/abs/1711.09601

Selfless Sequential Learning: https://arxiv.org/abs/1806.05421
 

---

##We humans are able to continually learn from experience and improve our performance on a task even if the information we learn from is spaced out in time or some of it is never shown again to us. Like when we learnt the english language, we no longer have to revise the rules of grammer as they have become solidified into our memory and we just keep learning more semantically complex words/phrases as we grow.(Link to second paper) We would like our neural networks to engage in such a learning process as well where its learning is compounding continually. However, the key of this process is that we must not forget what we learnt before. And this is where neural networks are know to fail. Usually, we deploy our neural network and freeze its weights. But if we did'nt freeze them and made them able to learn from new data out in the field, the network would learn the new information but would start erasing what it learnt before by overwritting the weights. This is what is called 'catostopic forgetting'. 

This blog is on sequential learning and how we can get neural networks to continue training once deployed in the wild under a variety of different constraints. This is a very practical and interesting concept that our models will have to eventually incorporate if we want to increase the adaptation ability of our networks. This is a crucial issues of deploying neural networks that is often ignored in research communities. Understanding how disentangled representations affect learning is something I have been looking into since.

Sequential learning, also referred to as continual, incremental, or lifelong learning (LLL), studies the problem of learning a sequence of tasks, one at a time, without access to the training data of previous or future tasks. Our main objective is : How do we add new classes to a model that is already trained on some finite number of classes?


<div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/icvpig/image13.png?raw=true" width="900" height="466" >
    <center>Incremental Learning rules</center>
</div>



**First lets break down why this is difficult : **

There are several naive approaches. One would be to simply add nodes for the extra classes in the softmax layer and train the model as the classes come. However this leads to the problem of ‘catastrophic forgetting’ where the network erases representations it learned for classes earlier in favor of the newer classes.  Another approach following this would be fix the feature layers and only train the classifier at the end. However the model then may not pickup on essential features which it does not have the appropriate filters for as the early filters are fixed. This is problematic when the class differences get small such as among household objects. Another approach would be just to train several model again and again or have separate models for new and old classes; the problems in both approaches can be easily inferred. 

Our network tries to learn some optimal weights $\theta$. $\theta$ lives in some N-dimensional space where N is the number of parameters in the model. Now in this space we know that they are multiple $\theta$s that would give us a similar loss. The larger we make the space of $\theta$s i.e N, the more number of optimal $\theta$'s there will be. Simply because I can take any optimal $\theta$ from the smaller space, and arrange it in many more ways in this larger space. We shall see a illustration of this below.  there are  $\theta_A^*$
 
 
Let us consider a system of only two weights for simplicity. Lets say that we have two tasks A and B. A's optimal weights are (2,2) and B's are (8,10). Now if I merge dataset A and B and try to learn (2,2) and (8,10) at the same time we would end up at around the average of the two (5,6) as that minimizes the average loss. Now say, I add two more weights to my model. If my first two weights learn (2,2), the third and fourth can learn (8,10) (this is not exactly how it would happen but enough to get the basic idea). So the two extra dimensions, gives the network more freedom to accomidate both representations. The fact that representation power increases as number of parameters increase is no suprise but key point here is how that is related to the networks inclination to erase representations it has previously learnt. In the first example it would **have to** erase what was learnt and in the second it **may not**. 
 
 Now consider if I was training them in sequence:
 
 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/cont1.png?raw=true" width="550" height="466" >
    <center> First Task A</center>
</div>


<div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/cont2.png?raw=true" width="550" height="466" >
    <center> Then Task B</center>
</div>

 
 If I had only two paramaters and were to train on A first and then on B, then my paramaters would change from (2,2) to (8,10). But what if were to add two paramaters now and continue training? In that case, the network has no incentive to keep the earlier paramaters as the new gradients are calculated for all parameters and the earlier ones will be repourposed altering their representations. Therefore the parameters are repourposed even though there is enough space to accommodate the new representations. This brings us to our first challenge : How to prevent the network from erasing representations of tsask A when it does'nt have to?
 
 The second challenge is a bit more subtle and related to *how* a network encapusulates the representations it has learnt. By this I mean does it learn dense or sparse representations. In the above example we say that even if the representations could be learnt using two paramteres, the network will still break that computation into smaller chunks and distribute it among all available parameters. This means a neural network naturally learns a sparse representation.(Check out one of ICLR 2019's <a href="https://venturebeat.com/2019/05/06/mit-csail-details-technique-that-shrinks-the-size-of-neural-networks-without-compromising-accuracy/">best paper</a> for an interesting follow up on this) If we could get the network to learn more dense representations that this would reduce the need to erase previous representations.
 
- And if the optimal weights were (8,10) then for four it would be (4,4,6,2) or such as the network is forced to learn a **distributed representation** vs a compact one by design.

So the two major problems of continual learning are:
1) Knowing which weights are important and which to change
2) Learnin g a more dense representation if possible

If we can appreciate these two major problems then we are already halfway done in understanding these three papers. 

 ## Elastic weight consolidation
 
The following theoretical explanation is not vital to understanding the proposed solution but is good to know. 
It's important to understand what training a network means from a probabilistic perspective. Supposing we have some data $\mathcal{D}$, we'd like to find the most probable parameters given the data, which is expressed as $p(\theta | \mathcal{D})$. What does this mean? Lets say there was only one optimal solution $\Theta _{1}$ then $p(\theta = \Theta _{1} | \mathcal{D}) =1 $ ,as every time we train our network we would converge to the same weights, and 0 for all others $\Theta$s.

Now say there were multiple optimas, $$\Theta_1 ..... \Theta_k$$. Some of these would be more probable that others due to factors like our initialization and how easily they are accessible in weight space. Unfeasible weights will have a probability of 0 and hard to access weights a lower probability that the rest. 

In short: $p(\theta | \mathcal{D})$  means what fraction of the times I would reach that theta if I were to train my network an infinite number of times.


We can calculate this conditional probability using Bayes' rule:

Bayes theorem states:
 $
 \begin{align}
 p(\theta | \mathcal{D}) &= \frac{p(\mathcal{D} | \theta) p(\theta)}{p(\mathcal{D})}
 \end{align}
 $
 
 Applying logs on both sides: 
 <center>
 $
 \begin{align}
 \log p(\theta | \mathcal{D}) &= \log p(\mathcal{D} | \theta) + \log p(\theta) - \log p(\mathcal{D})
 \end{align}
 $
 </center>
          
          
After we train on task A, the distribution of the weights will follow $p(\theta | \mathcal{D}_A)$. This kbecomes our new initilization for task B (just as in the simplier cases above)
$
\begin{align}
\log p(\theta | \mathcal{D}) &= \log p(\mathcal{D}_B | \Theta) + \log p(\Theta | \mathcal{D}_A) - \log p(\mathcal{D}_B)\\
\end{align}
$

The left side gives us the distribution of theta of training task A and then B. All the information learned when solving task A is contained in the conditional probability $p(\Theta | \mathcal{D}_A). 

This is essentially the initilization of the network before we train on task B.


Having this as our initilization tells us the weights $\Theta$ will finally reach are influenced by $\Theta_A$. The network is more likely to settle on weights closer to $\Theta_A$ in weight space. However, the abstract representations these weights represent are very sensitive to magnitude changes to the weights. So even though we have a natural inclination to end up closer to the solution of Task A in weight space, it is still too far in representation space. This posterior has all the information about what the network learnt from task A. 

The posterior $p(\theta | \mathcal{D}_A)$ is intractable i.e very difficult to compute thus we use an approximation. Rather than numerically approximating the posterior distribituion, we approximate it as a multivariate normal distribution using $\theta_A^*$  as the means. For the variance? We're going to specify the variance for each variable as <a href="https://en.wikipedia.org/wiki/Precision_(statistics)">precision</a>, the reciprocal of the variance. 
 Why is this? 
 
 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/normal_density_plot_2.png?raw=true" width="550" height="466" >
    <center> Two Gaussians with difference variances</center>
</div>
 
 Let $\theta_{ij}^*$ be the paramater in the i'th layer and j'th neuron.
 Let's take two gaussians having the same mean. Each reprenting two different parameters. If a weight is very important, it will have low variance, i.e the network will not continually alter it or pull it rapidy back when it does. A weight with higher variance means that there are more multiple suitable values for the weight. Thus the variance can be used to measure the importance of the weight. Weights with high importance have low variance and vice versa.
 
 
The Fisher information matrix $F$. <a href="https://en.wikipedia.org/wiki/Fisher_information">Fisher information</a> is "a way of measuring the amout of information that an observable random variable X carries about an unknown parameter $\theta$ upon which the probability of X depends." This is very close to the inverse variance of $\theta_{ij}^*$ . The Fisher information matrix is much more feasible to calculate than numerical approximation, which makes it a useful tool.

So, as we want to penalize changes to these important weights, we add this new term in our loss function which penalizes changes to weights according to their computed importance : 

$
\begin{align}
\mathcal{L}(\theta) = \mathcal{L}_B(\theta) + \sum\limits_{i} \frac{\lambda}{2} F_i (\theta_i - \theta_{A,i}^*)^2
\end{align}
$


 ## Memory Aware Synapses
 
 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/icvpig/image8.png?raw=true" width="900" height="466" >
    <center>Weight Consolidation - finding a balance between task A and B</center>
</div>


The approach here is different by one key aspect put succinctly in the paper as "Like other model-based approaches,
we estimate an importance weight for each parameter in the network. Yet in our case,
these importance weights approximate the sensitivity of the learned function to a param-
eter change rather than a measure of the (inverse of) parameter uncertainty, as in [12], or
the sensitivity of the loss to a parameter change, as in [39]. As it does not
depend on the ground truth labels, our approach allows computing the importance us-
ing any available data (unlabeled) which in turn allows for an adaptation to user-specific
settings."

The larger philosophy is the same as the first paper: We train our initial model and identify critical weights crucial for each class. Accordingly, we assign a weight to each neuron propotional to it's level of importance. Later, when we introduce new classes we penalise changes to the neurons depeding upon their given weight. 

Let $$\Omega_{ij}$$ denote the weight given to the i'th neuron in the j'th layer and let to the old and new proposed weights be denoted by $$\Theta_{ij}$$ and $$\Theta_{ij^{*}}$$. Our model is the function F that maps $x_{i}$ to $y_{i}$ by $F(x_{i}) = y_{i}$ . The importance of any one weight can be measured by how much changing it will change the output. This is nothing by the derivative of F with respect to $\Theta_{ij}$


$g_ij = \frac{\partial F(x)}{\partial \Theta_ij}$

To get the importance of very parameter, we take the average of its derivative over the entire dataset:

$\Omega _{ijk} = \frac{1}{N} \sum_{D=1}^{N} g_{ijk}(x_{D} )$

This represents the average importance of each parameter. The higher \Omega _{ijk} is the higher the importance of that parameter.

-- squared form

Now when task B has to be learnt we have an addition to the loss, a regularizer that penalizes changes to parameters that are deemed important for previous tasks:

$L_{B}= Loss +  \lambda\sum\limits_{ij}\Omega_{ij}(\Theta_{ij}-\Theta_{ij}^{*})^{2}$

The weights are found by the effect that changing them has on the loss. $$\frac{dL}{dw_{ij}}$$, is computed for each parameter and then the avgerage is taken over all points in *our* dataset. By our dataset I mean the one in which we expect our model to perform on. This is important as if we are using a model pretrained on ImageNet and dont require knowledge of certain casses then the model can forget those classes by associating a low cost to changing weights associated with those classes. This act of penalizing changes to important weights is called **Weight Consolidaion**.


**Self-less Sequential Learning**


<div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/icvpig/image6.png?raw=true" width="900" height="466" >
    <center>Weight consolidation along with corelation penalization</center>
</div>

Our motivation here is to encourage model sparsity, i.e even if our model is of large size the representation required for the target is concentrated within few neurons rather than being distributed all over. This will help us repurpose the other paramaters when more classes are entered as these paramaters will get a low degree of importance by either of the above two techniques. Learning a disentangled representation is more powerful and less vulnerable to catastrophic interference. If we make neurons individually representative, then the need to overwrite and forgot past classes decreases. Changing few neurons in a tanged representation would mess up the different tasks each contributes to. 

Authors achieve this by, firsty penalising changes to important weights as last time, and local penalization of correlated weights. The paper goes into a lot of detail but I will try to put the main idea briefly : 

For an input image, we would like only a few paramaters to be active in any layer. This would corrospond to a neurons that are individually representative. Initially authors tried to penalise if more than one neuron was active in a layer but this was too harsh. We must maintain a balance of penalizing joint activations while also allowing the network enough to actually learn what it is trying to.

So they impose a soft form of this constraint that caps the number of highly activated neurons per layer. Firstly, the index of the activation maps are kept fixed(as always) and if around a neighbourhood of a neuron, say m indexes to the right and left, there is joint activation then we penalise this in the loss. So within every 2m indexes, we try to have only one activation. This limits the number of high activations to N/2m per layer where N is the number of neurons in the layer. Here m is a hyperparamter. This forces the network to have few neurons of high activation per layer any time an example is passed through, making each neuron learn a dense representation for the target. 

Here we have an interesting association with [Hebbian Learning](https://en.wikipedia.org/wiki/Hebbian_theory)in the brain. For more reading about why disentangled representation help with overfitting please see this interesting paper “Reducing Overfitting in Deep Networks by Decorrelating Representations”
