---
layout: post
title: Coming Soon: An Intuitive way to see Priors 
---

An intuitive illustration of a prior from McElreath's Statistical Rethinking and more intutions of Bayesian analysis


Bayesian inference is really just counting and comparing of possibilities

 is is the same device that Bayesian inference o ers. In order to make good inference about what actually happened, it 
 helps to consider everything that could have happened. A Bayesian analysis is a garden of forking data, in which 
 alternative sequences of events are cultivated. As we learn about what did happen, some of these alternative sequences 
 are pruned. In the end, what remains is only what is logically consistent with our knowledge.
 is approach provides a quantitative ranking of hypotheses, a ranking that is maximally conservative, given the assumptions and data that go into it.  e approach cannot guarantee a correct answer, on large world terms. But it can guarantee the best possible answer, on small world terms, that could be derived from the information fed into it.

Suppose there’s a bag, and it contains four marbles.  ese marbles come in two colors: blue and white. 
We know there are four marbles in the bag, but we don’t know how many are of each color. 

Counting:
We can think of probability operations as counting operations i.e each multiplication or addition of any distribution or function essentially is a way to recount the happenings of certain events. 

To get the prob of BWB from one we make a tree diagram of the possibilities and cont the ways our desired outcome is possible. The more ways an option has it, the higher its prob. I.e if A and B cause C, the if A can cause C in many more ways than B, observing C makes A more plausible than B. 
The way to count the Option 2 below would be 1 * 3 * 1= 3 ways
Option 3 would have : 2 * 2 * 2 = 8 ways

 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/count2.png?raw=true" width="30" height="10" >
</div>

 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/forkingdata.png?raw=true" width="550" height="466" >
    <center> First Task A</center>
</div>

Prior: So for each option, the more number of ways it makes the data observed possible, the higher its plausibility. 
Below under Prior Count are the ways BWBB would be possible for each conjecture. Now suppose we had picked our bag from 
another meta-bag. And say in that bag there were two option 2 bags. So now the total number of ways option 2 would be the source of BWBB would be 2*16 as the first bag has 16 ways and so does the second. We do this for each bag to get an updated number of ways each option makes the data possible.


So now we see the Option 3 has surpassed 4 as there are more ways it could be the source. So we would say Option 3 is most likely. The count of bags in the meta-bags is a prior. In this case it happened to be a hardened fact and not a belief but a belief would act in the same way. 

In probabilities we just divide by the total number to normalise but these are essentially doing counting operations of number with large digits as counts increase exponentially. 
