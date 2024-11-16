#

## A First Glimpse into the "Factor Zoo"

- [The Factor Zoo](#crisis)
- [Bayes For Good!](#bay)
- [Reference](#ref)


In a previous blog, [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off our discussion in search of factors that drive cross-sectional security returns out-of-sample in the real word. Specifically, we talked about one key challenge in this journey - the multiple testing problem. Essentially, when factors are identified through extensive searches, their apparent in-sample predictive power often owes more to luck than to genuine predictive ability—a critical blocker on this journey.

The sheer volume of factors published, not to mention the countless more tested behind the scenes, highlights the exhaustive effort researchers have dedicated to this search. In this scenario, the traditional 1.96 t-statistic threshold no longer ensures a 5% Type I error rate. To address this, we discussed the bootstrap method as a way to mitigate the issue. This method combines customized orthogonalization—used to establish a purified null hypothesis that holds by design with bootstrapping to generate the actual distribution of robust metrics under the null hypothesis. These adjusted benchmarks provide a more reliable basis for comparison. While not a perfect resolution, we are still subject to a sample of smaller size compared to number of factors with evolving distribution, it’s certainly a solid starting point.

Time to proceed along the journey! With hundreds or even thousands of factors (Cochrane called this as 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), a lot more observations, problems and models to discuss!

### The Factor Zoo <a name="crisis"></a>

This huge number of factors claimed to predict security return in academic articles does not really align with the traditional wisdom in investment community - expected return is hard to predict. Even if these documented factors have slight and marginal prediction power, we should be in a pretty good position in terms making prediction on expected return. While this is simply not the case. Something seems to be off with this factor zoo - worth a bit digging here.

In the article "Replicating Anomalies", Hou, Xue & Zhang (2020) shed some lights into this puzzle. Quite amazingly, they grouped around 200 factors published into 6 categories, and tested all of them with a comprehensive data sets (1967 ~ 2016, US listed stocks) and consistent procedures. Each of the factors is tested on their predictive power on the cross sectional security returns over 3 horizons (1, 6, 12 months) via sorted long-short portfolios. Quite pessimistically, 65% of the factors failed the tradtional t-statistic treshold of 1.96. The failure rate rose further to an astonishing 82% if a 2.78 t-statistic accounting for multiple testing correction is used. 

One reason behind this low replication rate is the data set used. The 50-year long history of US security return constituets a quite comprehensive data set larger than the majority of data sets used in previous factor research. In the financial market generally with low signal to noise ratio, it is not that surprising to see a factor working locally and fail in a longer sample. Especially when there are incentives to customize the sample to achieve more significance for publication. 

Another cause that Hou, Xue & Zhou hilighted a lot in their article is the over-emphasis on the illiquid micro cap stocks in the previous factor research. A lot of factors (especially those from a behavioral root) demonstrate much better predictive power among small stocks for their less attention received and higher transaction cost required. Treating these microcap stocks equally in a equal weight factor portfolio construction or OLS regression is defintely an excessive emphasis. As these microcap stocks account for as little as 3% in the total market capitalization but as much as 60% of total number of stocks. 

On the other side, Jensen, Kelly & Pedersen (2023) holds an apposing opinion on Hou et al's gloomy replication results. They built an even broader data set spanning 93 countries around the world that go back as far as a century in the history and tested the replication under a Bayesian framework. Compared to the dire 35% successful rate from Hou, Xue & Zhang (2020), they achieved a significantly different 85% succesful rate of replication. Wow, such a big difference.

Several difference leads to this dramatic difference of replication rate. First and foremost, Jensen et al are looking into the CAPM alpha instead of raw factor returns. This change alone account for a +20% raise in replication rate. It makes some sense to neutralize the market beta in the factor research, after all we want to gain marginal improvement in explaining security return with new factors. While it might also twist the factors in replication. For example, for the low volatility factor, the original intend is to see whether stocks with lower volatility outperform the others. While when regressing out the market return, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. 

A lot more drivers are behind this sharp increase in successful rate. Like, Jensen et al uses a capped value weight in factor portfolio construction to avoid concentration in mega stocks like the magnificent seven. The market cap of a stock is capped at 80% percentile hence all stocks with size beyond this point would be assigned this 80% value. Additionaly, they are using a much longer history in US stock even compared to Hou et al's already extensive data set. Rather than looking into 3 horizons of 1 month, 6 month and 12 months, they exclusively focused on the 1 month horizon. Their innovative bayesian modeling also leads to some degree of difference.

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
