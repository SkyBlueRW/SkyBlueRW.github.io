## Navigating the Factor Zoo!

- [From Factors to Managed Portfolios](#portfolio)
- [The Classic](#classic)
- [The Bayesian Len](#bayes)
- [Reference](#ref)

In our previous blog, [A First Glimpse into the "Factor Zoo"](https://skybluerw.github.io/2024/12/07/factor-zoo.html), we took a bird's eye view of the empirical evidence for hundreds of factors in the "Factor Zoo" and saw how drastically different conclusions studies can arrive at. Despite the lingering debates over replication issues in empirical asset pricing research, it's time to step closer and zoom in on the inner workings of factor modeling and evaluation.

At the heart of empirical factor research usually lies one question: "Is this factor's alpha statistically different from zero, and is it economically meaningful hence expected to repeat?". Traditionally, researchers address this by focusing (almost exclusively) on a factor’s expected return and variance, reflecting theory’s emphasis on covariates and their first two moments and the analytical convenience that comes with them. It's not always the case. For example, investors during their investment exercise would definitely appreciate a more comprehensive picture of the return distribution for features like higher moments, tail behavior, invariant parameters and so one. Every extra insight potentially translate into an investment edge. While regardless of whether mean and variance summarize well to describe the performance of a factor, a clear, explicitely stated process for factor modeling and evaluatioin delivers value from every aspect to navigate the factor zoo. 

In this blog, we'll try to unpack the nuts and bolts behind the modeling and evaluation. We will begin with the traditional, frequentist toolkit with those classic methods in empirical asset pricing research and then march toward a Bayesian framwork innovation that Jensen, Kelly & Pedersen (2023) introduced to incorporate additional structures in modeling. Even under the current trend with machine learning techniques gainning more and more attention, these structured econometric insights remain crucial when samples are small, dimensions explode and signals hide in noise - the very challenges endemic to financial markets!

### From Factors to Managed Portfolios <a name="portfolio"></a>

What, then, is a factor in asset pricing?

Nothing mystical! A factor is simply a measurable variable that captures patterns of co-movement among security returns. It's worth highlighting that, although these co-movements may stem from a wide variety of forces (economic growth, geopolitical status, consumption, demand, investor sentiment, and so on), these drivers are usually abstract and unobservable concepts. For instance, we all know that investor sentiment moves markets, prices would surge on optimism and retreat on pessimism. Yet no one knows the "true" equation to define investor sentiment or how to gauge it in real time.

Fortunately, managed portfolios (sometimes also called factor mimicking portfolio with subtle difference) offer a workaround! A factor may carry implications across a wide range of domains from social psychology to consumer behavior to political events... While in asset pricing, it's our choice to discard any dimension unrelated to security return and focus solely on the market relevant component of the factor - essentially the projection of the factor onto the return space of securities. Now we reframe our objective from defining an abstract concept to measuring its projected returns - something equally powerful in financial markets but far easier to define and measure. With our focus squarely on financial market only, it is viable to construct a managed portfolio of securities whose returns directly capture this projection and by extension the factor’s financial impact.

Still take the investor sentiment as an example: although the true state of market mood is inherently hard to define or quantify, we know that certain securities (for example, those with high analyst forecast dispersion or larger short position open interest) tend to react more strongly to sentiment swings. A managed portfolio built on these characteristics aims to capture those performance differences and thus proxy the  factor. 

Typically, such managed portfolios are implemented as long-short portfolios built on observable security characteristics. The implementation choices are abundant: we can opt for characteristic sorting versus regression approaches, include or omit controls for the cross-effects of other factors, select quantile breakpoints, set rebalancing intervals, and so on. Despite all these flexibilities, the core idea remains the same: at each rebalancing date $$t$$, we form a portfolio whose return proxies the factor's projection, with predefined portfolio construction using previous period characteristics ($$c_{t-1}$$) and contemporaneous return ($$r_t$$).

$$
\begin{aligned}
f_t &= f(c_{t-1}, r_t), \forall t \in [1..T]\\
\end{aligned}
$$

The adopt of managed portfolio comes with clear convenience. Rather than chasing an unobservable economic construct and bear with all the bias and inaccuracy of the estimation following, we now work with a time series of predefined portfolio, which is easy to quantify, analyze and simulate from an investment perspective. 

The shift to managed portfolios brings immediate convenience. something concrete to work with. Easier to measure. Unconditional



### The Classic <a name="classic"></a>



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
