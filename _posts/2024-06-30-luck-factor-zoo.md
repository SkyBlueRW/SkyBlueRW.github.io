#

## The Adjustment for Luck!

- [Introduction](#introduction)
- [A multiple testing problem](#mul)
- [The anticipated volatility and the market take](#info)
- [Appendix](#appendix)
- [Reference](#ref)

### Introduction <a name="introduction"></a>

![Lucky_Sharpe](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/lucky_sharpe.png)

As the Nobel Laureate Ronald Coase once said: "If you torture data long enough, it will confess to anything".

It starts with the million dollar question - What factors explain security expected return? Ever since Fama & French's empirical work on the 3 factor model unleashed the new era of empirical asset pricing in the 90s, hundreds (if not thousands) of factors claimed to predict cross sectional or time series security return emerged in acamdeic and insutry research materials. While even with this many factors at our diposal, we are not really in an ideal position to predict security expected return in real world investment! quite some of these facotrs, despite their great in-sample perfomance (hence the publication), deteriorate the performance significantly out of the sample.

Pontiff & McLean (2016) used to followed up on the out of sample and post publication performance of ~100 cross sectional factors. Quite sadly, on average, the factor returns shrank 26% out of the sample used in the correpsonding paper and 58% post the publication. Despite all the dicussion or even debats about if it means a replicating crisis in financial literature, the deteriorating out-performance were indeed observed for a lot of factors documented. There can be a lot of reasons behind the curtain, each worthy a comprehensive discussion. In this blog, we will focus on one quite interesting aspects of the issue - a good historical performance due to luck and a logical fail afterward.

How good should one factor perform so that we are comfortable to declare statistical significance accounting for the turbulance of luck? That's the question we want to dive into in this blog along side with the resample statistical procedure that Harvey & Liu introduced to address this bias in their famous paper 'Lucky factors'.



### A Multiple Testing Problem <a name="mul"></a>

As bizzare as it might sounds at the first place, given the large number of candidate factors people tried, a significant number of them are meant to cross the finish line of publication due to luck! It's actually quit intuitive. Imagine someone without any special skill in tossing a fair coin. We would not expect him or her to toss 10 consecutive heads in a row - a low probability event (0.1%). While out of 10 thousand people replicating the same experiments, it's really not a surprise to see a few lucky guy achieve this low probability event out from luck! (the expected number is around 10).

Let's firstly put it in a formal statistical context for further discussion.


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


