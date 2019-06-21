---
layout: post
title: Comming Soon Guessing the Central Limit Theorem
---

[
CLT:The central limit theorem states that the distribution of sample means approximates a normal distribution as the sample size gets larger (assuming that all samples are identical in size), regardless of population distribution shape.

We say the distribution of total deviations in normal. And this implies ^
]

Making the foundations of the Guassian Distribution more intuitive

Perhaps the one topic in all statistics that is as prevalent as it is shrouded in mystery. Your professors and seniors failed to explain it and great textbooks introduce by pulling it out of a magic hat. In this blog we will show why the Guassian has some very natural properties and why it is critical is describing noisy or random phonemon and observations like like the one it was discovered to understand(access? better word). We want to understand why errors are considered normally distributed in linear regression and other ML algorithms and why the mean is used as a representiative number in many cases. I hope that the connection of random errors to the normal distribution blows your mind!

Here we will take part in function finding. Narrowing down the possible functions via figuring out properties that our function must obey. Perhaps an easier way to know the prevelance of the Gaussian is to identify some key properties and once we see a situation where we must have those, we can guess its the Guassian.
I guarentee you after this( and some of your own thought) you will walk away finding the foundations of the Guassian more intuitive


First let's consider X follows a Uniform distribution from 0 to 1 or 
$X\sim U(a,b)$
$X\sim U(0,1)$

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/gaussian/uniform2.png?raw=true" width="850" height="300" >

We know the mean or the expected value of this distribution is equal to 1/2. But what does 1/2 really represent? 
 If we were to sample a few or even alot of points and take their average, there is no guarentee we would the exact expected value.
Thus the common defination of the expected value says that if we were to sample N values of $x_i's$, then in the limit as N tends to infinity the expected value would *converge*, not equal,to 1/2: 
 $lim_{N\mapsto \infty} \frac{\sum_i^Nx_i}{N}\mapsto 1/2$
 
Let's play around with this. Every point in X can be represented as how much it deviates from 1/2: $1/2 + d_i$. Points to the left have a negative deviation and the right have posistive ones.
E.g)

0.6 = 0.5 + 0.1

0.4 = 0.5 - 0.1


As the uniform is symteric around its mean you can image what the distribution of deviations would look like. The plot of the distribution of deviations $d_i$ is:

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/gaussian/uniformdeviation3.png?raw=true" width="850" height="300" >

We see some nice properties of this distribution:

1) The distribution is symettric about 0

2)I am just as likely to get +0.1 as -0.1 or -0.2 as +0.2. For every positive value there is a equal negative value that occurs with the *same probability*(Due to symettriry)

3)Clearly if I were to sum up all the points in this distribution, I would get 0 (again due to the symettry)

Let's consider a finite number of points $0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1$ from X for simplicity. What if I were to change these to our alternate representation and sum them? Let's see what happens:
$\sum x_i = \sum 0.5 - d_i$
$\sum x_i = (0.5-0.4) + (0.5-0.3) + (0.5-0.2) + (0.5-0.1) + (0.5-0) + (0.5+0.1) + (0.5+0.2)+ (0.5+0.3) + (0.5+0.4)$
$\sum x_i = 10*0.5 = 5$

With our transformation $x_i=1/2+d_i$ you can see that every $d_i$ above 0.5 would cancel with every below. 
You can imagine this same result if I were to to it for the entire distribution and not just our discrete points. All the deviations would cancel each other out and I would be left with N times 1/2. (Keep in mind here we just summing the entire distribution and sampling and summing).

From this we get our first new defination of the mean: the mean is the number around which the deviations are perfectly symetrical and cancel each other out when summed.

This is conveyed in the mean formula as well: (we will be seeing this formulae from many different angles in this blog)

$$\frac{\sum x_i}{N}=\mu$$

$$\sum x_i=N\mu$$

We got the same thing when we summed our 10 points above. In our case we did:

$\sum x_i = \sum (\mu + d_i) = \sum \mu +\sum d_i $

And then using $\sum d_i = 0$

$\sum \mu +\sum d_i = \sum \mu +0 = N\mu$

$\sum d_i$ = 0 is visually appreant in the case of summing the whole distribution, but in the case of random sampling I will not get all the deviations perfectly cancelling out. We would expect most of them to, using 2) above, but it won't be perfect. But the idea is that given a lot of obervations we would very well approximate $\sum x_i$ by $N\mu$ as we would expect all the positive and negative deviations to cancel each other out.

Simulating random points from the uniform gives me:

a=np.random.uniform(size=10)

array([0.80714911, 0.34312811, 0.51680355, 0.73050447, 0.53303526,
       0.03949276, 0.28161832, 0.46822593, 0.0068999 , 0.8281418 ])
       

np.sum(a)

4.5549992045609695

5-0.5 so the deviations in this case are 0.5..
Which in our form is:

Leading to the sum as ___ or 5 +- 
[write about sum d_i/N as the thing that is summosed to converge to 0 in the limit, swamping effect]


Let's see if idea holds for non-symetrric distributions
Consider this gamma distribution. The red and blue line mark the occourance of the mean when x=0.76 with a probability of 1.11e-07

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/gaussian/Gammadist.png?raw=true" width="850" height="300" >

Now lets see the mean subtracted version

<img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/gaussian/Gammamean.png?raw=true" width="850" height="300" >

If we sum all values of x for this distribution we do in fact get 0. Thats because there are a few large deviations to the right but many smaller deviations to the left. When we sum them, the smaller values occour with a much higher frequency so they are able to cancel the larger values. So once again, the mean is the point around which the positive and negative deviations cancel out. 

Let's rewrite the mean formulae with this insight:

$$\frac{\sum x_i}{N}=\mu$$

$$\frac{\sum (\mu + d_i)}{N}=\mu$$

$$\frac{\sum \mu +sum d_i}{N}=\mu$$

If we were taking large amount of samples we would expect the positive and negative deviations to almost cancel each other out in the long run so $sum d_i \approx 0 $

$$\frac{\sum \mu}{N} \approx \mu$$

And as $\mu$ is a constant $\sum \mu = N\mu$ giving 

$$ \ mu \approx \mu$$

This is saying taking a large number of samples, we expect the sample mean to be a very good approximate of the true mean beacuase we expect the deviations around the mean to cancel each other out. When the deviations cancel each other out, we are left with the only consistent signal in the distribution which happens to be the mean. This idea of thinking in terms of how the sample mean would deviate from the true mean will provide us critical insight into the guassian distribution. In the case of the uniform it was quite straight forward, in the case of the gamma if the sample has frequencies that concur with the true frequencies given by the analytical distribution then we expect the smaller deviations occuring in their larger frequency to cancel out the larger ones occuring in their smaller frequency leaving only the mean as a consistent source of signal in the summation term. 




[We want to reslly understand the connection between the mean and deviations so lets:]
Let's consider a binomial distribution with p,q




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

-plot expected value plot of this

- consider these +1, -1 as errors and we are not infinitely adding them


We have the case of Normal like curves for single cases of uniform and binomial. Let's get a little furthur. First, lets restate our defination of the mean. When thinking about the mean, it helps greatly to consider the pracitical reason why its invention was necessary.

Our first defination of the mean stated "the mean is the number around which the deviations are perfectly symetrical and cancel each other out". But the deviations won't always be symetrical for non-uniform distributions. 


$$\frac{\sum x_i}{N}=\mu$$

$$\sum x_i=N\mu$$

$$\sum x_i-N\mu=0$$

$$\sum (x_i-\mu)=0$$

From this we can see that the mean is the number from which all the negative deviations and positive deviations sum to 0. 

Consider the set (1,1,1,1,99). The mean here is 20.6 and the $d_i's$ are -19.6 for the ones and +78.4 for 99. If we add all the x's expressed as $x_i + d_i$ we would get 5(20.6)-4(19.60)+78.4=5(20.6)
The mean is the value from which the magnitute of deviations to the left and right sum to 0. 

The summing operation over the values leads to N$\mu$ because we expect the deviations to cancel out, the mean is the only thing that contributes to the sum. If I just told you the mean of a distribution and told you I have sampled K points, you could guess the sum of those would be K$\mu$ and you would'nt be too far off. So suppose we observe some phonemeon that is additive, like random noise. Say there are 100 sources of noise in a measurement each capable to being +-1. At any time all these act, so we can expect the net sum to be 0.

$\sum(x_i - \mu )=0$

If every x_i has the same probability but if x_i has some other distribution like there are 98% 1's and 2's and 2% 99's then sums of the deviations of 1's and 2's should cancel out the deviation of 99's.

-mention limiting case of binomail is normal

--Quote from statistical rethinking about normal


Or in other worlds : large deviations are less likely than smaller ones. 











Consider only 10 points from this distribution from simplicity
