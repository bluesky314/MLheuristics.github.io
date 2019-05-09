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

 $
 \begin{align}
 p(\theta | \mathcal{D}) &= \frac{p(\mathcal{D} | \theta) p(\theta)}{p(\mathcal{D})}
 \end{align}
 $
 
Tell us the the weights thetaB will reach are influenced by thetaA. I.e the network is more likely to setlle on weights closer to thetaA in weight space. However, the abstract representations learnt are very sensitive to magnitude changes to the weights, esepecillay given that all the weights are changing. So even though we have a natural inclination to end up closer to thetaA in weight space, it is still too far in representation space.  

