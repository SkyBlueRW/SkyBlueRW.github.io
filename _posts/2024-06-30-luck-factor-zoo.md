#

## The Adjustment for Luck!

- [Those Factors shrink out of sample](#introduction)
- [A multiple testing problem](#mul)
- [A Resample Procedure to account for luck](#resample)
- [Appendix](#appendix)
- [Reference](#ref)

### Those Factors Shrink out of sample <a name="introduction"></a>


As Nobel Laureate Ronald Coase once said: "If you torture data long enough, it will confess to anything".

It starts with the million dollar question in finance and investment - What factors explain security expected return? Ever since the 90s when Fama and French's empirical work on the 3 factor model unleashed a new era of empirical asset pricing, hundreds (if not thousands) of factors have emerged in academic and industry research, each claiming to predict cross-sectional or time-series security returns. While despite this plethora of factors (John Cochrane calls it a factor zoo), predicting security expected returns in real-world investments remains a challenging task. Many of these factors, despite demonstrating strong in-sample performance (which lead to their publication), significantly underperform out-of-sample.

For example, Pontiff and McLean (2016) examined the out-of-sample and post-publication performance of around 100 cross-sectional factors from academic research. Unfortunately, they found that, on average, factor returns shrank by 26% out-of-sample and 58% post-publication. Hou, Xue & Zhang (2020) further exapeded this exercises to a total of 452 factors published and found that for as much as 65% of them,  t-statistics drop below 2 out of sample.

Let's leave alone all the dicussion and debates about potential replicating crisis in asset pricing literature for the moment, deteriorating out sample performance was indeed observed for a lot of factors published. Why is it the situation? The reasons behind this performance deterioration out of sample are numerous and complex, each deserving thorough research and discussion. In this blog we will try to discuss about one particularly interesting aspect of the problem: those "lucky factors" selected only because of test multiplicity from a large number of candidate factors. Likely, they would not continue the luck in a new sample!

Obviously, to improve our chance of expected return prediction, we hope to select factors that genuinly means something and are likely to maintain their predictive power out of sample. These lucky factors are what we hope to avoid in the modeling of expected return. To this goal, how can we adjust our factor research framework for the existence of lucky factors and how good should one factor perform so that we are comfortable to declare its statistical significance accounting for the turbulance of luck. That's the question that we hope to discuss in this blog. Specifically I hope to introduce to your attention the resample statistical procedure from paper "Lucky Factor" (Harvey & Liu, 2021). Given a pool of candidate factors, such a statistical procedure is quite helpful in evaluating marginal improvement on adding factors to existing factor models while also accounting for the lucky factor problem.


### A Multiple Testing Problem <a name="mul"></a>

What is this 'lucky factor' problem? It originates from the single hypothesis tests used for large number of candidate factors experimented without accounting for test multiplicity. 

When evaluating the performance of a single factor, we recognize its significance while accepting a small probability of false discovery. We test the null hypothesis that the expected return of the factor is zero. If this null hypothesis is not supported by the data, the factor is considered significant. A p-value is calculated to compare against a threshold, determining how compatible the null hypothesis is with the data. In the context of single hypothesis testing, a 5% p-value means there is a 5% risk of false discovery if we deem the factor significant.

However, this logic does not hold when many factors are tested. Imagine identifying one factor with a p-value of 5% — right at our threshold — after 399 unsuccessful attempts. The risk of accepting this 400th factor is no longer 5%. This is because, even if all 400 factors have an expected return of zero, randomness alone would give a probability greater than 99% of finding at least one factor with a p-value below 5%—these are the 'lucky' factors. Repeat the test 400 times do not do not properly describe our null hypothesis anymore. 

Unfortunately, this scenario is common in factor research. In the sparkling financial markets, hundreds of thousands of researchers have tested countless factors for predictive power using similar data sets. They generally use a p-value threshold of 1% or 5% under the single hypothesis test framework, leading to significant multiple testing issues. With so many factors tried, a factor showing strong in-sample predictability by the standards of single-factor testing is quite likely a result of random chance rather than genuine predictive power.


### A Resample Procedure to account for luck <a name="resample"></a>

enforce the null hypothesis to the context. alows for iteration to have an existing model set as null and then evaluate the incremental contribution.


![Lucky_Sharpe](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/factor_zoo_bootstrap.png)



The other day, I was watching a documentary video that tells the story of a future trader who acheived 2500%+ profit within 5 years since 2019. Quite a magnificent financial reward! Though even the trader himself admitted, he, in some degree, lived under the shadow of anxiety about continuity of making profits via trading - it's hard to determine whether the previous performance arises from exceptional skill or luck. Actually the balance might tilt a bit more toward the latter, considering the fact that almost all of his parterners exiting trading the way like him due to unbearable losses.

Do traders/portfolio managers/factors' nice historical performance come from something meaningful hence likely to continue in the future? This is definitely a million dollar question, with quite some hurdles to get a solid answer. As a matter of fact, deep in our hear, we know that it happes when a factor or trader with top the nouch historical performance fail. There can be really a lot reasons behind the curtain, each worthy for comprehensive discussion. In this blog, we will focus on one quite interesting scenario that can lead to it - a good historical performance due to luck in randomness and a logical fail afterward.



In the volatile financial market crowdeded with all kinds of participants, such temporary success from luck is not rare unicorn. It's like to have 10000 people tossing a fair coin for 10 times. It's expected to see some of them have 10 consecutive head toss even though they do not have special skill in tossing a head - they are not expected to replicate such results!

whether this factor/trader/pm with

Back in 90s, the publish of Fama French factor model unleash an era of factor research. Ever since, tens of thousands of factors claimed to predict cross sectional security return variations are published in all kinds of articles 
And it shouldn't be a surprise. Standing at 2024, the traditional data set such as market and fundamental data are investigated by too many researchers for too many trials. Quite naturally, tons of factors claimed to predict cross sectional security returns are there.

















It's really not a rare situation in investment research, that one read into a new paper detailing about a new anomaly that can predict the cross sectional stock return. You try to replicate it and enhance it in terms of a alpha signal with the arsenal of all kinds of modification. While it does not work out of sample in a paper trading despite the amazing performance delivered historically. What's wrong?

actually, there are hundreds of factors claim to predict cross-section stock return. A lot of times, (quantitative) investors would have trading signal 


When we research the data set intensively and experiments hundreds of factors, the baseline is no more none of them work. Significant result can emerge just out of randomness. Take the coin toss guess as analogy, it's quite unlikely for one people to guess correctly for 10 consecutive times of coin toss, while if we find 10 thousands people, it is not surprising to see a few of them are able to guess correctly out of luck not from skills in guessing coin toss.

simulation. 

Lasso, explicit account for multiple testing, achieve null hypothesis with the data observed

With pre-determined factors (not necessary), how to identify if a candidate facotr perform taking luck into account

what's p value?

Pontiff & McLean (2016) 26% lower out-of-sample and 58% lower post-publication

1 - (1 - \alpha) ^ k

central limiet theorem distribution of empirical mean. 

Bootstrap

identify 'true' factors sequentially.

V
https://mp.weixin.qq.com/s/QOdTdKjNE838FoM71gYJew
https://www.stat.cmu.edu/~larry/=sml/Boot.pdf

If you torture the data long enough, it will confess to anything. Ronald Coase

### Reference <a name="ref"></a>
- Harvey & Liu (2021): Lucky factor
- Pontiff & McLean (2016): Does Academic Research Destroy Stock Return Predictability?
- Hou, Xue & Zhang (2020): Replicating anomalies


