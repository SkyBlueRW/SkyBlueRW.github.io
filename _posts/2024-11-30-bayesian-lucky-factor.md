#

## A First Glimpse into the "Factor Zoo"

- [The Replication 'Crisis'](#crisis)
- [Bayes For Good!](#bay)
- [Reference](#ref)


In a previous blog [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off our discussion around challenges in finding factors with predictive power on security returns out of sample in the real word. Specifically, we talked about one critical blocker in this journey - the multiple testing problem. Essentially, when factors are identified through extensive searches, their apparent predictive power in sample may stem more from luck than genuine predictive ability. 

The thousands of factors out there and hundreds of thousands factors more potentially experimented behind the curton to reach these publications obviously demonstrate a quite exhustive effort in searching factors. Facing this scenario of multiple testing, passing the traditional t-statistic threshold of 1.96 is no longer a sufficient guarantee of 5% type I error. The bootstrap method we discussed in the previous blog come as an attempt to mitigate this problem. Customized orthogonalization technique is used to establish a purified null hypothesis that is guarantted to hold in the sample by design, followed by bootstrap to generate the real distribution of some robust metrics of choice under the null hypothesis as the adjusted control benchmark for comparison. Not a perfect resolution, we are still subject to a sample of smaller size compared to number of factors with evolving distribution. But definitely a good start point.

Time to continue the journey! With hundreds or even thousands of factors (Cochrane called this as 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), a lot more observations, problems and modeling to discuss!

### The Replication "Crisis" <a name="crisis"></a>

This huge number of factors documented to predict security return in academic articles does not really align with the traditional wisdom in investment community - expected return is hard to predict. Even if these documented factors have slight and marginal prediction power, we should be in a pretty good position in terms making prediction on expected return. While this is not the case. Something is off with the factor zoo.

In the article "Replicating Anomalies", Hou, Xue & Zhang (2020) shed some lights into this puzzle. Quite amazingly, they grouped around 200 factors into 6 categories, and tested all of them under the same treatment and data sets (1967 ~ 2016, US listed stocks). Each of the factors is tested on their predictive power on the cross sectional security returns over 3 horizons (1, 6, 12 months) via sorted long-short portfolios. The result is not really in favor. 65% of the factors failed the tradtional t-statistic treshold of 1.96. The failure rate rose further to 82% if a 2.78 t-statistic accounting for multiple correction is used. Quite an disapointing replication rate - some call it a replication crisis in empirical asset pricing research. 

One cause of this low replication rate is the data set used. A 50-year long history of US security return constituets a quite comprehensive data set larger than the data set used in majority of the research documenting these factors. In the financial market full of uncertainties, it is not that surprising to see a factor working locally and fail in a longer sample. Especially when there are incentives to customize the sample to achieve more significance for publication. Another cause that Hou, Xue & Zhou hilighted a lot in their article is the over-emphasis on the micro cap stocks in the previous factor research. A lot of factors (especially those from a behavioral root) demonstrate much better predictive power among small stocks for their less attention received and higher transaction cost required. Treating these microcap stocks equally in a equal weight factor portfolio construction or OLS regression is defintely an excessive emphasis. As These microcap stocks account for as little as 3% in the total market capitalization but as much as 60% of total number of stocks. 

On the other side, Jensen, Kelly & Pedersen (2023) holds an apposing opinion on this gloomy replication results. They built an even broader data set spanning 93 countries around the world that go back as far as a century in the history for their own replication. Compared to the dire 35% successful rate from Hou, Xue & Zhang (2020), they achieved a significantly different 85% succesful rate of replication. 

Several difference leads to this dramatic difference of replication rate. First and foremost, Jensen et al are looking into the CAPM alpha instead of raw factor returns. This change alone account for a +20% raise in replication rate. It makes some sense to neutralize the market beta in the factor research, after all we want to gain marginal improvement in explaining security return with new factors. While it might also twist the factors in replication. For example, for the low volatility factor, the original intend is to see whether stocks with lower volatility outperform the others. While when regressing out the market return, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. 

A lot more drivers are behind this sharp increase in successful rate. Like, Jensen et al uses a capped value weight in factor portfolio construction to avoid concentration in mega stocks like the magnificent seven. The market cap of a stock is capped at 80% percentile hence all stocks with size beyond this point would be assigned this 80% value. Additionaly, they are using a much longer history in US stock even compared to Hou et al's already extensive data set. Rather than looking into 3 horizons of 1 month, 6 month and 12 months, they exclusively focused on the 1 month horizon. Their innovative bayesian modeling also leads to some degree of difference.

![GDP](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/replication.jpg)

35% vs 85% Quite a drmatic difference, no wonder all the discussions and debates around wheather there is a replication crisis in empirical asset pricing research. 






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
