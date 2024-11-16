#

## A First Glimpse into the "Factor Zoo"

- [The Factor Zoo](#crisis)
- [Bayes For Good!](#bay)
- [Reference](#ref)


In a previous blog, [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off our discussion around finding factors that drive cross-sectional security returns out-of-sample in the real word. Specifically, we talked about one key challenge in this journey - the multiple testing problem. Essentially, when factors are identified through extensive searches, their apparent in-sample predictive power often owes more to luck than to genuine predictive ability.

The sheer volume of factors published, not to mention the countless more tested behind the scenes, demonstrates a quite exhaustive effort to this search. In this scenario, the traditional 1.96 t-statistic threshold no longer ensures a 5% Type I error rate. The bootstrap method we discussed in the previous blog come as an attempt to mitigate this problem. A customized orthogonalization to establish a purified null hypothesis that holds by design is combined with bootstrapping to generate the actual distribution of desried robust metrics under the null hypothesis. These adjusted benchmarks provide a more reliable basis for comparison. While not a perfect resolution, we are still subject to a sample of smaller size compared to number of factors with evolving distribution, it’s certainly a solid starting point.

Time to proceed along the journey! With hundreds or even thousands of factors (Cochrane called this as 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), a lot more observations, problems and models to discuss!

### The Factor Zoo <a name="crisis"></a>

This vast number of factors claimed to predict security returns in academic articles stands in contrast to the traditional wisdom of the investment community - predicting expected returns is difficult. If these documented factors truly possessed even modest predictive power, we’d be in a strong position to forecast expected returns. Yet, this isn’t the case. Something seems off in this 'Factor Zoo' and it’s worth investigating further.

In their paper "Replicating Anomalies", Hou, Xue & Zhang (2020) shed some lights on this puzzle. Quite remarkably, they replicated nearly 200 published factors, grouped them into 6 categories, and tested them using a comprehensive dataset of U.S. stocks (1967–2016) under consistent procedures. Each factor's predictive power was evaluated over three time horizons (1, 6, and 12 months) through sorted long-short portfolios. The finding was bitter: 65% of the factors failed to surpass the traditional t-statistic threshold of 1.96, and the failure rate further climbed to an astonishing 82% when a stricter threshold of 2.78 (accounting for multiple testing corrections) was applied.

Why such dismal replication rates? One cause lies in the dataset used. Hou et al.’s 50-year dataset of U.S. security returns is more comprehensive than the majority of data sets used in earlier factor studies. In the financial markets, where the signal-to-noise ratio is inherently low, it’s not surprising for a factor to perform well in localized samples but fail in broader datasets. It is especially the case when there are incentives to customize the sample to achieve more significance for publication. 

Another significant factor highlighted by Hou et al. is the disproportionate emphasis on illiquid micro-cap stocks in earlier research. Many factors, particularly those with behavioral roots, show stronger predictive power among smaller stocks, likely due to their lower levels of investor attention and higher transaction costs. However, weighting micro-cap stocks equally in factor portfolio construction or regression analysis creates an imbalance. These stocks represent as little as 3% of total market capitalization but account for up to 60% of the total number of stocks, leading to an overemphasis that skews results.

On the other side, Jensen, Kelly, and Pedersen (2023) offer a contrasting view. Using an even broader dataset spanning 93 countries and nearly a century of history, they tested factor replication under a Bayesian framework. Their results were significantly different: an 82% replication success rate compared to Hou et al.’s 35%. How could the outcomes diverge so dramatically? Several key differences in data and test procedure are behind this discrepancy. 

First and probably foremost, Jensen et al. switched from raw factor return to CAPM alpha, which alone increased the replication rate by over 20%. This adjustment makes some sense since the goal of factor research is to identify additional improvements beyond the market beta. However, it also introduce some unintentional distortions. For example, for the low volatility factor, the original intend is to see whether stocks with lower volatility outperform the others. While when regressing out the market return to the CAPM alpha, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. 

A lot more drivers are behind this sharp increase in successful rate. Like, Jensen et al uses a capped value weight in factor portfolio construction to avoid concentration in mega stocks. The market cap of a stock is capped at 80% percentile hence all stocks with size beyond this point would be assigned this 80% percentile value. Additionaly, they are using a much longer history in US stock even compared to Hou et al's already extensive data set. Rather than looking into 3 horizons of 1 month, 6 month and 12 months, they exclusively focused on the 1 month horizon. Their innovative bayesian modeling also leads to some degree of difference.

![GDP](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/replication.jpg)

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
