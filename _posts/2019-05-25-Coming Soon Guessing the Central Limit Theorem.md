---
layout: post
title: Comming Soon Guessing the Central Limit Theorem
---

Making the foundations of the Guassian Distribution more intuitive

Perhaps the one topic in all statistics that is as prevalent as it is shrouded in mystery. Your professors and seniors failed to explain it and great textbooks introduce by pulling it out of a magic hat. In this blog we will show why the Guassian has some very natural properties and why it is critical is describing noisy or random phonemon and observations like like the one it was discovered to understand(access? better word)

Here we will take part in function finding. Narrowing down the possible functions via figuring out properties that our function must obey. Perhaps an easier way to know the prevelance of the Gaussian is to identify some key properties and once we see a situation where we must have those, we can guess its the Guassian.
I guarentee you after this( and some of your own thought) you will walk away finding the foundations of the Guassian more intuitive


First let's consider X follows a Uniform distribution from 0 to 1 or #X\simU(0,1)

-pic

We know the mean of this distribution or E(X) is equal to 1/2. But what does 1/2 represent? 
The common defination says: If we were to sample N number of $x_i's$ then in the limit of $N \mapsto \infty$:
 $\sum \frac{x_i}{N}\mapsto 1/2$
 
But let's play around with this. Every point in X can be represented as how much it deviates from 1/2: $1/2 + d_i. Points to the left have a negative deviation and the right have posistive ones. 
So 0.6=0.5 + 0.1
and 0.4=0.5-0.1

The plot of the deviations $d_i$ would look like:

We see that this distribution is symettric about 0. I am just as likely to get +0.1 as -0.1. Not only that but for every positive value there is a equal negative value that occurs with the *same probability*(As this is the uniform)
You can imagine that if I were to sum up all the points in this distribution, I would get 0.

Consider the finite number of points 0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1 from X for simplicity.
If I were to sum these with our transformation $x_i=1/2+d_i$ you can see that every $d_i$ about 0.5 would cancel with every below. So I would be left with $$10(1/2) + \sum d_i = 10(1/2)$$
You can imagine this same result if I were to to it for the entire distribution and not just our discrete points. All the deviations would cancel each other out and I would be left with N times 1/2 where N is the number of points sampled.

From this we get our first new defination of the mean: the mean is the number around which the deviations are perfectly symetrical and cancel each other out

This defination is very tidy for our uniform case and we will soon extend this to the case of other non-uniform distributions.
But before lets consider another simple game. This game is coin tossing and if the coin is heads I win 1$ and if tails I loss 1$
Statisitcs will tell you E(X) = (1/2)(1) + (1/2)(-1) = 0

Which is saying in the log run sum +1 -1 +1 +1 -1 +1 +1 -1 +1 +1 -1 +1 -1 ..... all +1s will cancel -1s. But if you think about it for an odd number of tosses N like 5, we are bound to not get 0. Because to get 0 we need a equal number of +1s and -1s and here that is just not possible. So in the optimal senerio that the first 4 winnings cancel each other out the last one would yield +1 or -1. However in the real world we could have got 4 heads and 1 tails also yielding +2 winnings or any combination. If N=100 we could have a whole host of possible winnings from +100 to -100. But +100 seems pretty rare right? I would have to get all heads for that. I bet you that's its more rare than +50. Can you think why this would be the case?

What about for smaller values? Is +3 more rare than +1? or -3 than -1? This is a good time to use some of our previous work and think about this.

What we want to argue here is that +2 is less likely than +1 and -2 is less likely than -1. The farther the winning is away from 0, the less likley it is. 

We can model a single toin coss as a Bernoulli distribution and a set of tosses as a Binomial distribution 

$X \sim  Bn(p=1/2,N)$

$P(X=x)=\binom{N}{x} p^n(1-p)^{N-x}$

$P(X=x)=\binom{N}{x} (1/2)^x(1/2)^{N-x}$

$P(X=x)=\binom{N}{x} 1/2^N$

We can plot this for different values of N and see which x's are most likley. Keep in mind x is the number of heads here. So if x=10 is most likley with N=25 it means 10 heads and 15 tails are the most likley outcome.


We see that the most likley number is N/2( remember N/2 corrosponds to the case of N/2 heads and N/2 tails and winning of 0). And values away from that becomes less and less likley. The relationship is strictly monotonic is the left and right regions. This is a key point we will exploit later. You can pause and think why this would be the case.

This is the case becuase the $\binom{N}{x}$ term is maximized in our binomial distribution at x=N/2. If you remember this term is added in the bernoulli to count the number of ways an outcome can now occour. So if N=4 the possible pairs are (1,1),(1,-1),(-1,1) and (-1,-1) but (1,-1) is the same as (-1,1) as we dont care about ordering so this gets accounted in the factor $\binom{2}{1}=2$. And this is true for large numbers as well. So the reason why N/2 is most likley or a winning of 0 is most likley is because in N tosses the number of *ways I can sum +1 and -1 to equal 0 is more than the number of ways I can use them to get any other number* and *ways I can sum +1 and -1 to equal +1 is more than the number of ways I can use them to get +2*. But anyways I hope it was already quite intutive to you from the setting of the game that a winning of 0 was most likley small winnings/losses were more likley than large winnings/losses, we have just verified this mathematically and made clear nearby cases such as +2 and +1. 

In the example of N=50, 25 corrosponds to the case of 0 winnings, 24 of 1$ loss and 26 of 1$ profit. Due to the symmetry 24 and 26 have equal likleyhood we are equally likley to loose an amount as we are to gain it. 
The plot of this would look like:[bin of N=50 but with winnings on x-axis]

-mention limiting case of binomail is normal

--Quote from statistical rethinking about normal


Or in other worlds : large deviations are less likely than smaller ones. 











Consider only 10 points from this distribution from simplicity
