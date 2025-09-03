
## Navigating the Factor Zoo!

- [From Factors to Managed Portfolios](#portfolio)
- [The Classic](#classic)
- [The Bayesian Len](#bayes)
- [Reference](#ref)

In the previous blog, [A First Glimpse into the "Factor Zoo"](https://skybluerw.github.io/2024/12/07/factor-zoo.html), we took a bird’s eye view of the empirical evidence and saw how drastically conclusions can swing given different datasets and portfolio construction choices. Replication debates aside, it’s time to step closer and look at how factor evaluation and modeling actually work.

At the heart of empirical factor research sits a straightforward yet stubborn question: "Is this factor's return statistically different from zero, and is it economically meaningful hence likely to persist?". It's no surprise that investors care about more than mean and variance of return when judging factors and associated expected returns. Extra looks at the distibution such as tail risk, time varying parameter, dependnce on the past can translate into a real world edge in investment. Even so, a Gaussian framework, uniquely defined by mean and variance remains a reasonable starting point, for its theoretical gounding and analytical tractability. That's exactly where we'll start this time.

In this blog, we'll try to unpack the nuts and bolts behind the modeling and evaluation. We start from the classic frequentist toolkit used in in empirical factor research and then explore the Bayesian framework that Jensen, Kelly & Pedersen (2023) recommended to add addtional structure and reduce variance. Even with machine learning thecniques in the spotlight nowadays, these structured econometric techniques and the market structures that they explicit still matter when samples are short, dimensions explode, and signals hide in noise - the everyday reality for much of what we face in financial markets.


### Building a "Managed Portfolio" <a name="portfolio"></a>

In its essence, factor research is a finance-specific way to approach prediction tasks. In almost every factor study, well see a regularly rebalanced long–short portfolio built from lagged security (or issuer) characteristics, and then all analysis is run on that portfolio’s return — a managed portfolio meant to represent the factor. 
