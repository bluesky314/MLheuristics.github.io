---
layout: post
title: Coming Soon Intutions from Linear Regression
---
Insights from linear regression to carry forward

---

I will not attempt to reinvent the wheel and explain linear regression analysis from scratch but rather summarise certain results
and highlight insights that one can carry forward in their study of machine learning. I will also list some references that one should
read if one does not already know the material. Understanding linearity greatly helps when dealing with the non-linear.

Geometric derivation

Here is a great set of videos for learning about linear regression and the geometric intution of OLS: https://www.youtube.com/watch?v=oWuhZuLOEFY, in fact
all of Ben's videos are great and we(atleast I) are lucky to have him on YouTube. He has made a ton of videos around the topic.

I will use his material to explain the simpler geometric derviation:

Lets say the column space of X forms some high-dimensional plane and our target vector Y does not live on that place. We want to pick a point
on the plane that is as close to Y as possible. To find this point, we drop a perpendicular line from Y to the place and this is our point.


Assumptions of OLS

Our objective for linear regression is to estimate some paramaters $\beta$ of the model which represent the importance of effect of a variable on our target.  OLS is guarentted to be the best minimum variance unbiased estimator of $\beta$ given its assumptions. 

 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Linear-reg/BLUE.png?raw=true" width="900" height="366" >
    <center> Parameter distribution</center>
</div>
 

Above we see that there is some true $\beta^p$ that exists. Now every time we sample a dataset from the population we will get a different estimate as $\hat{\beta}$. According to OLS: $E[\hat{\beta}]=\beta$ and among any other estimator it has the smallest variance, i.e it on average closer to the true value(this is called BLUE).
Our parameters or importances have to be unbiased. I.e from many samples, our procedure is able to get the true degree of importance and when its wrong it is due to random fluctuations in sampling and not due to systemic error in model definition. OLS gives us the best procedure to determine this line given the assumptions.

Here is a great list of assumptions along with examples:http://r-statistics.co/Assumptions-of-Linear-Regression.html and :https://en.wikipedia.org/wiki/Linear_regression#Assumptions

The need for these is that we not only want our model to do well, but also the importances to be reflective of real relationships. Under some conditions unimportant variables can falsely seem to be related to the target or their effects can be exaggerated or masked. 

I will just briefly touch upon a few assumptions:

Multi-colinearity: https://stats.stackexchange.com/questions/1149/is-there-an-intuitive-explanation-why-multicollinearity-is-a-problem-in-linear-r

Omitted variable bias - 
https://statisticsbyjim.com/regression/confounding-variables-bias/
Omitted variables can also create a false relation. If X1 is binary Africa or not. And Y is intelligence. It may be the case that as Africa has low education, X1 is given a negative coefficient as being from Africa is now negatively related to intelligence. But the true cause is intelligence not being from Africa. Education is correlated to Africa and Africa is falsely given a importance.

In case of single variable linear regression we can dervie the expression of the output analytically. 

The expression for the relationship between y and x is: 
$y= \beta _{0} + \beta _{1}x$

Then:
$\beta _{1}=\rho \frac{\sigma _{y}}{\sigma _{x}}$

But there is a better we express the relationship. In face, I would argue the above is the *worst* way. A more intutive way to formulate this would be :
$y= \beta _{0} + \beta _{1}(x - \bar{x})$

Where we put in the mean subtracted version of x. Now if we take summation on both sides and divide by n we get:
$\beta _{0} = \bar{y}$ 
which makes our equation

$y= \bar{y} + \beta _{1}(x - \bar{x})$

So now we are only modelling how y changes from its mean for different values of x! This is to say that there is some base value $\bar{y}$ and
all x does, is that it causes y to deviate from that base value. Not only that but the relationship is monotonic. 
And x can only do this when it deviates from its own mean! So essentially we are modelling how deviations of x from its mean affect deviations of y from its mean.
Lets bring back the analytical solution for the slope now:
$\beta _{1}=\rho \frac{\sigma _{y}}{\sigma _{x}}$

$\rho$ the corelation coefficent tells us on average how much x and y move together. If $\rho$ is 1 then for each increase in standard deviation in x,
y also increases by one standard deviation. So if x had a standard deviation of 50 and y of 100. Every time x went 50 above its mean, y would go 100
above its mean.  For 0.8 $\rho$, a 1 increase in standard deviation in x,
is expected to cause a 0.8 * $\sigma _{y}$ increases in y. So if x went 50 above we would expect y to go 100*0.8=80 above.

--img-

So corelation coefficent effectively models how one's deviation affects the other. This seems like all we would really need to get the relationship 
between x and y but what are those $\sigma _{y} and \sigma _{x}$ terms doing there then? Well, those are just scaling terms. And this brings me to my
favorite expression of the problem. As we mean subtracted x, we can write:

$y= \beta _{0} + \rho (x - \bar{x}) \frac{\sigma _{y}}{\sigma _{x}}$

which is :

$y= \beta_{0} + \rho x_{z} \sigma _{y}$

and as the intercept absorbs the mean:

$y= \bar{y} + \rho x_{z} \sigma _{y}$

$x_{z}$  - how many standard deviation x is away from its mean

$\rho$ - strength of relationship between x and y

$\sigma _{y}$ - y's standard deviation

Lets see what $\rho x_{z}$ represent: $x_{z}$ represents how much x has moved away from its standard deviation so $\rho x_{z}$ represents how much y has moved away from its standard deviation.
Then $\rho x_{z} \sigma _{y}$ represents the total magnitude change in y from its mean.
The $\sigma _{y}$ is essentially a scaling term to unnormalise our measures.

Thus we see that linear regression is modelling the relation between the variances between variables. The mean of variable and its standard deviation are only shifting and scaling factors. 



So essentially we are modelling how the variances in x affect y. 

Lets interpret this 



