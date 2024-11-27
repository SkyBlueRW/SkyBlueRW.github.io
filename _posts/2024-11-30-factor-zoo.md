#

## A First Glimpse into the "Factor Zoo"

- [The Factor Zoo](#crisis)
- [The Skeptical and the Optimistic](#two)
- [And more](#more)
- [Reference](#ref)

### The Factor Zoo <a name="crisis"></a>


In a previous blog, [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we kicked off the discussion around identifying factors that drive cross-sectional security returns out-of-sample in the real world. Specifically, we talked about one critical challenge in this journey - the multiple testing problem. Basically, when factors are identified through extensive searches, their apparent in-sample predictive power often owes more to luck than to genuine predictive ability. The massive number of factors published, not to mention the countless more tested behind the scenes, demonstrates a quite exhaustive effort researchers have devoted to this quest. Facing this typical mutiple testing scenario, the traditional 1.96 t-statistic threshold no longer ensures a 5% Type I error rate. 

The bootstrap method discussed previously comes as an attempt to mitigate this problem. By combining a customized orthogonalization technique, which sets up a purified null hypothesis that holds by design, with bootstrapping, researchers can establish more reliable baselines for statistical tests. While not a perfect solution - we are still subject to a sample of smaller size compared to number of factors with evolving distribution, it’s certainly a solid starting point.

Time to pcontinue our exploration! With hundreds or even thousands of factors (what Cochrane called the 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), there are plenty more observations, challenges and models to discuss! 

Looking a little closer at this massive collection of factors, each claiming to predict security returns, it doesn't quite align with the conventional wisdom of investment community: predicting expected returns is really difficult. If these documented factors truly possess even modest predictive power, we’d be well-equipped to forecast returns by combining them together. Yet, it isn’t the case. Something seems off about this 'Factor Zoo' and it’s definitely worth digging into. 

What can we take from the Factor zoo? How should we interpret it? In this blog, let's start this quest by checking out two opposing views on the matter. 

### The Skeptical and The Optimistic <a name="two"></a>

In their paper "Replicating Anomalies", Hou, Xue & Zhang (2020) shed some lights on the factor zoo. Quite remarkably, they replicated nearly 200 published factors and tested them using a comprehensive dataset of US stock market (1967–2016). Each factor's predictive power was evaluated under consistent test procedures for three horizons (1, 6, and 12 months) through sorted long-short portfolios. The finding was sobering: **65% of the factors failed to surpass the traditional t-statistic threshold of 1.96**. The failure rate further climbed to an astonishing 82% when a stricter threshold of 2.78 accounting for multiple testing corrections, was used.

Why such dismal replication rates? The authors believe one of the key driver is the excessive emphasis on illiquid micro-cap stocks in earlier factor research. Many factors show much stronger predictive power among stocks of smaller size，likely due to the lower levels of investor attention recevied and higher transaction costs required to arbitrage. These micro-cap stocks can account for as much as 60% of the total number of stocks but as little as 3% of the total market capitalization, representing investment opportunities with questionable capacity and profitability. Weighting these micro-cap stocks equally as the other 97% in factor portfolio construction or regression as some previous factor research did would creates a significant imbalance and skews the conclusions more favorably toward significance.

Another equally important driver of the low replication rate lies in the dataset used. The 50-year dataset of US security returns is much more comprehensive than the majority of data sets used in earlier factor studies. In the financial market with inherently low signal-to-noise ratio, it’s not surprising for a factor to perform well in localized samples but fail in broader datasets. This is especially the case when there are incentives to customize the sample to achieve more significance for publication.

On the other side, there is also a much more optimistic angle in this discussion. In the article "Is There a Replication Crisis in Finance", Jensen, Kelly, and Pedersen (2023) offered a contrasting view. Using an even broader dataset spanning 93 countries with their innovative Bayesian testing framework, they reached a significantly different result: a **82% replication success rate**.

**82% vs 35%**! How could the outcomes diverge so dramatically? Jensen et al. delved into this intriguing discrepancy themselves. As summarized in the chart below, several differences in the test procedure and data set are behind this divergence in replication rate. 

![GDP](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/replication.jpg)
Source: Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance

First and probably foremost, factor returns are constrcuted quite differently. Instead of using the raw portfolio return of the long-short factor portfolio as Hou et al. did, Jensen et al. switched to the CAPM alpha, which is essentially the regression residual of the raw factor return over market portfolio. This change alone increased the successful rate by over 20%! 

Removing exposure to market beta definitely has its merits. After all, we hope to identify factors that can provide additional predictive power in addition to traditional factors like market beta.However, it's worth mentioning that it might introduce some unintentional distortions. For instance, when testing the low volatility factor, the original intend is to see whether stocks with lower volatility outperform the others. While when regressing out the market return to the CAPM alpha, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. We might be testing something different than we initially thought.

The rest of the increase in the replication rate can be attributed to various less impactful differences in test procedures and datasets. For example, Jensen et al. chose to use capped market value weights in factor portfolio construction to avoid excessive impact from mega-cap stocks. They also focused exclusively on the 1-month holding horizon and utilized a longer data set. 

### And More <a name="more"></a>

Now that we've acknowledged the existence of the Factor Zoo and checked out how different the replication results can be. Our impressions of the validity of factors can vary significantly depending on the test procedures adopted and the datasets examined. The way factors are built and tested can lead to different empirical results about their effectiveness and reliability. What can we take from it?

Obviously, from investors' perspective, the construction of factor portfolios hence the test procedure isn't a one-size-fits-all process. It heavily depends on who the investor is, what their investment opporunity sets look like, and how sensitive they are to restrictions like transaction costs. As a result, investors can deploy dramatically different methods to gain factor exposures hence significantly different performance. For example, an asset owner looking to conduct long-term stragetic allocation won't find Jensen's exclusive focus on the 1 month horizon intriguing. Similarly, a hedge fund exploiting arbitrage with efficient trade execution will definitely find Hou et al.'s market value weighting scheme too restrictive. Judging from this anlge, there is not an absolute right or wrong in the comparison, different test procudures make sense to different investors. The point is more to have sense about the impact of decision made in test and have it consistent with real world portfolio construction. 

The difference arising from difference in datasets can be even trickier. Typically, statistical conclusions from a larger data set should provide us much more confidence hence Jensen et al's data set is in favor for its long history and wider coverage on financial markets globally. While this edge on confidence rely on the same distribution across history and markets. Under the same distribution, we can comfortably say that more data to more confidence. While it is not always the case in both dimmensions. market, time 

It's worth to mention, even though we have a multitude of factors at our disposal, this doesn't necessarily make predicting expected returns an easy task. Many factors share common ground in predicting returns, and adding more highly correlated factors doesn't contribute much additional predictive power. In fact, incorporating factors that are closely related can lead to redundancy and overfitting rather than improving the robustness of predictions.

The differences arising from datasets can be even trickier to navigate. Using a short historical period might not provide sufficient data to derive statistically significant results, while relying on a longer history introduces the issue of changing distributions over time. Markets evolve, and the relationships captured by factors may shift. This raises a crucial question: how do we link the past with the future? How can we gain confidence that a factor working in the past is likely to continue working in the future?

Perhaps one way to bridge this gap is to delve deeper into the economic channels and underlying assumptions behind each factor. Understanding the rationale and mechanisms that drive a factor's performance can provide insight into its potential persistence. If a factor is grounded in sound economic theory or reflects enduring behavioral biases, it may be more likely to remain effective over time.


### Reference <a name="ref"></a>
- Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance
- Hou, Xue & Zhang (2018): Replicating Anomalies
- Cohcrane (2011): Discount Rates
