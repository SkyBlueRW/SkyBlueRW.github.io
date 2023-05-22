
#


## Nowcasting: The News From Jagged Economic Data 

- [Economic Indicators: the informative and nerve-wracking data flow](#data)
- [The Dynamic Factor modeling of Economic Indicators](#dfm)
- [The insights from DFM](#news)
- [EM Estimation](#em)
- [Reference](#ref)


### Economic Indicators: the informative and nerve-wracking data flow <a name="data"></a>


Financial market is like a bustling abstraction of economic activities, where people jump into the bus for economic objects such as sharing income and mitigating risk. Therefore, it is not surprising to see that economic conditions are quite relavant in managing investment within the financial markets.

Empirical research has also validated this notion. Scholars and industry experts have dedicated significant efforts to conduct studies, revealing the profound influence of various economic factors on the performance of asset classes, yield curves, sectors, styles, and so on. It hilighted the importance of considering economic indicators when making informed investment decisions.

While it is not a straghtforward task to incorporate the data flow of economic indicators into a regular investment decision process. We are faced with an overwhelming number of indicators, which are unstructured in their natures. Just like the chart below shows.

#### Economic Data Flow: Jagged and Mixed Frequency

![Image of Pyramid](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/ragged_economic_indicator.png)

*Lucrezia Reichlin's [Presentation on Nowcast](https://www.oecd.org/naec/new-economic-policymaking/NAEC_2019_Nowcasting_L_Reichlin.pdf)*

On one hand, these indicators are published at different frequencies. For example, we have indicators such as GDP, which is published on a quarterly basis, PMI, which is published monthly, or even indicators released at higher frequencies like electricity usage, market data and so on. On the other hand, the publish schedule can vary significantly for different indicators. For instance, GDP and Industrial Production  are typically published more than one month after the reporting period, while PMI is usually published immediately after the reporting period. 

Fortunately, we have the nowcast model at our disposal to navigate this complex data flow. Originally developed with a primary focus on monitoring GDP growth at central banks, the nowcast model provides a cohesive statistical framework to handle the irregular and mixed-frequency nature of economic data. This model empowers us to establish a robust system that continually updates our insights on economies based on the incremental release of data, regardless of its irregular frequency and release schedule.

In this blog, we will explore the remarkable capabilities of the nowcasting model. We will delve into the intuition behind this powerful tool, focusing on its modeling and estimation aspects. Additionally, we will provide practical insights on ways to incorporate this model into the decision-making process through illustrative toy examples.

### The Dynamic Factor modeling of Economic Indicators <a name="dfm"></a>

Embarking on our exploration, let's delve into the inner workings of the nowcast model to gain some intuition. At its core, the nowcast model is built on the foundation of a dynamic factor model (DFM). By incorporating equations to link indicators at different frequencies and utilizing a customized EM (Expectation-Maximization) algorithm, the nowcast model effectively addresses the challenges posed by mixed-frequency and irregular data flow by treating indicators not yet published as missing values via Kalman filter.

**Dynamic Factor Model**


As the foundation of a nowcast model, the DFM aim to find a concise set of latent factors that drive a significant portion of the variation across a wide array of observed economic indicators. What set the DFM apart as "dynamic" is that it jointly model and estimate both the observed economic indicators and the transition dynamics of the latent factors. 

In the nowcast model, all economic indicators are modeled at their highest frequency. The observed economic indicators, denoted as $$y_t$$, are governed by a small set of latent factors, denoted as $$f_t$$. Each latent factor represents a specific aspect of the economy. The dynamics of the latent factors and the idiosyncratic components $$\epsilon_t$$ are modeled using a vector autoregressive (VAR) process.

A typical DFM representation of nocast model are as follows where $$\Lambda$$ is the loading matrix that determins how a economic indicator impacted by lattent factors and matrix $$A_p$$ governs the evolve of the lattent factor. 

$$
\begin{aligned}
y_t &= \mu + \Lambda f_t + \epsilon_t \\
f_t &= A_1 f_{t-1} + ... + A_p f_{t-p} + u_t \\ 
\epsilon_{i,t} &= \alpha_i \epsilon_{i, t-1} + ... + e_{i,t} \\ 
u_t &\sim N(0, Q) \\
e_{i, t} &\sim N(0, I)
\end{aligned}
$$

It's also quite easy to impose further structures in the model to represent the reality. For example, Banbura, Giannone & Reichlin(2010) partitioned $$f_t$$ into 3 factors: A global factor $$f_t^{G}$$ that loads on every economic indicator and summarize the general economic condition and two factors $$f_t^{N}, f_t^{R}$$ that loads on nomial indicators and real indicators separately to account for cross section structure within real and nominal indicators.

Such a formation can be easily achieved via restrictions on the loading matrix, the transition matrix and the covariance matrix.

$$
\Lambda = \begin{bmatrix}
    \Lambda_{N,G} & \Lambda_{N,N} & 0 \\
    \Lambda_{R,G} & 0 & \Lambda_{R,R}
\end{bmatrix}
$$

$$
A_i = \begin{bmatrix}
    A_{i,G} & 0 & 0 \\
    0 & A_{i, N} & 0 \\
    0 & 0 & A_{i,R}
\end{bmatrix}
$$

$$
Q = \begin{bmatrix}
    Q_G & 0 & 0 \\
    0 & Q_N & 0 \\
    0 & 0 & Q_R
\end{bmatrix}
$$

**Handling of mixed frequency**

Since the DFM is at the highest frequencies of all economic indicators, an equation to align indicators at lower frequency would be required. Let's take the case of integrating GDP into a monthly model as an example. Suppose $$GDP_t$$ refers to the unobserved monthly GDP series. 

The goal is to align the observed QOQ GDP growth ($$x_t^{Q} = log(\dfrac{GDP_{t-2} + GDP_{t-1} + GDP_t}{GDP_{t-5} + GDP_{t-4} + GDP_{t-3}})$$) and the unobserved MOM GDP growth ($$x_t^{M} = log(\dfrac{GDP_t}{GDP_{t-1}})$$)

$$
\begin{aligned}
x_t^M &= \mu_Q + \Lambda_Q f_t + \epsilon_t^Q \\ 
\downarrow
x_t^Q = 9 \mu_Q + \Lambda_Q f_{t} + 2\Lambda_Q f_{t-1} + \Lambda_Q f_{t-2} + \Lambda_Q f_{t-3} + \Lambda_Q f_{t-4} + \epsilon_{t}^Q + 2\epsilon_{t-1}^Q + 3\epsilon_{t-2}^Q + 2\epsilon_{t-3}^Q + \epsilon_{t-4}^Q 
\end{aligned}
$$

$$
\begin{aligned}
log(\dfrac{GDP_{t-2} + GDP_{t-1} + GDP_t}{GDP_{t-5} + GDP_{t-4} + GDP_{t-3}}) &\approx  log(\dfrac{GDP_t}{GDP_{t-1}} (\dfrac{GDP_t-1}{GDP_{t-2}})^2 (\dfrac{GDP_t-2}{GDP_{t-3}})^3 (\dfrac{GDP_t-3}{GDP_{t-4}})^2 \dfrac{GDP_4}{GDP_{t-5}}) \\
&\downarrow \\
x_t^{Q} &\approx x_{t}^M + 2x_{t-1}^M + 3x_{t-2}^M + 2x_{t-3}^M + x_{t-4}^M
\end{aligned}
$$

With the linking equation, we can include the quarterly GDP growth in a monthly model 

$$
\begin{bmatrix}
  y_t \\
  x_t^Q
\end{bmatrix} = \begin{bmatrix}
  \mu \\
  \mu_Q
\end{bmatrix} +  \begin{bmatrix}
  \Lambda &0 &0 &0 &0 &I_n &0 &0 &0 &0 &0 \\
  \Lambda_Q &2\Lambda_Q &3\Lambda_Q &2\Lambda_Q &\Lambda_Q &0 &1 &2 &3 &2 &1
\end{bmatrix}  \begin{bmatrix}
  f_t \\
  f_{t-1} \\
  f_{t-2} \\ 
  f_{t-3} \\
  f_{t-4} \\
  \epsilon_{t} \\
  \epsilon_{t}^Q \\
  \epsilon_{t-1}^Q \\
  \epsilon_{t-2}^Q \\
  \epsilon_{t-3}^Q \\
  \epsilon_{t-4}^Q \\
\end{bmatrix}
$$





**Handling of jagged publish**



### EM estimation <a name="news"></a>

### The News from the economic Data <a name="news"></a>



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
