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

 ## Elastic weight consolidation
 
 Our network tries to learn some optimal weights $\theta$. $\theta$ lives in some N-dimensional space where N is the number of parameters in the model. Now in this space we know that they are multiple $\theta$s that would give us a similar loss. The larger we make the space of $\theta$s i.e N, the more number of optimal $\theta$'s there will be. Simply because I can take any optimal $\theta$ from the smaller space, and arrange it in many more ways in this larger space. We shall see a illustration of this below.  there are  $\theta_A^*$
 
 Let us consider a system of only two weights for simlicity. Lets say that we have two tasks A and B. A's optimal weights are (1,1) and B's are (1,9). Now if I try to learn (1,1) and (1,9) at the same time, I would end up at (1,4.5) to minimize the average loss. Now say, I add one more weight. Now if my first two weights learn (1,1) my third one can learn (9). So the one extra dimension, gives the network more freedom to accomidate both learnings. The fact that representation power increases as number of parameters increase is no suprise but key point here is how that is related to the networks inclination to erase representations it has previously learnt. 
 
 If I were to train on A before and then only on B after, the my weights would change from (1,1) to (1,9) in the first case. But what about the second? In that case as well, as the network has no incentive to keep (1,1) it would simply erase it even though it could have 
