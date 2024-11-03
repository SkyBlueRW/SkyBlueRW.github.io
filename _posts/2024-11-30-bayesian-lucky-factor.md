#

## A First Glimpse into the "Factor Zoo"

- [The Replication 'Crisis'](#crisis)
- [Bayes For Good!](#bay)
- [Reference](#ref)


In the previous blog [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off our discussion around challenges finding factors to predict security returns out of sample in the real word. Specifically, we talked about one critical blocker in this journey - the multiple testing problem. Broadly, when factors are identified through extensive or exhaustive searches, their apparent predictive power in sample may stem more from luck than genuine predictive ability. 

The thousands of factors out there and hundreds of thousands factors more potentially experimented behind the curton to reach these publications obviously demonstrate a quite exhustive effort in searching of factors. Facing this scenario of multiple testing, passing the traditional t-statistic threshold of 1.96 is no longer a sufficient guarantee of 5% type I error. 

The bootstrap method discussed in the previous blog come as an attempt to counter this problem. Customized orthogonalization technique is used to establish a purified null hypothesis that is guarantted to hold in the sample by design, followed by bootstrap to generate the real distribution of some robust metrics of choice under the null hypothesis as the adjusted control benchmark for comparison. Not a perfect resolution, we are still subject to a sample of smaller size compared to number of factors with evolving distribution. But definitely a good start point acknowledging and mitigating it.

Time to continue the journey! With hundreds or even thousands of factors (Cochrane called this as 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), a lot more observations, problems and modeling to discuss!

### The Replication "Crisis" <a name="crisis"></a>

This large number of factors documented to predict security return separately in academic articles does not really align the traditional wisdom in investment - expected return is hard to predict. We should be in a pretty good position in terms making prediction on expected return even if these documented factors have slight and marginal prediction power on it. While this is not the case and something is off with the large pool of factors.

Hou, Xue & Zhang (2018) shed some lights into this puzzle in the article "Replicating Anomalies". Quite amazingly, they grouped almost 200 factors into 6 categories, and tested all of them under the same treatment and data sets (1967 ~ 2016). Each of the factors is tested on their predictive power on the cross sectional return over 3 horizons (1, 6, 12 months) via sorting long-short portfolios. The result is not really in favor. 65% of the factors failed the tradtional t-statistic treshold of 1.96. The failure rate rose further to 82% if a 2.78 t-statistic accounting for multiple correction is used. 

Quite an disapointing replication rate - some even call it a replication crisis in asset pricing research. One cause of this low replication rate is the data set used. A 50-year long history of US security return constituets a quite comprehensive data set larger than majority of the research documenting these factors. In the financial market full of uncertainties, it is not that surprising to see a factor working locally fail in a longer sample. Especially when there are incentives to customize the sample for significance. 

Another cause that Hou, Xue & Zhou hilighted in their article is the over-emphasis in small and tiny stocks in the previous factor research. 









65%, 82%



Or to make things simpler, just raise the bar of the t-statistic to account for this much lossened selection! For instance, Hou, Xue & Zhang (2020) adpoted a 2.78 t-statistic for the 5% confidence level to account for this multiple testing problem. 




### Bayes For Good <a name="bay"></a>

All of this will be helpful in our battle against the multiple testing issues in factor research. While we definitely could use some more help. After all the statistical significance derived under the frequentist approach is an assessment on the compatability of data and the null hypothesis (generally set to be the factor do no have predictive power). In the sense it measures the likelihood of the data if the null hypothesis is true ($$P(Data|H_0)$$). Tough containing certain aspects of information, It is not as relavant as we hope at the first place. After all, the more relavant question in factor research is probably this - given the data observed, how likely is the factor truly bearing the predictive power ($$P(H_1|Data)$$).



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
- Hou, Xue & Zhang (2018): Replicating Anomalies
- Cohcrane (2011): Discount Rates
