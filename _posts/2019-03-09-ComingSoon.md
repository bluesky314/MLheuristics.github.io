---
layout: post
title: Coming Soon
---
Blogpost on 3 recent continual learning covering :

Overcoming catastrophic forgetting problem by weight consolidation and long-term memory : https://arxiv.org/abs/1805.07441

Memory Aware Synapses - Learning what (not) to forget : https://arxiv.org/abs/1711.09601

Selfless Sequential Learning: https://arxiv.org/abs/1806.05421
 

---

We humans are able to continually learn from experience and improve our performance on a task even if the information we learn from is spaced out in time or some of it is never shown again to us. Like when we learnt the english language, we no longer have to revise the rules of grammer as they have become solidified into our memory and we just keep learning more semantically complex words/phrases as we grow.(Link to second paper) We would like our neural networks to engage in such a learning process as well where its learning is compounding continually. However, the key of this process is that we must not forget what we learnt before. And this is where neural networks are know to fail. Usually, we deploy our neural network and freeze its weights. But if we did'nt freeze them and made them able to learn from new data out in the field, the network would learn the new information but would start erasing what it learnt before by overwritting the weights. This is what is called 'catostopic forgetting'. 


Continual Learning is the task of continuing the learning process in neural networks even when the data it was intially trained on is no longer available.
taskA,taskB

 
 Our network tries to learn some optimal weights $\theta$. $\theta$ lives in some N-dimensional space where N is the number of parameters in the model. Now in this space we know that they are multiple $\theta$s that would give us a similar loss. The larger we make the space of $\theta$s i.e N, the more number of optimal $\theta$'s there will be. Simply because I can take any optimal $\theta$ from the smaller space, and arrange it in many more ways in this larger space. We shall see a illustration of this below.  there are  $\theta_A^*$
 
Think of weights as dimensions.

Let us consider a system of only two weights for simlicity. Lets say that we have two tasks A and B. A's optimal weights are (2,2) and B's are (8,10). Now if I merge dataset A and B and try to learn (2,2) and (8,10) at the same time I would end up at around the average of the two (5,6) as that minimizes the average loss. Now say, I add two more weights to my model. If my first two weights learn (2,2), the third and fourth can learn (8,10) (this is not exactly how it would happen but enough to get the basic idea). So the two extra dimensions, gives the network more freedom to accomidate both representations. The fact that representation power increases as number of parameters increase is no suprise but key point here is how that is related to the networks inclination to erase representations it has previously learnt. In the first example it would **have to** erase what was learnt and in the second it **may not**. 
 
 Now consider if I was training them in sequence.
 If I had only two weights and were to train on A first and then on B, the my weights would change from (2,2) to (8,10). But what if were to add two weights now and continue trainning? In that case, the network has no incentive to keep the earlier weights as the new gradients are calculated for all and the neurons will be repourposed altering the earlier representation learnt. These neurons are repourposed even though there is enough space to accomidate the new representations. And if the optimal weights were (8,10) then for four it would be (4,4,6,2) or such as the network is forced to learn a **distributed representation** vs a compact one by design.

The two problems listed here are what the three papers hope to tackle:
1) Knowing which weights are important and which to change
2) learning a more compact representation if possible


 ## Elastic weight consolidation
The following theoretical explanation is not vital to understanding the ... but is good to know. 
It's important to understand what training a network means from a probabilistic perspective. Supposing we have some data $\mathcal{D}$, we'd like to find the most probable parameters given the data, which is expressed as $p(\theta | \mathcal{D})$. What does this mean in our context? Lets say there was only one optimal solution $\Theta _{1}$ then $p(\theta = \Theta _{1} | \mathcal{D}) =1 $ <b> as every time we train our network we would converge to the same weights.

Now say there were multiple optimas, $\Theta _{1}$ ..... $\Theta _{k}$. <b> Some of these would be more probabal that others due th factors like our initialization and how easily they are accessible in weight space. Unfeasible weights will have a probability of 0 given D.


We can calculate this conditional probability using Bayes' rule:

Bayes theorem states:
 $
 \begin{align}
 p(\theta | \mathcal{D}) &= \frac{p(\mathcal{D} | \theta) p(\theta)}{p(\mathcal{D})}
 \end{align}
 $
 
After we train on task A, the distribution of the weights will follow $p(\theta | \mathcal{D})$. This becomes our new initilization for task B (just as in the simplier cases above)
$
\begin{align}
\log p(\theta | \mathcal{D}) &= \log p(\mathcal{D}_B | \theta) + \log p(\theta | \mathcal{D}_A) - \log p(\mathcal{D}_B)\\
\end{align}
$

The left side gives us the distribution of theta of training task A and then B. All the information learned when solving task A is contained in the conditional probability 

#theta|D_a

This conditional probability can tell us which parameters are important in solving task A.

   
Tell us the the weights thetaB will reach are influenced by thetaA. I.e the network is more likely to setlle on weights closer to thetaA in weight space. However, the abstract representations learnt are very sensitive to magnitude changes to the weights, esepecillay given that all the weights are changing. So even though we have a natural inclination to end up closer to thetaA in weight space, it is still too far in representation space.  

Next, what is Mackay's work on Laplace approximation and how is it relevant here? I skimmed the paper and this is what I suspect is the answer. 

Rather than numerically approximating the posterior distribituion, we model it as a multivariate normal distribution using $\theta_A^*$  as the means. What about the variance? We're going to specify the variance for each variable as <a href="https://en.wikipedia.org/wiki/Precision_(statistics)">precision</a>, the reciprocal of the variance. 
 Why is this? 
 Let $\theta_A_ijk^*$ be the i'th layer, j'th neuron and k'th weight. 
 Let's take two gaussians having the same mean. Each reprenting two of the ijk'th weights. If a weight is very important, it will have low variance, i.e the network will not continually alter it or pull it rapidy back when it does. A weight with higher variance means that there are more multiple suitable values for the weight. Thus the variance can be used to measure the importance of the weight. Weights with high importance have low variance and vice versa.
 
 
The Fisher information matrix $F$. <a href="https://en.wikipedia.org/wiki/Fisher_information">Fisher information</a> is "a way of measuring the amout of information that an observable random variable X carries about an unknown parameter $\theta$ upon which the probability of X depends." This is very close to the inverse variance of $\theta$ . The Fisher information matrix is much more feasible to calculate than numerical approximation, which makes it a useful tool.

$
\begin{align}
\mathcal{L}(\theta) = \mathcal{L}_B(\theta) + \sum\limits_{i} \frac{\lambda}{2} F_i (\theta_i - \theta_{A,i}^*)^2
\end{align}
$


 ## Memory Aware Synapses

The approach here is different by one key aspect put sucillently in the paper as "Like other model-based approaches,
we estimate an importance weight for each parameter in the network. Yet in our case,
these importance weights approximate the sensitivity of the learned function to a param-
eter change rather than a measure of the (inverse of) parameter uncertainty, as in [12], or
the sensitivity of the loss to a parameter change, as in [39] (see Figure 2). As it does not
depend on the ground truth labels, our approach allows computing the importance us-
ing any available data (unlabeled) which in turn allows for an adaptation to user-specific
settings."

Our model is the function F that maps $x_{i}$ to $y_{i}$ by $F(x_{i}) = y_{i}$ . The importance of any one weight can be measured by how much changing it will change the output. This is nothing by the derivative of F with respect to $\theta_{ijk}$

g_{ijk}=\frac{\partial F(x)}{\partial \theta_{ijk}}

To get the importance of very parameter, we take the average of its derivative over the entire dataset:

\Omega _{ijk} = \frac{1}{N} \sum_{D=1}^{N} g_{ijk}(x_{D} )

This represents the average importance of each parameter. The higher \Omega _{ijk} is the higher the importance of that parameter.

-- squared form

Now when task B has to be learnt we have an addition to the loss, a regularizer that penalizes changes to parameters that are deemed important for previous tasks:

L_{B}= Loss +  \lambda\sum\limits_{ij}\Omega_{ij}(\Theta_{ij}-\Theta_{ij}^{*})^{2}

Where Loss is the general loss function we are using and the second is our new regularization term.
