
#

## Anchor Your Forecast the Bayesian Way

- [Introduction](#introduction)
- [The Bayesian Taste of Black Litterman](#bay)
  - [The Prior](#subparagraph1)
  - [The Investment View (Likelihood)](#subparagraph2)
  - [The Posterior](#subparagraph3)
- [Deviate From a Neutral Point!](#dev)
- [Summary](#summary)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Mean Variance Optimization stands as the brilliant foundation of almost everything built in the name of modern portfolio theory (Dr. Markowitz, the genius behind this foundation sadly passed away last month. RIP sir). While it can perform quite peculiar confronted with estimation errors on expected return! 

In a previous blog ([The Conviction Pyramid of Portfolio Construction](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html)), we explored the trail of thought aimed at alleviating this issue by reducing our reliance on expected return estimates. While the allure of better forecasting expected returns and reaping the rewards is truly irresistible. Even a slight improvement in estimating expected returns can lead to tremendous financial rewards! Now, the time has come to delve deeper into this line of thinking and enhance our approach to estimating expected returns.

Obtaining a reliable estimate of expected returns ranks among the most formidable challenges in the modern world of finance. The volatility and ever-changing nature of security returns create a complex puzzle that hinders the task. In the meanwhile, it is probably this complexity that makes it an intriguing and captivating topic. In this ever-evolving landscape, there is no universally guaranteed or recognized method for accurate estimation, leaving us with ample room for exploration and hang out.

In this blog, let's start the journey with the Bayesian framework initially brought within the Black-Litterman model (BL). Such a framework enables us to start from a neutral point and incorporate investors' views/forecast on expected return to deviate from it.

### The Bayesian Taste of Black-Litterman <a name="bay"></a>

Looking into the ingredints of security return distribution. Covariance $$\Sigma$$ can usually be estimated from past returns in reasonable accuracy (We are generally able to maintain a volatility target based on historical data as shown in [The "maximum Diversification Frontier"](https://skybluerw.github.io/2023/06/22/The-Maximum-Diversification-Frontier.html)). While in majority cases, the expected return $$\mu$$ can not be known with reasonable certainy. What's more, an mean variance optimization is often more prone to estimtion errors in the estimate of expected return. 

$$
\begin{aligned}
r|\mu \sim N(\mu, \Sigma)
\end{aligned}
$$

For such an important but 'dangerous' exercise on forecast of expected return, we will need to grid with every bit of information we have while also account for the significant uncertainty around it. Aligning this idea, BL takes investors' original forecast on expected returns as noisy observations (essentially a partial likelihood) and further anchors it to a robust prior with the Bayes formula. In such a way, a more informed estimate anchored to the neutral prior arise in the form of posterior as shown in the chart below.


**The Bayesian Framework within Black-Litterman**

![BL](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/bl.png)


One last word before diving into details. It's definitely possible  to expand the framework to a more general probalistic expressions (I.E. [Kolm, Ritter & Simonian (2021)](https://www.pm-research.com/content/iijpormgmt/47/5/91) proposed such an expression with much less assumptions that can even incorporate views on hidden factors) while this kind of expansion generally comes with cost of tractbillity and computational burden. Let's stick to the Gaussian world with the traditional BL models in this blog. 

#### The Prior <a name="subparagraph1"></a>

Immediately you might ask. You mentioned we are starting from a neutral point for starter. What should this neutral point be? Can we trust any kind of return information to be our neutral start point if there is so much volatiltiy and unstationariness in the security return? Black & litterman's answer was yes and their choice rest upon the CAPM model. 

Under CAPM, market portfolio is the tagent portfolio containing all the information reqruied to price expected return of every security ($$E(r) - r_f=  r_f + \beta(E(r_M) - r_f)$$). With reversed optimization below we can easily turn the pricing information embedded in market weight ($$x_M$$) to its impled return ($$\pi$$). 

$$
\begin{aligned}
max_x & x^T \mu - \dfrac{1}{2}\lambda x^T\Sigma x \\
&\downarrow \\
x_M = (\lambda \Sigma)^{-1} \pi &\leftrightarrow \pi = \lambda \Sigma x_M
\end{aligned}
$$

Such an implied return is MVO consistent with the market portfolio in the sense that an optimization with this implied return would lead exactly to market portfolio. This feature makes the implied return a great neutral point especially when you are benchmarked to the market portfolio. We will stay at the market portfolio until there is strong enough evidence to deviate.

It is also worth to mention that we have other options in addition to the market portfolio. Though losing that bit of theoretical support from CAPM, we can switch to other becnmark portfolios for prior extraction. Similarly as the case of the market portfolio, we will get the prior consistent with its corresponding benchmarke portfolio. In the financial market where most portfolio managers are benchmarked to some reference portfolios, the technique is of great help.

Put the prior more formally in mathematics leads to the distribution below. The prior mean $$\pi$$ is set to be the implied return extracted from benchmark portfolio. As to the variance around the prior, a covariance matrix proportional to the unconditional covariance matrix is often used $$\Sigma_{\pi} = \tau \Sigma$$. $$\tau$$ is generally set to be $$\dfrac{1}{T}$$ or $$\dfrac{1}{T-k}$$ making $$\tau \Sigma$$ the sampling variance when we are logging the expected return via the security return.

We get our information on the expexted return from the 'conservative' side for a starting point.

$$
\begin{aligned}
\mu &\sim N(\pi, \Sigma_{\pi}) \\
\end{aligned}
$$

#### The Investment View (Likelihood) <a name="subparagraph2"></a>

With a reasonable neutral point to start with. We can now turn to the incorporation of investment views/forecast. That is how we make abnormal returns (also probably loss :) ).As I see, this is the most innovative part of the Black-Litterman model. 

The BL model takes the investment view as obersavations with uncentainties ($$\epsilon$$) and further use it as likelihood in a Bayes formula for information combination in the next step. Additionaly, they propose to express all views (absolute or relative) in linear equations with Gaussian noise, which help to expand usage in scenarios of partial views. The diagonal $$\Omega$$ measures the uncertainty around Q and is inverse to investors' confidence on the their views. Under such a paradigm, we can easily express our invesment views via modifying the design matrix P. 


$$
\begin{aligned}
Q &= P \mu + \epsilon \\
\epsilon &\sim N(0, \Omega) \\
\Omega &= \begin{pmatrix}
\omega_1 & 0 & ... & 0 \\
0 & \omega_2 & ... & 0 \\
... & ... & ... & ... \\
0 & 0 & ... & \omega_k \\
\end{pmatrix}
\end{aligned}
$$

For example, for a universe of security a, b, c. It is easy to have an absolute view on a subset of the security universe (like a and b's expected return are 5% and 10%)

$$
\begin{aligned}
\begin{pmatrix}
0.05 \\
0.1
\end{pmatrix} &=
\begin{pmatrix}
1 & 0\\
0 & 1
\end{pmatrix}
\begin{pmatrix}
\mu_1 \\
\mu_2
\end{pmatrix} + 
\begin{pmatrix}
\epsilon_1 \\
\epsilon_2
\end{pmatrix}
\end{aligned}
$$

It is also quite intuitive to incorporate a bunch of relative forecast (such as average expected return of a and b is around c's and a's expected return shold be lower than b's)

$$
\begin{aligned}
\begin{pmatrix}
0 \\
0.05
\end{pmatrix} &=
\begin{pmatrix}
0.5 & 0.5 & -1\\
-1 & 1 & 0
\end{pmatrix}
\begin{pmatrix}
\mu_1 \\
\mu_2 \\
\mu_3
\end{pmatrix} + 
\begin{pmatrix}
\epsilon_1 \\
\epsilon_2 \\
\epsilon_3
\end{pmatrix}
\end{aligned}
$$

Since $$\mu$$ and $$\Omega$$ are the only two source of randomness in the equation. Once we condition on the distribution on $$\mu$$, we can get a partial likelihood in terms of Q as shown below. 

$$
\begin{aligned}
Q|\mu &\sim N(P\mu, \Omega)
\end{aligned}
$$

This is our information on the expexted return from the 'adventurous' side. 

#### The Posterior <a name="subparagraph3"></a>

**Posterior for $$\mu$$**

With both prior ($$\mu$$) and likelihood ($$Q\|\mu$$), a more educated estimate of posterior mean is alomst there.

$$
\begin{aligned}
\mu &\propto exp((\mu - \pi)^T \Sigma_{\pi}^{-1} (\mu - \pi)) \\
Q|\mu, \Omega &\propto exp((Q - P\mu)^T \Omega^{-1} (Q - P\mu)) \\
\end{aligned}
$$

It takes the standard Bayes formular along side a few more lines of algebra to pin down the posterior for the mean return $$\mu\|Q$$.

$$
\begin{aligned}
\mu|Q, \Omega &\propto \mu * Q|\mu, \Omega \\
\mu|Q, \Omega &\propto exp((\mu - \pi)^T \Sigma_{\pi}^{-1} (\mu - \pi)) * exp((Q - P\mu)^T \Omega^{-1} (Q - P\mu)) \\
      &\propto exp((\mu - \mu^{\star}) ^T M^{-1}(\mu - \mu^{\star})) \\
\mu^{\star} &= ((\Sigma_{\pi})^{-1} + P^T\Omega^{-1}P)^{-1}((\Sigma_{\pi})^{-1} \pi + P^T\Omega^{-1}Q) \\
M &= ((\Sigma_{\pi})^{-1} + P^T\Omega^{-1}P)^{-1} \\
&\downarrow \\
\mu|Q, \Omega &\sim N(\mu^{\star}, M)
\end{aligned}
$$

**Posterior for r**

With the new BL estimate of $$\mu$$, we can finally circle back to the return distribution, which we cares most. 

$$
\begin{aligned}
r|Q, \Omega &\propto r|\mu * \mu|Q, \Omega\\
&\downarrow \\
r|Q, \Omega &\sim N(\mu^{\star}, \Sigma + M) \\
\end{aligned}
$$

Compared to the original $$r\|\mu \sim N(\mu, \Sigma_{\pi})$$, we replace the true $$\mu$$ with our estimation $$\mu^{\star}$$. Simultaneously, the variance increased to $$\Sigma + M$$ accounting for our forecast on expected return as well. 


### Deviate From a Neutral Point! <a name="dev"></a>

With all the work up to the point, what do we finally get? Is it consistent with the idea of deviating from a neutral point based on investment views as allerged? It would become much clearer after a few more algebra transformations. 

$$
\begin{aligned}
\mu^{\star} &= \pi + \Sigma_{\pi}P^T(\Omega + P\Sigma_{\pi}P^T)^{-1} (Q-P\pi) \\
\end{aligned}
$$

The BL estimation $$\mu^{\star}$$ can also be represented as the summation of prior mean return and an adjustment term accounting for investors' view to take active risk. $$(Q-P\pi)$$ is simply the difference between investors' view and prior mean. The difference is further scaled by a ratio roughly in the form of $$\dfrac{Prior Variance}{Investment View Variance + Prior Variance}$$ adjusted to the return space.

Quite clearly, two factors jointly decide the magnitude of our deviation. Other than the difference between prior mean and investment view, the comparison between prior variance and investment view variance also play a critical part. In an extreme case of infinity variance on investment view or zero variance on prior, the BL estimation is exactly the prior mean estimation. Starting from this point, as variance on prior becomes larger compared to variance on investment view, the BL estimation gradually move torward to a blend with higher emphasis on investors' views. This is an estimation error awared forecast!


**The Shrinkage Perspective**

Another representation providing great intuition can be gained from the shrinkage perspective as well. The BL estimation $$\mu^{\star}$$ can be decomposed into weighted average of prior mean and the return mean estimation implied from investment views $$P\mu_{view} = Q$$. Though $$\mu_{view}$$ is not uniquely defined in case of partial investment views (P is not invertible in the case), it does not hinder us from using it for further intuitions.

As shown below the summation of the two weights equal to an identity matrix ($$  W_0 + W_{view} = I $$). The BL estimation lies between the the prior mean and mean forecast from investment views. 


$$
\begin{aligned}
\mu^{\star} &= ((\Sigma_{\pi})^{-1} + P^T\Omega^{-1}P)^{-1}((\Sigma_{\pi})^{-1} \pi + P^T\Omega^{-1}Q) \\
 &= ((\Sigma_{\pi})^{-1} + P^T\Omega^{-1}P)^{-1}((\Sigma_{\pi})^{-1} \pi + P^T\Omega^{-1}P\mu_{view}) \\
 &= W_0 \pi + W_{view} \mu_{view} \\
 W_0 &= ((\Sigma_{\pi})^{-1} + P^T\Omega^{-1}P)^{-1} (\Sigma_{\pi})^{-1} \\
 W_{view} &= ((\Sigma_{\pi})^{-1} + P^T\Omega^{-1}P)^{-1} P^T\Omega^{-1}P \\
  W_0 + W_{view} &= I 
\end{aligned}
$$

What is amazing is that such an BL estimation can be obtained from a Weighted Least Square (WLS) regression as below. 

$$
\begin{aligned}
\begin{pmatrix}
\pi \\
Q 
\end{pmatrix} &= \begin{pmatrix}
I\\
P
\end{pmatrix}\mu + e \\
e &\thicksim N(0, \begin{pmatrix}
\Sigma_{\pi} & 0 \\
0 & \Omega
\end{pmatrix})
\end{aligned}
$$

In such setting, both prior and investment views are taken as noisy obversations. We count on a WLS to get new estimation on expected return based on all such information. 


### Summary <a name="summary"></a>

In the blog we have discussed the BL model from the Bayesian angle. I hope you find it a useful tool for expected return estimation as me. The BL model is particularly suit for this task. Looking into the challenges arised from wild estimation error on forecast of expected return. BL provided a way to anchor it to implied return from benchmark. From a investment product perspective, there can hardly any much neutral or safe point as this return. As most if not all portfolio managers are benchmarked to some portfolio (Even hedge fund should be benchmarked to case or zero portfolio?). Even with this anchor, we still need to evaluate the uncertainty around our estimate. The Bayesian framework within the BL model is definitly good for that purpose as well.

### Reference <a name="ref"></a>
  
  - Black & Litterman (1991): Global Asset Allocation: combining investors views with market equilibrium
  - Idzorek (2007): A Step-By-Step Guide to Black-Litterman Model: Incorporating user-specified confidence level
  - Kolm & Ritter (2017): On the Bayesian interpretation of Black-Litterman
  - Kolm, Ritter & Simonian (2021): Black-Litterman and Beyond: The Bayesian Paradigm in Investment Management
  - Walters (2007): The Black-Litterman Model in Detail
