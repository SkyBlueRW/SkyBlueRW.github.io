#

## The Bayesian Modeling of Factors!

- [Introduction](#introduction)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

In a previous blog ([The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html)), we have discussed one challenge that can lead to deteriorating out of sample performance in security return prediction - the multiple testing problem. Essentially, when factors are identified through extensive or exhaustive searches, their apparent predictive power in sample may stem more from luck than genuine ability. 

The thousands of factors out there claimed to predict security return and hundreds of thousands factors potentially experimented to reach these publications obviously represent a quite exhustive effort in the searching of factors. 




capped value weight, residual return compared to market


we are easily subject to multiple selection bias. clean representation of the null hypothesis with bootstrap

refrain from local noise

$$
\begin{aligned}
\hat{\alpha}^i &= \alpha^i + \epsilon^i \\
\epsilon^i &\sim N(0, \sigma^2) \\
E(\alpha|\hat{\alpha}) &= E(\alpha) + \dfrac{cov(\alpha, \hat{\alpha})}{var(\hat{\alpha})} (\hat{\alpha} - E(\hat{\alpha})) \\
&=E(\hat{\alpha}) + \dfrac{var(\alpha)}{var(\alpha) + var(\hat{\alpha})} (\hat{\alpha} - E(\hat{\alpha})) \\
&= E(\hat{\alpha}) + \dfrac{1}{1 + \dfrac{var(\hat{\alpha})}{var(\alpha)}} (\hat{\alpha} - E(\hat{\alpha}))
\end{aligned}
$$

### Reference <a name="ref"></a>
- Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance
- Hou, Xue & Zhang (2020): Replicating Anomalies
