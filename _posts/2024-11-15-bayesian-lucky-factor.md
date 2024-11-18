#

## A First Glimpse into the "Factor Zoo"

- [The Factor Zoo](#crisis)
- [The Pro and Con sides](#two)
- [Reference](#ref)

### The Factor Zoo <a name="crisis"></a>


In a previous blog, [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off the discussion around identifying factors that drive cross-sectional security returns out-of-sample in the real world. Specifically, we talked about one critical challenge in this journey - the multiple testing problem. Basically, when factors are identified through extensive searches, their apparent in-sample predictive power often owes more to luck than to genuine predictive ability. The massive number of factors published, not to mention the countless more tested behind the scenes, demonstrates a quite exhaustive effort researchers have devoted to this quest. Facing this typical mutiple testing scenario, the traditional 1.96 t-statistic threshold no longer ensures a 5% Type I error rate. 

The bootstrap method discussed previously come as an attempt to mitigate this problem. By combining a customized orthogonalization technique, which sets up a purified null hypothesis that holds by design, with bootstrapping to generate the actual distribution of desired robust metrics under the null hypothesis, researchers can establish more reliable benchmarks for statistical test. While not a perfect resolution, we are still subject to a sample of smaller size compared to number of factors with evolving distribution, it’s certainly a solid starting point.

Time to proceed along the journey! With hundreds or even thousands of factors (Cochrane called this 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), there are a lot more observations, challenges and models to discuss!

In this blog, let's check out two opposing views on the 'Factor Zoo'. This massive collection of factors, each claiming to predict security returns, doesn't quilte line up with the investment community’s conventional wisdom: predicting expected returns is difficult. If these documented factors truly possess even modest predictive power, we’d be well-equipped to forecast returns. Yet, this isn’t the case. Something seems off in this 'Factor Zoo' and it’s definitely worth a bit digging. 

### The Pro and Con sides <a name="two"></a>


In the paper "Replicating Anomalies", Hou, Xue & Zhang (2020) shed some lights on this puzzle. Quite remarkably, they replicated nearly 200 published factors and tested them using a comprehensive dataset of U.S. stocks (1967–2016) under consistent procedures. Each factor's predictive power was evaluated over three time horizons (1, 6, and 12 months) through sorted long-short portfolios. The finding was bitter: 65% of the factors failed to surpass the traditional t-statistic threshold of 1.96. The failure rate further climbed to an astonishing 82% when a stricter threshold of 2.78 accounting for multiple testing corrections.

Why such dismal replication rates? One key cause highlighted by Hou et al. is the disproportionate emphasis on illiquid micro-cap stocks in earlier research. Many factors show much stronger predictive power among stocks of smaller size， likely due to the lower levels of investor attention recevied and higher transaction costs required. However, weighting these micro-cap stocks equally in factor portfolio construction or regression analysis as a lot of factor research did obviously creates an imbalance. These stocks represent as little as 3% of total market capitalization but account for up to 60% of the total number of stocks, leading to an overemphasis that skews results.

One cause lies in the dataset used. Hou et al.’s 50-year dataset of U.S. security returns is more comprehensive than the majority of data sets used in earlier factor studies. In the financial markets with inherently low signal-to-noise ratio, it’s not surprising for a factor to perform well in localized samples but fail in broader datasets. It is especially the case when there are incentives to customize the sample to achieve more significance for publication. 

On the other side, Jensen, Kelly, and Pedersen (2023) offered a contrasting view. Using an even broader dataset spanning 93 countries and nearly a century of history, they reached a significantly different result: a 82% replication success rate compared to Hou et al.’s 35%. How could the outcomes diverge so dramatically? Several key differences in data and test procedure are behind this discrepancy. 

Obviously the different data sets used account for a significant , Jensen et al. switched from raw factor return to CAPM alpha, which alone increased the replication rate by over 20%. This adjustment makes some sense since the goal of factor research is to identify additional improvements beyond the market beta. However, it also introduce some unintentional distortions. For example, for the low volatility factor, the original intend is to see whether stocks with lower volatility outperform the others. While when regressing out the market return to the CAPM alpha, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. 

A lot more drivers are behind this sharp increase in successful rate. Like, Jensen et al uses a capped value weight in factor portfolio construction to avoid concentration in mega stocks. The market cap of a stock is capped at 80% percentile hence all stocks with size beyond this point would be assigned this 80% percentile value. Additionaly, they are using a much longer history in US stock even compared to Hou et al's already extensive data set. Rather than looking into 3 horizons of 1 month, 6 month and 12 months, they exclusively focused on the 1 month horizon. Their innovative bayesian modeling also leads to some degree of difference.

![GDP](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/replication.jpg)
Source: Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance


35% vs 85% is quite a drmatic difference, no wonder all the discussions and debates around wheather there is a replication crisis in empirical asset pricing research. small make sense. 






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
