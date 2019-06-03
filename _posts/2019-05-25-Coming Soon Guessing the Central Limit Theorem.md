---
layout: post
title: Comming Soon Guessing the Central Limit Theorem
---

Making the foundations of the Guassian Distribution more intuitive

Perhaps the one topic in all statistics that is as prevalent as it is shrouded in mystery. Your professors and seniors failed to explain it and great textbooks introduce by pulling it 
out of a magic hat. 

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

We see that this distribution is symettric about 0. I am just as likely to get +0.1 as -0.1. Not only that but for every positive value there is a equal negative value that occurs with the $same probability$(As this is the uniform)
You can imagine that if I were to sum up all the points in this distribution, I would get 0.

Consider the finite number of points 0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1 from X for simplicity.
If I were to sum these with our transformation $x_i=1/2+d_i$ you can see that every $d_i$ about 0.5 would cancel with every below. So I would be left with 10(1/2) + \sum d_i = 10(1/2)
You can imagine this same result if I were to to it for the entire distribution and not just our discrete points. All the deviations would cancel each other out and I would be left with N times 1/2 where N is the number of points sampled.

From this we get our first new defination of the mean: the mean is the number around which the deviations are perfectly symetrical and cancel each other out

This defination is very tidy for our uniform case and we will soon extend this to the case of other non-uniform distributions.
But before lets consider another simple game. This game is coin tossing and if the coin is heads I win 1$ and if tails I loss 1$
Statisitcs will tell you E(X) = (1/2)(1) + (1/2)(-1) = 0

Which is saying in the log run sum +1 -1 +1 +1 -1 +1 +1 -1 +1 +1 -1 +1 -1 ..... all +1s will cancel -1s. But if you think about it for an odd number of tosses N like 5, we are bound to not get 0. Because to get 0 we need a equal number of +1s and -1s and here that is just not possible. So in the optimal senerio that the first 4 winnings cancel each other out the last one would yield +1 or -1. However in the real world we could have got 4 heads and 1 tails also yielding +2 or maybe the other way around. What we want to argue here is that +2 is less likely than +1 and -2 is less likely than -1. Or in other worlds : large deviations are less likely than smaller ones. 











Consider only 10 points from this distribution from simplicity
