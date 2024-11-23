#

## A First Glimpse into the "Factor Zoo"

- [The Factor Zoo](#crisis)
- [The Skeptical and the Optimistic](#two)
- [And more](#more)
- [Reference](#ref)

### The Factor Zoo <a name="crisis"></a>


In a previous blog, [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off the discussion around identifying factors that drive cross-sectional security returns out-of-sample in the real world. Specifically, we talked about one critical challenge in this journey - the multiple testing problem. Basically, when factors are identified through extensive searches, their apparent in-sample predictive power often owes more to luck than to genuine predictive ability. The massive number of factors published, not to mention the countless more tested behind the scenes, demonstrates a quite exhaustive effort researchers have devoted to this quest. Facing this typical mutiple testing scenario, the traditional 1.96 t-statistic threshold no longer ensures a 5% Type I error rate. 

The bootstrap method discussed previously comes as an attempt to mitigate this problem. By combining a customized orthogonalization technique, which sets up a purified null hypothesis that holds by design, with bootstrapping, researchers can establish more reliable status quo for statistical test. While not a perfect resolution - we are still subject to a sample of smaller size compared to number of factors with evolving distribution, it’s certainly a solid starting point.

Time to pcontinue our exploration! With hundreds or even thousands of factors (what Cochrane called the 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), there are plenty more observations, challenges and models to discuss! 

Looking a little closer into this massive collection of factors, each claiming to predict security returns, it doesn't quite align with the conventional wisdom of investment community: predicting expected returns is really difficult. If these documented factors truly possess even modest predictive power, we’d be well-equipped to forecast returns by combining them together. Yet, it isn’t the case. Something seems off about this 'Factor Zoo' and it’s definitely worth a bit digging. 

What can we take from the factor zoo? How should we interpret it? In this blog, let's start this quest by checking out two opposing views around it. 

### The Skeptical and The Optimistic <a name="two"></a>

In the paper "Replicating Anomalies", Hou, Xue & Zhang (2020) shed some lights into the factor zoo. Quite remarkably, they replicated nearly 200 published factors and tested them using a comprehensive dataset of US stock market (1967–2016). Each factor's predictive power was evaluated under consistent test procedures for three horizons (1, 6, and 12 months) through sorted long-short portfolios. The finding was bitter: 65% of the factors failed to surpass the traditional t-statistic threshold of 1.96. The failure rate further climbed to an astonishing 82% when a stricter threshold of 2.78 accounting for multiple testing corrections was used.

Why such dismal replication rates? The authors believe one of the key driver is the excessive emphasis on illiquid micro-cap stocks in earlier factor research. Many factors show much stronger predictive power among stocks of smaller size，likely due to the lower levels of investor attention recevied and higher transaction costs required to arbitrage. These micro-cap stocks can account for as much as 60% of the total number of stocks but as little as 3% of the total market capitalization, representing investment opportunity with questionable capacity and profitability. Obviously, weighting these micro-cap stocks equally as the other 97% in factor portfolio construction or regression as some previous factor research did would create a big imbalance and distort the conclusion more favorable toward significance.

Another key driver of the low replication rate, probably equally important, lies in the dataset used. The 50-year dataset of US security returns is much more comprehensive than the majority of data sets used in earlier factor studies. In the financial market with inherently low signal-to-noise ratio, it’s not surprising for a factor to perform well in localized samples but fail in broader datasets. It is especially the case when there are incentives to customize the sample to achieve more significance for publication. 

There is also a much more optimistic angle in this discussion. In the article "Is There a Replication Crisis in Finance", Jensen, Kelly, and Pedersen (2023) offered a contrasting view. Using an even broader dataset spanning 93 countries with their innovative Bayesian testing framework, they reached a significantly different result: a 82% replication success rate.

82% vs 35%! How could the outcomes diverge so dramatically? Jensen et al. looked into this interesting  discrepancy themselves. As summarized in the chart below, several key differences in the test procedure and data set are behind this discrepancy. 

![GDP](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/replication.jpg)
Source: Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance

First and probably foremost, 





Obviously the different data sets used account for a significant , Jensen et al. switched from raw factor return to CAPM alpha, which alone increased the replication rate by over 20%. This adjustment makes some sense since the goal of factor research is to identify additional improvements beyond the market beta. However, it also introduce some unintentional distortions. For example, for the low volatility factor, the original intend is to see whether stocks with lower volatility outperform the others. While when regressing out the market return to the CAPM alpha, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. 

A lot more drivers are behind this sharp increase in successful rate. Like, Jensen et al uses a capped value weight in factor portfolio construction to avoid concentration in mega stocks. The market cap of a stock is capped at 80% percentile hence all stocks with size beyond this point would be assigned this 80% percentile value. Additionaly, they are using a much longer history in US stock even compared to Hou et al's already extensive data set. Rather than looking into 3 horizons of 1 month, 6 month and 12 months, they exclusively focused on the 1 month horizon. Their innovative bayesian modeling also leads to some degree of difference.






65%, 82%



Or to make things simpler, just raise the bar of the t-statistic to account for this much lossened selection! For instance, Hou, Xue & Zhang (2020) adpoted a 2.78 t-statistic for the 5% confidence level to account for this multiple testing problem. 




### And More <a name="more"></a>

We have seen two contrasting views, each bears merits of the analysis. What can we take.



### Reference <a name="ref"></a>
- Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance
- Hou, Xue & Zhang (2018): Replicating Anomalies
- Cohcrane (2011): Discount Rates
