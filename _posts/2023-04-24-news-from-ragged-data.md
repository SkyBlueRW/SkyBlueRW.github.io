
#


## The News From Ragged Economic Data 

- [Economic Indicator: the informative and nerve-wracking data flow](#data)
- [The Dynamic Factor modeling of Economic Indicators](#dfm)
- [The News from the economic Data](#news)
- [Reference](#ref)

economic data special
ragged
different frequency

### Economic Indicator: the informative and nerve-wracking data flow <a name="data"></a>



#### Economic Data Flow: Ragged and Mixed Frequency

![Image of Pyramid](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/ragged_economic_indicator.png)

*Lucrezia Reichlin's [Presentation on Nowcast](https://www.oecd.org/naec/new-economic-policymaking/NAEC_2019_Nowcasting_L_Reichlin.pdf)*

### The Dynamic Factor modeling of Economic Indicators <a name="dfm"></a>


### The News from the economic Data <a name="news"></a>




nowcast 
one side a cohesive stat framework to handle this raged different frequency

joint modeling of the dynamics of data with different frequency.

present forecast in an insightful way such that forecast of variable of interest is updated as weighted sum of news measured as different between realization and forcast of other variables. Formalization of work process hence easy to fit into investment decision process.

info arrive in an incremental manner


- [Introduction](#introduction)
- [Reference](#ref)


### Introduction <a name="introduction"></a>


$$
\begin{aligned}
\Omega_v &:\{x_{i, t_i}, t_i=1,2,...,T_{i,v}, i = 1,...,n \} \\
P[x_{i,t}|\Omega_v] &= E[x_{i,t}|\Omega_v] \\ 
E[x_{i,t}|\Omega_{v+1}] &= E[x_{i,t}|\Omega_v] + E[x_{i,t}|I_{v+1}] \\ 
I_{v+1, j} &= x_{j, T_{j, v+1}} - E[x_{j, T_{j, v+1}} | \Omega_v] \\
E[x_t|I_{v+1}] &= E[x_t I_{v+1}^T]{E[I_{v+1} I_{v+1}^T]}^{-1} I_{v+1}
\end{aligned}
$$

unexpected news

Gaussian


$$
\begin{aligned}
E[x_t|I_{v+1}] &= \sum_{j \in J_{v+1}} b_{j,t,v+1}(x_{j, T_{j,v+1}} - E[x_j,T_{j, v+1}|\Omega_v]) \\ 
\end{aligned}
$$


$$
\begin{aligned}
x_t &= \mu + \Lambda f_t + \epsilon_t \\
f_t &= A_1 f_{t-1} + ... + A_p f_{t-p} + u_t \\ 
\epsilon_{i,t} &= \alpha_i \epsilon_{i, t-1} + e_{i,t} \\ 
\end{aligned}
$$


### Reference <a name="ref"></a>


- Banbura, Giannone & Reichlin(2010): Nowcasting
- Banbura & Modugno (2010): Maximum Likelihood Estimation of Factor Models on Datasets with Arbitrary Pattern of Missing Data
- Bok, Caratelli, Giannone, Sbordone & Tambalotti (2018): Macroeconomic Nowcasting and Forecasting with Big Data
- Chad Fulton's Blog: [Large dynamic factor models, forecasting, and nowcasting](http://www.chadfulton.com/topics/statespace_large_dynamic_factor_models.html)
