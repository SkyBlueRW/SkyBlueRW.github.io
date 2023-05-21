
#


## Nowcast: The News From Ragged Economic Data 

- [Economic Indicators: the informative and nerve-wracking data flow](#data)
- [The Dynamic Factor modeling of Economic Indicators](#dfm)
- [The insights from DFM](#news)
- [EM Estimation](#em)
- [Reference](#ref)


### Economic Indicators: the informative and nerve-wracking data flow <a name="data"></a>


Financial market is like a bustling abstraction of economic activities, where people jump into the bus for economic objects such as sharing income and mitigating risk. Therefore, it is not surprising to see that economic conditions are quite relavant in managing investment within the financial markets.

Empirical research has also validated this notion. Scholars and industry experts have dedicated significant efforts to conducting studies, revealing the profound influence of various economic factors on the performance of asset classes, yield curves, sectors, styles, and so on. It hilighted the importance of considering economic indicators when making informed investment decisions.

While it is not a straghtforward task to incorporate the data flow of economic indicators into a regular investment decision process. We are faced with an overwhelming number of indicators, which are unstructured in their natures. Just like the chart below shows.

#### Economic Data Flow: Ragged and Mixed Frequency

![Image of Pyramid](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/ragged_economic_indicator.png)

*Lucrezia Reichlin's [Presentation on Nowcast](https://www.oecd.org/naec/new-economic-policymaking/NAEC_2019_Nowcasting_L_Reichlin.pdf)*

On one hand, these indicators are published at different frequencies. For example, we have indicators such as GDP, which is published on a quarterly basis, PMI (Purchasing Managers' Index), which is published monthly, or even indicators released at higher frequencies like electricity usage, market data and so on. On the other hand, the publish schedule can vary significantly for different indicators. For instance, GDP and Industrial Production  are typically published more than one month after the reporting period, while PMI is usually published immediately after the reporting period. 

Fortunately, we have the nowcast model at our disposal to navigate this complex data flow. Originally developed with a primary focus on monitoring GDP growth at central banks, the nowcast model provides a cohesive statistical framework to effectively handle the irregular and mixed-frequency nature of economic data. This model empowers us to establish a robust system that continually updates our insights on economies based on the incremental release of data, regardless of its irregular frequency and release schedule.

In this blog, we will explore the remarkable capabilities of the nowcasting model. We will delve into the intuition behind this powerful tool, focusing on its modeling and estimation aspects. Additionally, we will provide practical insights on how to effectively incorporate this model into the decision-making process through illustrative toy examples.


### The Dynamic Factor modeling of Economic Indicators <a name="dfm"></a>

To begin, we will unravel the underlying principles of the nowcasting model, shedding light on its inner workings. We will explore the methodologies employed in modeling and estimation, demystifying the process and making it accessible to both experts and novices alike. By understanding the foundation of the nowcasting model, we can better appreciate its value and the insights it offers.

At its heart

### The News from the economic Data <a name="news"></a>

### EM estimation <a name="em"></a>


nowcast 
one side a cohesive stat framework to handle this raged different frequency

joint modeling of the dynamics of data with different frequency.

present forecast in an insightful way such that forecast of variable of interest is updated as weighted sum of news measured as different between realization and forcast of other variables. Formalization of work process hence easy to fit into investment decision process.

info arrive in an incremental manner




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
