
#

## Anchor Your Forecast the Bayesian Way

- [Introduction](#introduction)
- [The Bayesian Taste of Black Litterman](#bay)
  - [The Prior](#subparagraph1)
  - [The Investment View (Likelihood)](#subparagraph2)
  - [The Posterior](#subparagraph3)
- [Deviating From a Neutral Point!](#dev)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

Mean Variance Optimization is the genius foundation of almost everything built in the name of modern portfolio theory (Dr. Markowitz passed away last month. RIP sir). While it can perform quite bizzare with estimation errors on expected returns! 

In a previous blog ([The Conviction Pyramid of Portfolio Construction](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html)), we have discussed one trail of thought to alleviate such issue by reducing dependency on estimation of expected return. Now it's the time to turn to another trail of thought to improve our estimation on expected return.

Attaining a reliable estimate on expected return is probably the most challenging task in the modern world of finance, which is also exactly the point making it a quite interesting topic. There is no universally guaranteed or recoganized method for it. We have all the room to explore and wander. 

In this blog, let's start the journey with the Bayesian framework initially brought within the Black-Litterman model (BL). Such a framework enables us to start from a neutral point and deviate away based on the magnitued and uncertainty around our forecast.

### The Bayesian Taste of Black-Litterman <a name="bay"></a>

To work with the volatile and often unstationary security return, BL takes investors' original forecast on expected returns as observations with uncertainties (likelihood) and further anchors it to a robust prior with the Bayes formula. In such a way, a more informed estimate anchored to the prior arise in the form of posterior as shown in the chart below.


**The Bayesian Framework within Black-Litterman**

![BL](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/bl.png)


#### The Prior <a name="subparagraph1"></a>

Immediately you might ask. What should this neutral point be? Can we trust any kind of return information to be our neutral start point if there is so much volatiltiy and unstationariness in the security return? Black & litterman's answer was yes and their choice rest upon the CAPM model. 

Under CAPM, market portfolio is the tagent portfolio containing all the information reqruied to price expected return of every security ($$E(r) - r_f=  r_f + \beta(E(r_M) - r_f)$$). with the reversed optimization below we can easily turn the insight embedded market weight ($$x_M$$) to its impled return ($$\pi$$). 

$$
\begin{aligned}
max_x & x^T \mu - \dfrac{1}{2}\lambda x^T\Sigma x \\
&\downarrow \\
x_M = (\lambda \Sigma)^{-1} \pi &\leftrightarrow \pi = \lambda \Sigma x_M
\end{aligned}
$$

Such an implied return is MVO consistent with the market portfolio in the sense that an optimization with the implied return would lead exactly to the market portfolio. This feature makes the implied return a great neutral point especially when you are benchmarked to the market portfolio as we will stay at the market portfolio until there is a strong enough expected return forecast to make us deviate. 

It is also worth to mention that we have other options in addition to the market portfolio. Though losing that bit of theoretical support from CAPM, we can switch to other becnmark portfolios for prior extraction maintaining the idea. Similarly as the case of the market portfolio, we will get the prior consistent with its corresponding benchmarke portfolio. In the financial market where most portfolio managers are benchmarked to some portfolio, the technique is of great help.

Put the prior more formally in mathematics leads to the distribution below. The mean of the distribution is set to be the implied return extracted from benchmark portfolio. As to the variance around the prior, a matrix proportional to the unconditional covariance matrix is often used $$\Sigma_{\pi} = \tau \Sigma$$. $$\tau$$ is generally set to be $$\dfrac{1}{T}$$ or $$\dfrac{1}{T-k}$$ making $$\tau \Sigma$$ the sampling variance when we are observing the mean via the security return.

$$
\begin{aligned}
\mu &\sim N(\pi, \Sigma_{\pi}) \\
\end{aligned}
$$

#### The Investment View (Likelihood) <a name="subparagraph2"></a>

With a reasonable neutral point to start with. We can now turn to the incorporation of investment views/forecast. As I see, this is the most innovative part of the Black-Litterman model. 

The BL model takes the investment view as obersavations with uncentainties ($$\epsilon$$) and further use it as likelihood in a Bayes formula for the next step. Additionaly, they propose to express all views (absolute or relative) in linear equations with Gaussian noise. The diagonal $$\Omega$$ measures the uncertainty around Q and is inverse to investors' confidence on the their views.Under such a paradigm, we can easily express our invesment views via modifying the design matrix P. 

It's definitely possible to expand it to more general probalistic expressions (I.E. [Kolm, Ritter & Simonian (2021)](https://www.pm-research.com/content/iijpormgmt/47/5/91) proposed such an expression that can incorporate views on hidden factors) while that generally comes with cost of tractbillity and computational burden.

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

Back to the traditional linear expression! It is easy to have an absolute view on a subset of the security universe (a and b's expected return are 5% and 10%)

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

It is also quite intuitive to incorporate a bunch of relative forecast such as average expected return of a and b is around c's. a's expected return shold be lower than b's

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

Since $$\mu$$ and $$\Omega$$ are the only two source of randomness in the equation. Once we condition the distribution on $$\mu$$, we can have a likelihood in terms of investment Q as shown below. 

$$
\begin{aligned}
Q|\mu &\sim N(P\mu, \Omega)
\end{aligned}
$$

#### The Posterior <a name="subparagraph3"></a>

**Posterio for $$\mu$$**

Now we have both prior ($$\mu$$) and likelihood and likelihood ($$Q\|\mu$$)

$$
\begin{aligned}
\mu &\propto exp((\mu - \pi)^T \Sigma_{\pi}^{-1} (\mu - \pi)) \\
Q|\mu, \Omega &\propto exp((Q - P\mu)^T \Omega^{-1} (Q - P\mu)) \\
\end{aligned}
$$

It takes just a few lines of algebra to pin down the posterior for the expected return $$\mu\|Q$$. The posterior is conditional on our expected return forecast combined from the prior.

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

**Posterio for r**

What we really need in practice is actually the posterior for the return  $$r\|Q, \Omega$$, which is not also easily available.

$$
\begin{aligned}
r|Q, \Omega &\sim N(\mu^{\star}, \Sigma + M)
\end{aligned}
$$



### Deviating From a Neutral Point! <a name="dev"></a>

$$
\begin{aligned}
\mu^{\star} &= \pi + \Sigma_{\pi}P^T(\Omega + P\Sigma_{\pi}P^T)^{-1} (Q-P\pi) \\
\Sigma + M &= (\Sigma + \Sigma_{\pi}) - \Sigma_{\pi} P^T (\Omega + P\Sigma_{\pi}P^T)^{-1}P\Sigma_{\pi}
\end{aligned}
$$


Also a shrink
WLS 
shrink on portfolio also



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

regression, adding restriction

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



  ### Reference <a name="ref"></a>
  - Black & Litterman (1991): Global Asset Allocation: combining investors views with market equilibrium
  - Idzorek (2007): A Step-By-Step Guide to Black-Litterman Model: Incorporating user-specified confidence level
  - Kolm & Ritter (2017): On the Bayesian interpretation of Black-Litterman
  - Kolm, Ritter & Simonian (2021): Black-Litterman and Beyond: The Bayesian Paradigm in Investment Management
  - Walters (2007): The Black-Litterman Model in Detail
