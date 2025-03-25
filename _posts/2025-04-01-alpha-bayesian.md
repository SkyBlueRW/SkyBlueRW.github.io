## Bayesian len in factor zoo!

- [The "Big Hit"](#introduction)
- [Here Comes the Change](#change)
- [Reference](#ref)




In the previous blog [A First Glimpse into the "Factor Zoo"](https://skybluerw.github.io/2024/12/07/factor-zoo.html), we took a high level look into the empirical results of factors within the "factor zoo" and saw how different or even opposite conclusions can be drawn from there. Despite the unsettled debates about whether there are serious replication problems in empirical asset pricing literature, it's time to zoom in and take a closer look. 

Obviously, The goal does not align exactly of factor researchs in acadmia and in industry. To serve investment exercise, we look for more than a "yes or no" answer as hypothesis testing got us in academic research. Rather, we look to learn as much as possible of the distribution of the factor performance, where any bit of additional information enhance the edge in investment. But those spirites of modeling with insights of the market are universal. In this blog, we turn our attention to the modeling and evaluation bits of the "factor zoo". We will start with the a more frequentist flavor with all the classic methods in empirical asset pricing for factor evaluation and march toward the Bayesian framework that Jesen, Kelly & Pedersen (2023) used, which provides greater flexibility to impose structures in the process.

Even under the current context of more and more shifting of research paradigm from traditional econometric methods to machine learning techniques, such insights expressed as model structures can be quite helpful and likely necessary considering the limited amount of data available in the financial market and their troubling natures of low signal to noise ratio.

When we say a factor helps to predict expected return, we actually declare some co-movements of security returns identified and measured. While unfortunately, though these kinds of co-movements can originate from a variety of causes like economic growth, geopolitical status, consumption, demand, investor sentiment... They are generally abstract concept that can hardly be defined and measured precisely and timely. For example, every body knows investor sentiment play a huge role in securities' return. Market roar when investors feel good and become vulnerable when permistism spreads. While no one can define excatly what's the equation for sentiment and how to measure it reasonably, which makes all the following efforts like estimating the sensitivity of volatile security return on the not well defined factor quite hopeless.

Obviously, defining and measuring factor itself is already a challenge. Researchers circled around for mitigations. Rather than defining and measuring the factor directly, they cleverly announce that the part of factors that is relevant with the financial market - a projection of the factor onto the payoff space of securities is all we care. A factor can have much more meaning beyond financial market in all kinds of aspects, while as long as financial market is the only focus, there is not a reason stopping us from building a managed portfolio of securities - the building block of financial market, to measure the financial aspect of that factor. Now things become much easier, we turn the problem from precisely define and measure a factor to find out a managed portfolio whose performance proxy the financial aspect of the factor. Quite naturally, we can start from security characteristics seen relevant with its sensitivity to such factor and take it for the construction of the managed portfolio. 

Traditionally, such managed portfolios are obtained via long short sorting of security characterstics

$$
\begin{aligned}
f_t &= f(c_{t-1}, r_t)\\
\end{aligned}
$$


[Stochastic Discount Factor: a nutshell of asset pricing](https://skybluerw.github.io/2023/03/17/sdf-nutshell.html))




### The "Big Hit" <a name="introduction"></a>


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
