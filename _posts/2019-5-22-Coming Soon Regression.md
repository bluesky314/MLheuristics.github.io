---
layout: post
title: Coming Soon Intutions from Linear Regression
---
Insights from linear regression to carry forward

---
$Y=\beta_{0}+\beta_{1} X+\epsilon$
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
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Linear-reg/BLUE.png?raw=true" width="450" height="366" >
    <center> Parameter distribution</center>
</div>
 

Above we see that there is some true $\beta^p$ that exists. Now every time we sample a dataset from the population we will get a different estimate as $\hat{\beta}$. According to OLS: $E[\hat{\beta}]=\beta$ and among any other estimator it has the smallest variance, i.e it on average closer to the true value(this is called BLUE).
Our parameters or importances have to be unbiased. I.e from many samples, our procedure is able to get the true degree of importance and when its wrong it is due to random fluctuations in sampling and not due to systemic error in model definition. OLS gives us the best procedure to determine this line given the assumptions.

Here is a great list of assumptions along with examples:http://r-statistics.co/Assumptions-of-Linear-Regression.html and :https://en.wikipedia.org/wiki/Linear_regression#Assumptions

The need for these is that we not only want our model to do well, but also the importances to be reflective of real relationships. Under some conditions unimportant variables can falsely seem to be related to the target or their effects can be exaggerated or masked. 

I will just briefly touch upon a few assumptions:

Multi-colinearity: https://stats.stackexchange.com/questions/1149/is-there-an-intuitive-explanation-why-multicollinearity-is-a-problem-in-linear-r

When two variables co-occur very frequently, it is difficult to disentangle one's effects from the other. Remember we want a regression model where the paramater estimates represent true relationships in the real world. Multi-colinearity leads to the case where our output Y is stable and optimal but the paramter estimates are incorrect. This leads to incorrect inferences about the effects of the variables.

Say each of X1 and X2 has some information about Y. The more correlated X1 and X2 are with each other, the more the information content about Y from X1 and X2 are similar or overlapping, to the point that for perfectly correlated X1 and X2, it really is the same information content. If we now put X1 and X2 in the same regression model to explain Y, the model tries to "apportion" the information that (X1,X2) contains about Y to each of X1 and X2, in a somewhat arbitrary manner. There is no really good way to apportion this, since any split of the information still leads to keeping the total information from (X1,X2) in the mode.

Imagine we have two vectors pointing in almost the same direction with some small angle between them. To get to a far away point I could use one alot and add a tiny bit of the other or vice versa or use approximately half of each. As there are multiple ways to reach our point, how much of each to take is not clear.


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

## Hypothesis Testing

$$\hat{\beta}_{1}=\frac{Cov(X,Y)}{S_{xx}}$$


$$\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)y_{i}}{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)^{2}}$$

Now $y_{i}$ can be written in terms of the true parameters we are trying to approximatate: Now $$y_{i} = \beta_{0}^p+\beta_{1}^p x_i+\epsilon$$ This is a very critical step as we now connect the true paramaters with our estimated ones.

So 

$$\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)(\beta_{0}^p+\beta_{1}^p x_i+\epsilon_i)}{S_{xx}}$$


$$\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)(\beta_{1}^p x_i)+\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\epsilon_i}{S_{xx}}$$


$$\hat{\beta}_{1}=\frac{S_{xx}\beta_{1}^p+\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\epsilon_i}{S_{xx}}$$


$$\hat{\beta}_{1}=\beta_{1}^p+\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\epsilon_i}{S_{xx}}$$

We want the variance in $\beta$ as that gives us a measure of uncertainty over our regressed value.

$$V(\hat{\beta}_{1})=V(\beta_{1}^p)+V(\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\epsilon_i}{S_{xx}})$$


$$V(\hat{\beta}_{1})=\frac{1}{S_{xx}^2}V(\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\epsilon_i)$$


$$V(\hat{\beta}_{1})=\frac{1}{S_{xx}^2}\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)^2V(\epsilon_i)$$

$$V(\hat{\beta}_{1})=\frac{1}{S_{xx}}V(\epsilon_i)$$

This expression is quite insightful. It says that the only reason our estimated $\beta$ varies is due to $V(\epsilon_i)$ being non-zero. I.e the reason why we get different estimates for $\beta$ from samples in the population is due the presence of random noise. Each sample has a different amount of noise which shifts our estimates. We also see that a way todecrease the variance in our estimate is the increase the variance in our $x$ values i.e take samples from a wide range. 
 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Linear-reg/noiseline.jpg?raw=true" width="450" height="366" >
    <center> Parameter distribution</center>
 
</div>
 <div id="container">
    <img src="https://github.com/bluesky314/bluesky314.github.io/blob/master/images/Linear-reg/staightline.jpg?raw=true" width="450" height="366" >
    <center> Parameter distribution</center>
</div>
From the first graph we see that no matter what chuck on x values we take we will get the exact same slope. But in the second, due the uneven presence of noise, we will get slightly different values of the slope. The presence of noise is the fundamanetal cause of uncertainty in paramaters.


We assume $\beta$ follows a normal distribution as $$\hat{\beta}_{1}\sim N(\beta_{1}^p,V(\hat{\beta}_{1}))$$
As we only have one sample we do not know $$V(\hat{\beta}_{1})$$, to adjust for our ignorance we will do two things:

1) Use the sample variance of residuals to approximate $$V(\epsilon_i)$$ 

So $$V(\hat{\beta}_{1})\approx \frac{1}{S_{xx}}\frac{\sum \epsilon^{2}_i}{N}$$

2) Instead of using the normal distribution, we will use the t-distribution which is much wider and accounts for more uncertainty

--t dist img---

We then conduct our hypothesis test regularly with 
See how standard error of different B1,2,3 come into play




\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)(\beta_{0}^p+\beta_{1}^p x_i+\epsilon_i)}{S_{xx}}

\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)(\beta_{1}^p x_i)+\sum_{i=1}^{n}\left(x_{i}-\overline{x}\right)\epsilon_i}{S_{xx}}
