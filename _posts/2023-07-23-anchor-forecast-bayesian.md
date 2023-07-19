
#

## Anchor Your Forecast the Bayesian Way

- [Introduction](#introduction)
- [The Bayesian Taste of Black Litterman](#bay)
  - [The Prior](#subparagraph1)
  - [The Investment View (Likelihood)](#subparagraph2)
  - [The Posterior](#subparagraph1)
- [The Shrinkage Perspective](#shrink)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

So, Mean Variance Optimization (MVO) is the genius foundation of almost everything built in the name of modern portfolio theory. While it can perform quite bizzare with estimation errors! 

In a previous blog ([The Conviction Pyramid of Portfolio Construction](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html)), we have discussed one trail of thought to alleviate such issue by reducing dependency on estimation of expected return. Now it's the time to turn to another trail of thought to improve our estimation on expected return.

Attaining a somewhat reliable estimate on expected return might be the most challenging task in the modern world of finance. While it is probably the reason why it is such an intersting topic. There is not one universally guaranteed or recoganized method for it. We have all the room to explore and wander. In this blog, let's start the journey with the Bayesian framework initially introduced as Black-Litterman model. 

### The Bayesian Taste of Black-Litterman <a name="bay"></a>

Essentially, we start from a neutral point and deviate away from it based on the magnitued and uncertainty around our forecast.


To counter the great volitility and unstationary embedded in security return, the model takes investors' forecast on expected returns as observations with uncertainties and further anchors it to a robust prior extracted from benchmark portfolio. Bayesian helps us to combine the prior and likelihood (investor forecast) to a more informed posterior. 
Let's delve into the details from a Bayesian perspective.

**The Bayesian Framework within Black-Litterman**

![BL](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/bl.png)


#### The Prior <a name="subparagraph1"></a>

what should this neutral point. BL's answer ...


#### The Investment View (Likelihood) <a name="subparagraph2"></a>

#### The Posterior <a name="subparagraph3"></a>


### The Shrinkage Perspective <a name="shrink"></a>


Also a shrink
WLS 
shrink on portfolio also

  

bayesian/shrink

factor model as a way to include piror information

Though not directly mentioned initially, it is no longer a secret that the famous optimization model Black-Litterman is a Bayesian model. The model takes investor views as observations with uncertainties and further combine it with prior extracted from the market portfolio in a genius way. Specifically, it provides a consistent Bayesian framework to overlay investor views on top of a neutral portfolio. Definitely worth knowing.

In this blog, we will try to delve into the Bayesian intuitions that underpin the Black-Litterman model. Upon the process of Black-Litterman from a 

https://palomar.home.ece.ust.hk/MAFS6010R_lectures/slides_shrinkage_n_BL.pdf

tau: step by step 0.01 to 0.05, 1/T or 1/T-k if unbiased


$$
\begin{aligned}
\mu &\propto exp((\mu - \pi)^T \Sigma_{\pi}^{-1} (\mu - \pi)) \\
Q|\mu, \Omega &\propto exp((Q - P\mu)^T \Omega^{-1} (Q - P\mu)) \\
\mu|Q, \Omega &\propto exp((\mu - \pi)^T \Sigma_{\pi}^{-1} (\mu - \pi)) * exp((Q - P\mu)^T \Omega^{-1} (Q - P\mu)) \\
      &\propto exp((\mu - \mu^{\star}) ^T M^{-1}(\mu - \mu^{\star}))
\end{aligned}
$$

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



  ### Reference <a name="ref"></a>
  - Black & Litterman (1991): Global Asset Allocation: combining investors views with market equilibrium
  - Idzorek (2007): A Step-By-Step Guide to Black-Litterman Model: Incorporating user-specified confidence level
  - Kolm & Ritter (2017): On the Bayesian interpretation of Black-Litterman
  - Kolm, Ritter & Simonian (2021): Black-Litterman and Beyond: The Bayesian Paradigm in Investment Management
  - Walters (2007): The Black-Litterman Model in Detail
