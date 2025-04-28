## Navigating the Factor Zoo!

- [From Factors to Managed Portfolios](#portfolio)
- [The Bayesian Len](#bayes)
- [Reference](#ref)

In our previous blog [A First Glimpse into the "Factor Zoo"](https://skybluerw.github.io/2024/12/07/factor-zoo.html), we took a bird's eye view of the general empirical results of hudreds for hundres of factors in the "Factor Zoo" and saw how different (or even contradictory) conclusions can emerge from them. Despite the lingering debates over replication issues in empirical asset pricing research, it's time to step closer and zoom in on the inner workings of modeling and evaluating of these factors.

As we saw in our Factor Zoo survey, the central question in empirical factor research is often: "Is this factor's alpha statistically different from zero, and is it economically meaningful?". Traditionally, researchers address this by examing a factor's expected return and variance, reflecting asset pricing theory's emphasis on covariates and their first two moments as well as for their nice analytical properties. 

It is true that it's not always the case. For example, investors during their investment exercise would definitely appreciate a more comprehensive picture of the return distribution for features like higher moments, tail behavior, invariant parameters and so one. Every extra insight can translate into an investment edge. While regardless of whether mean and variance generalize well for the performance of a factor, a clear, explicitely stated process for factor modeling and evaluatioin delivers value from every aspect. 


This question is typically addressed by examing a factor's expected return and variance, reflecting the emphasis on covariates and their first two moments in the theory of asset pricing. It is true that it is not always the case. For example investors in their investing exercise would definitely appreciate a more comprehensive picture of the return distribution like higher moments, tail behavior, invariant parameters. While regardless of the end goal, a clear and explicitely stated framework for factor modeling and evaluation benefits in all aspects.




The central question in empirical asset pricing is generally: "Is this factor's alpha statistically different from zeor, and is it economically meaningful?". As demonstrated in the two survey papers in the previous blog, this question is typically address by examing a factor's expected return and variance, which reflect and originates from the emphasis on covariates and their first two moments in theoretical asset pricing. 

The central question in empricial factor research is usually: "Is this factor's alpha statistically differnt from zero, and is it economically meaningful?". Guided by the theory of asset pricing, which focus heavily on covariates and their first two moments. This questions is usually answered around the expected return and variance of the performance of a factor. As investors investing in real world, we definitely appreciate any further information about the distribution in addition to the two, since every additional insights, potentially translate into an investment edge. No matter what's the end goal, both academics and practitioners can benefit from a clear statement about the modeling and evaluation.

Obviously, The goal does not align exactly for factor researchs in acadmia and in industry. To serve investment exercise, we look for more than a "yes or no" answer that hypothesis testing seeks in academic research. Rather, we look to learn as much as possible of the distribution of the factor performance, where any bit of additional information enhance the edge in investment. But those spirites of modeling originated from insights of the market are universal. 

In this blog, we turn our attention to the modeling and evaluation bits of the "factor zoo". We will start with the a more frequentist flavor with all the classic methods in empirical asset pricing for factor evaluation and march toward the Bayesian framework that Jesen, Kelly & Pedersen (2023) used, which provides greater flexibility to impose structures in modeling.

Even under the current context of more and more shifting of research paradigm from traditional econometric methods to machine learning techniques, such insights expressed as model structures can be quite helpful and likely necessary considering the limited size of sample available in the financial market, their fastly hiking dimensions and troubling natures of low signal to noise ratio.

### From Factors to Managed Portfolios <a name="portfolio"></a>

The naturally question following is probably - what's exactly a "factor"?

When we say a factor helps to predict expected return, we actually declare some co-movements of security returns identified and measured. While unfortunately, though these kinds of co-movements can originate from a variety of causes like economic growth, geopolitical status, consumption, demand, investor sentiment... They are generally abstract concept that can hardly be defined and measured precisely and timely. For example, every body knows investor sentiment play a huge role in securities' returns. Market roar when investors feel good and become vulnerable when permistism spreads. While no one can define excatly what's the equation for sentiment and how to measure it reasonably, which makes all the following efforts like estimating the sensitivity of volatile security returns on the not well defined factor quite meaningless.

Luckily, there is a way to dodge around it. Rather than defining and measuring the factor exactly and directly, researchers cleverly announce that only the part of factors that is relevant with the financial market - a projection of the factor onto the payoff space of securities is all investors care. A factor can have much more meaning beyond financial market in all kinds of aspects, while as long as financial market is the only focus, there is not a reason stopping us from building a managed portfolio of securities - the building block of financial market, to measure the financial aspect of that factor. Now things become much easier, we turn the problem from precisely define and measure an abstract concept of factor to find out a managed portfolio whose performance proxy the financial aspect of the factor. Quite naturally, investors start from security characteristics seen relevant with its sensitivity to such factor and take it for the construction of the managed portfolio. 

Traditionally, such managed portfolios are obtained via the construction of long short portfolios based on security characterstics. There are a lot of pieces and dots in their construction: whether we are doing this by sorting, whether the sorting should be conditional on some other characteristics for their control, or even whether regression is a better mean than sorting. Despite all the details, for each rebalancing, the return of the managed portfolio $$f_t$$ is a function of characterstics observed ahead of time $$c_{t-1}$$. The return series of such a managed portfolio is supposed to be a proxy of a factor's impact on all kinds of securities in the financial market.

$$
\begin{aligned}
f_t &= f(c_{t-1}, r_t), \forall t \in [1..T]\\
\end{aligned}
$$

Using a portfolio instead of a few securities to proxy fator helps to reduce noise,  while definitely not all of them. Other than the true signal $$\alpha$$ that governs the long term performance of the factor, which is likely to linger around in the future out of sample and what we care! Another key driver behind $$f_t$$ (a lot of the times larger in magnitude) is a series of disturbance term $$\epsilon_t$$ representing shokc specific to each of the period. 

$$
\begin{aligned}
f_t&= \alpha + \epsilon_t \\
\epsilon_t &\sim N(0, \sigma^2) \\
&\forall t \in [1..T]
\end{aligned}
$$

Traditionally in empirical asset pricing, the signal embeded in the facotr $$\alpha$$ is seen as a constant, which leads to pretty straightfoward estimation. The sample mean of the realized returns from the managed portfolio (from here on, let's just call it factor return for short), with the distrubance term netting out for their 0 expected value, is our estimate on $$\alpha$$. Its standard error is also captured as $$\dfrac{1}{T}\sigma^2$$ under the IID Gaussian assumption. Further analysis like hypothesis testing is a natural extension from here.

$$
\begin{aligned}
\hat{\alpha} &= \bar{f_t}= \dfrac{1}{T}\sum_t f_t = \alpha + \dfrac{1}{T}\sum_t \epsilon_t \\
\end{aligned}
$$

While, unfortunately, such a concise and intuive estimation process does not necessarily lead to a smooth journey ahead. For one hand, volatility.

especially nowadays with the continous emergence of new factors. For one hand, the number of parameters required for estimation increased exponentially with the increase of factors. While the sample of the data does not grow at a comparable speed - not even close! This is also the reason why there is rarely effort following the trail to model all factors jointly as a whole. The additional parameters required to mdoel the interaction among the factors just make things worse. 

On the other hand, the data sets are notoriously famous for its 

Clearly, we can use some innovation beyond the traditional framework to light our road ahead.


### The Bayesian Len <a name="bayes"></a>

The Bayesian statistic is potentially an answer. Facing a data set with classic feature of small N (sample size) and large k (dimension), it's probably a good idea to in


Although things more and more toward the direction of machine learning techniques instead of traditional econometric.

Bayesian model

In a frequentist view, too less data to construct a large model. 

benefit: flexible framwork to combine.  less vunerable to multiple testing, all parameters can be modeled together much easily. way more easier to work with large number of parameters. 

model for assessing factor replicability. hierarchical structure to model themes cross regions and regimes.


pool of information about alpha cross different samples. 


story - mean - variance large, hard particularly multiple factor, curse dimension, inject domain knowledge via bayesian framework - how the result compare - open flexibility for further structure for alpha and shock. 

$$
\begin{aligned} 
&\text{Frequentist} \\
f_t&= \alpha + \epsilon_t \\
& \epsilon_t \sim N(0, \sigma^2) \\
\hat{\alpha} &= \bar{f_t}= \dfrac{1}{T}\sum_t f_t = \alpha + \dfrac{1}{T}\sum_t \epsilon_t \\
&\text{dimensional curse ...} \\
&\text{Bayesian} \\
\alpha &\sim N(0, \tau^2) ~~\text{(prior)}\\
\end{aligned}
$$

$$
\begin{aligned}
\mathbb{E}[X|Y,Z] &= \mu_x + (\Sigma_{XY}, \Sigma_{XZ}) 
\begin{pmatrix} 
\Sigma_{YY} & \Sigma_{YZ}  \\
\Sigma_{ZY} & \Sigma_{ZZ}  \\
\end{pmatrix}^ {-1} 
\begin{pmatrix}
Y-\mu_Y \\
Z-\mu_Z \\
\end{pmatrix} \\
Var(X|Y,Z) &= \Sigma_{XX} -  (\Sigma_{XY}, \Sigma_{XZ}) 
\begin{pmatrix} 
\Sigma_{YY} & \Sigma_{YZ}  \\
\Sigma_{ZY} & \Sigma_{ZZ}  \\
\end{pmatrix}^ {-1} 
\begin{pmatrix}
\Sigma_{XY} \\
\Sigma_{XZ} \\
\end{pmatrix} \\
\end{aligned} 
$$

$$
\begin{aligned}
E[\alpha|\hat{\alpha}]&=\dfrac{\tau^2}{\tau^2 + \sigma^2/T} \hat{\alpha}\\
Var[\alpha|\hat{\alpha}]&=\dfrac{\tau^2/T}{\tau^2 + \sigma^2/T}\Sigma^2
\end{aligned}
$$


**alpha hacking**

$$
\begin{aligned}
f_t^{OOS} &= \alpha + \epsilon_t \\
\hat{\alpha}^{OOS} &=\bar{f_t}^{OOS} = \alpha + \dfrac{1}{T^{OOS}} \sum_t \epsilon_t \\
f_t^{IS} &= \alpha + \epsilon_t + u_t, ~~~ u_t\sim(\bar{\epsilon}, \sigma_u^2) \\
\hat{\alpha}^{IS} &= \bar{f_t}^{IS} = \alpha + \dfrac{1}{T^{IS}}\sum_t{(\epsilon_t+u_t)}\\
&\Downarrow\\
E(\alpha|\hat{\alpha}^{IS}, \hat{\alpha}^{OOS}) &= \dfrac{1}{1 + \dfrac{1}{1 + (\dfrac{\tau^2 T^{IS}}{\sigma^2+\sigma_u^2} + \dfrac{\tau^2 T^{OOS}}{\sigma^2})}} (w(\hat{\alpha}^{IS}-\bar{\epsilon}) + (1-w)\hat{\alpha}^{OOS}) \\
w&= \dfrac{\sigma^2/T^{OOS}}{(\sigma^2+\sigma_u^2)/T^{IS} + \sigma^2/T^{OOS}}
\end{aligned}
$$

**hierachy**

$$
\begin{aligned}
f_t^i &= \alpha^i + \epsilon_t^i \\
\alpha^i &= c + w^i, ~~c\sim N(0, \tau_c^2), ~w^i\sim N(0, \tau_w^2) \\
Cor(\epsilon_t^i \epsilon_t^j) &=\rho \\
&\Downarrow \\
E(\alpha^i|\hat{\alpha}^1,..,\hat{\alpha}^N)&= \dfrac{1}{1 + \dfrac{\rho\sigma^2}{\tau_c^2T}+ \dfrac{\tau_w^2+(1-\rho)\sigma^2/T}{\tau_c^2N}}\dfrac{1}{N}\sum_j^N \alpha_j + \dfrac{1}{1 + \dfrac{(1-\rho)\sigma^2}{\tau_w^2T}}(\hat{\alpha}^i - \dfrac{1}{1 + \dfrac{\tau_w^2+(1-\rho)\sigma^2/T}{(tau_c^2+\rho\sigma^2/T)N}}\dfrac{1}{N}\sum_j^N \alpha_j)
\end{aligned}
$$



**finally**

$$
\begin{aligned}
&\Omega = var(\alpha), \Sigma = var(\epsilon) \\
E(\alpha|\hat{\alpha}) &= (\Omega^{-1} + T\Sigma^{-1})^{-1}(\Omega^{-1}\mathbb{1}\alpha^0 + T\Sigma^{-1}\hat{\alpha})
\end{aligned}
$$


heavy role of prior.
### Reference <a name="ref"></a>
- Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance
- Bali, Engle & Murray (2016): Empirical Asset Pricing: The Cross Section of Stock Returns
- Cochrane (2011): Presidential Address: Discount Rates
