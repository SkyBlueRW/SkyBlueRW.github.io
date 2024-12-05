#

## A First Glimpse into the "Factor Zoo"

- [The Factor Zoo](#crisis)
- [The Skeptical and the Optimistic](#two)
- [And more](#more)
- [Reference](#ref)

### The Factor Zoo <a name="crisis"></a>


In our previous blog, [The Adjustment for Luck](https://skybluerw.github.io/2024/06/26/luck-factor-zoo.html), we embarked on an exploration of how to identify factors that genuinely drive cross-sectional security returns out-of-sample in the real world. We focused on one critical challenge in this journey: the multiple testing problem. Essentially, when factors are identified through extensive searches, their apparent in-sample predictive power often owes more to luck than to true predictive ability. The massive number of factors published, not to mention the countless others tested behind the scenes, highlights just how exhaustive researchers have been in this quest. In the face of this typical multiple testing scenario, the traditional 1.96 t-statistic threshold no longer ensures a 5% Type I error rate.

The bootstrap method also discussed in that blog comes as an attempt to mitigate this problem. By combining a customized orthogonalization technique, which sets up a purified null hypothesis that holds by design, with bootstrapping, researchers can establish more reliable baselines for statistical tests. While it's not a perfect solution - we are still subject to a sample of smaller size compared to number of factors with evolving distribution, it’s certainly a solid starting point.

It's time to continue our exploration! With hundreds or even thousands of factors (what Cochrane called the 'Factor Zoo' in his [presidential address](https://www.nber.org/papers/w16972) to the American Finance Association), there is plenty more observations, challenges and models to discuss! 

Looking a bit closer at this massive collection of factors, each claiming to predict cross sectional security returns, we notice it doesn't quite align with the conventional wisdom in the investment community: predicting expected returns is really difficult. If these documented factors truly possessed even modest predictive power marginally, we'd be well-equipped to forecast returns by combining them. Yet, that's not the case. Something seems off about this 'Factor Zoo', and it's definitely worth digging into.

So, what can we take from the Factor Zoo? How should we interpret it? In this blog, let's start this quest by examining two opposing views on the matter.

### The Skeptical and The Optimistic <a name="two"></a>

First, let's consider the perspective offered by Hou, Xue, and Zhang (2020). In their paper 'Replicating Anomalies', they shed light on the Factor Zoo by undertaking the ambitious task of replicating nearly 200 published factors. Using a comprehensive dataset of the U.S. stock market spanning from 1967 to 2016, they evaludated each factor's predictive power under the same test procedures of sorted long-short portfolios across three investment horizons (1, 6, and 12 months). The findings were sobering: **65% of the factors failed to surpass the traditional t-statistic threshold of 1.96**. When a strcter threshold of 2.78 was applied to account for multiple testing corrections, the failure rate climbed further to an astonishing 82%!

Why such dismal replication rates? The authors believe one of the key driver is the excessive emphasis on illiquid micro-cap stocks in earlier factor research. Many factors show much stronger predictive power among smaller stocks，likely due to the lower levels of investor attention they recevie and higher transaction costs required to arbitrage them. These micro-cap stocks can account for as much as 60% of the total number of stocks but as little as 3% of the total market capitalization, representing investment opportunities with questionable capacity and profitability. Weighting these micro-cap stocks equally as the other 97% in factor portfolio construction or regression as some previous factor research did creates a significant imbalance and skews the conclusions more favorably toward significance.

Another equally important driver contributing to the low replication rate lies in the dataset used. Hou, Xue, and Zhang utilized a 50-year dataset of U.S. security returns, which is much more comprehensive than the datasets employed in many earlier factor studies. In the financial market with an inherently low signal-to-noise ratio, it's not surprising for a factor to perform well in localized samples but falter in broader datasets. This is especially true when there's an incentive to customize the sample to achieve greater significance for publication.

There's also a much more optimistic angle to this discussion. In their article "Is There a Replication Crisis in Finance", Jensen, Kelly, and Pedersen (2023) offered a contrasting perspective. Utilizing an even broader dataset spanning 93 countries and applying their innovative Bayesian testing framework, they reached a significantly different result: an **82% replication success rate**.

**82% vs 35%**! How could the outcomes diverge so dramatically? Jensen et al. delved into this intriguing discrepancy themselves. As summarized in the chart below, several differences in  test procedure and datasets are behind this divergence in replication rates. 

![GDP](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/replication.jpg)
Source: Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance

First and perhaps most importantly, the construction of factor returns differs significantly between the two studies. Instead of using the raw returns of the long-short factor portfolios, as Hou et al. did, Jensen et al. opted to use the CAPM alpha, which is essentially the regression residual of the raw factor return over market portfolio. This change alone increased the successful rate by over 20%! 

Removing exposure to market beta definitely has its merits. After all, we are aiming to identify factors that can provide additional predictive power in addition to traditional ones like market beta. However, it's important to note that this approach might introduce some unintended distortions. For instance, when testing the low volatility factor, the original intend is to evaluate whether stocks with lower volatility outperform the others. While when regressing out the market return to the CAPM alpha, it actually turns the low volatility factor into something similar to the betting against beta factor - a distinct factor. We might be testing something different than we initially thought.

The rest of the increase in the replication rate can be attributed to various less impactful differences in test procedures and datasets. For example, Jensen et al. chose to use capped market value weights in factor portfolio construction to avoid excessive impact from mega-cap stocks. They also focused exclusively on the 1-month holding horizon and utilized a longer data set. 

### And More <a name="more"></a>

Now that we've acknowledged the existence of the Factor Zoo. It's clear that our impressions of the factors from it can vary significantly depending on the test procedure adopted and the datasets examined. The way factors are built and tested can lead to different empirical results regarding their effectiveness and reliability. So, what can we take from this?

Obviously, from investors' perspective, the construction of factor portfolios hence the test procedure isn't a one-size-fits-all process. It heavily depends on who the investor is, what their investment opporunity sets look like, and how sensitive they are to restrictions like evaluation horizon and transaction costs. As a result, investors can deploy dramatically different methods to gain factor exposures, leading to significantly different performance outcomes. 

For example, an asset owner looking to conduct long-term strategic allocation might not find Jensen et al.'s exclusive focus on the 1-month horizon particularly relevant. Similarly, a hedge fund exploiting arbitrage with efficient trade execution might find Hou et al.'s market-value weighting scheme too restrictive. From this angle, there's no absolute right or wrong in the comparison; different test procedures make sense to different investors. The key is to understand the impact of decisions made in testing and ensure they are consistent with real-world portfolio construction.

However, this doesn't mean investors who share similar investing procedures to Jensen et al. should celebrate the promising prospect suggested by the 82% replication rate. They are still not in a position to throw in hundreds of "working" factors and boom a great forecast of future security returns emerges. Many factors share common ground in predicting returns, and adding highly correlated factors doesn't contribute much additional predictive power. In fact, in Jensen et al.'s hierarchical Bayesian model, factors are modeled with shared sources of predictive power to account for this point. They grouped all the factors into 13 categories, within which factors share quite high correlations.

It becomes even trickier when it comes to differences in datasets used for testing. Typically, statistical conclusions from a larger dataset should provide more confidence; hence, Jensen et al.'s dataset might be favored for its long history and wider coverage of global financial markets. However, this edge in confidence relies on the assumption of the same or similar distribution across history and markets. This isn't always the case in either dimension. Market movements from 70 years ago during World War II might not provide much insight into how investors should invest today. Also, it's not surprising to find that different financial markets around the globe operate under different structures.

And that's still not the end of the problem list. Even if we magically figure out a legit dataset and draw statistical significance with test procedures highly consistent with what would be done in real world invsting, Will it still hold true tomorrow? 

How can we link actions to take in the future to data observed in the past? This is probably the biggest challenge (definitely one big puzzle to me) in forecasting security returns. There may not be a perfect or even a good enough way to bridge the gap. What investors typically take advantage of is that there is generally a phase of change, even for a volatile system like the financial market. It won't change 180 degrees all of a sudden; hence, we can still use relevant information from the near past. Additionally, this highlights the benefit of a structural model instead of relying solely on empirical results. With clearly defined assumptions and logical chains, we're better guided in understanding what's happening and what's not.


### Reference <a name="ref"></a>
- Jensen, Kelly & Pedersen (2023): Is There a Replication Crisis in Finance
- Hou, Xue & Zhang (2018): Replicating Anomalies
- Cohcrane (2011): Discount Rates
