---
layout: post
title: Intutions from Linear Regression
---
Insights from linear regression to carry forward

---

I will not attempt to reinvent the wheel and explain linear regression analysis from scratch but rather summarise certain results
and highlight insights that one can carry forward in their study of machine learning. I will also list some references that one should
read if one does not already know the material. Understanding linearity greatly helps when dealing with the non-linear.

Geometric derivation

Here is a great set of videos for learning about linear regression and the geometric intution of OLS: https://www.youtube.com/watch?v=oWuhZuLOEFY, in fact
all of Ben's videos are great and we are lucky to have him on YouTube. He has made a ton of videos around the topic.

I will use his material to explain the simpler geometric derviation:

Lets say the column space of X forms some high-dimensional plane and our target vector Y does not live on that place. We want to pick a point
on the plane that is as close to Y as possible. To find this point, we drop a perpendicular line from Y to the place and this is our point.


Assumptions of OLS

Here is a great list of assumptions along with examples:http://r-statistics.co/Assumptions-of-Linear-Regression.html


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

$y= \beta _{0} + \rho (x - \bar{x}) \frac{\sigma _{y}}{\sigma _{x}$

$y= \bar{y} + \rho x_{z} \sigma _{y}$

x_{z}  - how many standard deviation x is away from its mean
\rho - strength of relationship between x and y
\sigma _{y} - y's standard deviation

So lets intrepret this symbol for symbol. We are saying y equals $\bar{y}$ plus the how much x has deviated times $\rho$ 

So essentially we are modelling how the variances in x affect y. 

Lets interpret this 



