

#

## The "Maximum Diversification Frontier"

- [Introduction](#introduction)
- [MD Portfolio: the theoretical underpings](#why)
  - [Let's go for diversification](#subparagraph1)
  - [Anything special for strategic asset allocation?](#subparagraph2)
  - [The frontier part](#subparagraph3)
- [How's the performance for the past decade](#perf)
- [Reference](#ref)

  ### Introduction <a name="introduction"></a>


In the previous blog post [The Conviction Pyramid of Portfolio Construction](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html#risk), we embarked on an exploration of diverse portfolio construction methods, each tailored to different levels of market information availability. One such method we discussed (and I found very handy in quite some applications) is the Maximum Diversification (MD), which aims to achieve maximum diversification in terms of correlation. Such a method is a direct application of the notion of diversification for efficient risk premium harvest and provides much more flexibility in integrating optimization constraints compared to its closely related couterpart Risk Parity (RP). 

Expanding our exploration of MD, this blog post will take a closer look at its **application in strategic asset allocation**. We will examine the underlying theoretical foundations and assumptions that contribute to the maintenance of a consistent long-term balance between risk and return within MD. More importantly, we will explore MD at various volatility targets to construct an achievable "Maximum Diversification Frontier" and examine its performance in the markets of US, Eurozone, Japan, and China.

Prepare to be intrigued as we reveal the fascinating interplay between MD and risk targets across the past decades in these four markets. The resulting "Maximum Diversification Frontier" showcases an upward frontier, depicting the increasing realized risk and return at corresponding risk targets. Hence as a parrallel of the efficient frontier (probably also intersect at some points), I have the blog named as "Maximum Diversification Frontier". 

![MD Frontier](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/MD_Frontier.png)


### MD Portfolio: the theoretical underpings <a name="why"></a>

#### Let's go for diversification ! <a name="subparagraph1"></a>


Diversification is the old wisdom since the begining of the modern portfolio theory. As Nobel Prize laureate Harry Markowitz is reported to have said, “diversification is the only free lunch” in investing. It is believed that in a rational market under long term perspective, only the non-diversifiable systematical risk (those covaries with stochastic discount factor, consumption, etc...) is rewarded with expected return. Hence efficient diversification reducing idiosyncratic risk (at least in a unconditional context without further information) is deemed as granted to improve risk adjusted return.

Bearing such notion, MD is introduced to explore the un-perfect correlation of securities in the universe. More formally, it maximize the diversification ratio defined as weighted average volatility over the portfolio volatility. The ratio can be as large as 1 in the case all securities move exactly. With diversification ratio as optimization object, MD portfolio overweight securities having low correlation with others leading to a quite intuitive and direct implementation of diversification.

$$
\begin{aligned}
Max_{w} & \dfrac{w^T \sigma}{\sqrt{w^T \Sigma w}} \\
w^T 1 &= 1
\end{aligned}
$$

#### Anything special for strategic asset allocation? <a name="subparagraph2"></a>


Is there any futher rationale other than the fact that MD is a result of direct implementation of diversification? For sure there is, especially in the context of strategic asset allocation. In our previous [discusion](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html#risk), we noted that for a portfolio to be MD, every pair of securities within the portfolio should hold for the following conditions

$$
\begin{aligned}
\dfrac{1}{\sigma_i} \dfrac{\partial \sigma_p}{\partial w_i} &= \dfrac{1}{\sigma_j} \dfrac{\partial \sigma_p}{\partial w_j}
\end{aligned}
$$

as a contrast, the maximum sharpe ratio diversification requires the following conditions

$$
\begin{aligned}
\dfrac{1}{r^{e}_i} \dfrac{\partial \sigma}{\partial w_i} &= \dfrac{1}{r^{e}_j} \dfrac{\partial \sigma}{\partial w_j} \\
\end{aligned}
$$

Combining the two, it is essentially saying that MD is the Maximum Sharpe Ratio portfolio if expected return is linearly proportional to its volatility for every security in the universe. We grab the holy grail with MD! 

Believe me, this balance relationship between return and volatility is not some crazy illution in the allocation of asset classes. There is not a definitive conclusion if asset classes should share the same sharpe ratio. While the assumption that asset classes have comparable return volatility ratio is generally recogonized for good making MD at least a reasonable choice in asset allocation. Asset classes (equity, fixed income, commodity, etc ...) are generally well diversified. In a long term horizon, investors would flush into the asset class with extraodinary return compared to its volatility as risk adjusted return is what they commonly look for. The capital flow would simply hike price of the asset class hence reducing its risk adjusted return to a comparable level of other asset classes.

It is generally the case for the past 20 years (bear with the poor drawing of the green line)

![Historical Perf](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/historical_perf.png)

*Source: [Bankeronwheels.com](https://www.bankeronwheels.com/the-long-game-historical-market-returns-2022-expectations/)*

It is also the case in the long term capital market expectation forecast for institutional investors. (Below is the one from BlackRock)

![CMA](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/BLK_CMA.png)

*Source: [www.blackrock.com](https://www.blackrock.com/institutions/en-us/insights/charts/capital-market-assumptions)*

In both charts, asset classes clustered around a straight line. Asset classes share comparable return to volatility ratio, making MD a reasonable choice in asset allocation.


#### The frontier part <a name="subparagraph3"></a>


What about the frontier part in the title? It originates from the great flexibility that MD optimization can incorporate. For any given feasible set of the universe, there should be at least one portfolio with maximized diversification ratio as it's a relative metric. With such a feature, we can easily incorporate other optimization constraints in the MD optimization, of which I found the risk target optimization as a great match. 

To me, such a MD optimization coupled with risk targets is an intuitive implementation of the idea firstly position us within the region where risk is bearable and then make efficient use of the risk taken for reward.

### How's the performance for the past decade <a name="perf"></a>

Let's cut further words and see how it performs in some major markets (US, Eurozone, Japan, China). 

The market value weighted equity indexes, aggreagate bond indexes and commodity indexes from S&P are used throughout the following backtest analysis. S&P indexes are used here as their index levels are freely available at their [website](https://www.spglobal.com/spdji/en/index-family/equity/). While it is such a pitty that their data only covers the past decade. From a perspective of strategic asset allocation, 10 year is probably just a little longer than a 'blink'. 

In each market, MD portfolio is optimized with volatility target ranging from 3% to 13% with the following set up. 

$$
\begin{aligned}
Max_{w} & \dfrac{w^T \sigma}{\sqrt{w^T \Sigma w}} \\
w & > 0 \\
w^T 1 &<= 1 \\
\sqrt{w^T \Sigma w} & = \sigma_{target}
\end{aligned}
$$

For sure other constraints for risk, regulation, etc can be incorporated as well. While here just for illustration purpose, I will keep it short and simple. In each market, the covariance matrix is estimated with exponential weighted sample covariance matrix on daily return with halflife of 126. The portfolios are optimized and rebalanced quarterly starting from 2015 (with first 2 years for parameter estimation) to 2023.

The final results of all backtests are displayed in the chart of the very begining of the blog. I have also list the detailed performance in the table below here "MD @ x Risk" represents the MD portfolio given x volatility target. As imagined in the first place, MD provides a reasonable solution as strategic asset allocation. I would like to hilight the following two points specifically

1. The volatility target is effective that all portfolios' volatility is bounded close to their volatility targets. With only local information used at each rebalancing, we are able to managing long term volatility effectivly. It is likely due to the clustering and long term mean reversion characteristic universal in all kinds of volatilities.
2. As we increase the volatility target, the final expected return also increase at a relatively stable fasion. In my opinion, it is one indirect sign that the risk is used rather efficiently hence additional risk taking can bring futher reward.

This MD with risk target method, in my opinion serves well as the starting point for asset allocation. Specifically it should be quite handy for asset only investors without much constraint in matching durations or cash flows or so. In the case a set of solutions with different volatility level can be provided to suit the specific demands from products and clients.


<table border="1" class="dataframe">  <thead>    <tr>      <th></th>      <th colspan="2" halign="left">US</th>      <th colspan="2" halign="left">Eurozone</th>      <th colspan="2" halign="left">Japan</th>      <th colspan="2" halign="left">China</th>    </tr>    <tr>      <th></th>      <th>Annualized STD</th>      <th>Annualized Ret</th>      <th>Annualized STD</th>      <th>Annualized Ret</th>      <th>Annualized STD</th>      <th>Annualized Ret</th>      <th>Annualized STD</th>      <th>Annualized Ret</th>    </tr>  </thead>  <tbody>    <tr>      <th>MD @ 3% Risk</th>      <td>3.59</td>      <td>2.61</td>      <td>3.47</td>      <td>0.74</td>      <td>3.19</td>      <td>1.55</td>      <td>3.08</td>      <td>3.77</td>    </tr>    <tr>      <th>MD @ 4% Risk</th>      <td>4.77</td>      <td>3.01</td>      <td>4.52</td>      <td>1.06</td>      <td>4.20</td>      <td>2.13</td>      <td>4.10</td>      <td>4.17</td>    </tr>    <tr>      <th>MD @ 5% Risk</th>      <td>5.89</td>      <td>3.66</td>      <td>5.55</td>      <td>1.43</td>      <td>5.22</td>      <td>2.57</td>      <td>5.11</td>      <td>4.54</td>    </tr>    <tr>      <th>MD @ 6% Risk</th>      <td>7.01</td>      <td>4.13</td>      <td>6.57</td>      <td>1.83</td>      <td>6.25</td>      <td>2.97</td>      <td>6.12</td>      <td>4.89</td>    </tr>    <tr>      <th>MD @ 7% Risk</th>      <td>8.06</td>      <td>4.81</td>      <td>7.59</td>      <td>2.25</td>      <td>7.29</td>      <td>3.34</td>      <td>7.13</td>      <td>5.18</td>    </tr>    <tr>      <th>MD @ 8% Risk</th>      <td>9.01</td>      <td>5.32</td>      <td>8.61</td>      <td>2.64</td>      <td>8.34</td>      <td>3.68</td>      <td>8.14</td>      <td>5.43</td>    </tr>    <tr>      <th>MD @ 9% Risk</th>      <td>10.17</td>      <td>5.55</td>      <td>9.57</td>      <td>3.19</td>      <td>9.40</td>      <td>4.00</td>      <td>9.16</td>      <td>5.56</td>    </tr>    <tr>      <th>MD @ 10% Risk</th>      <td>11.29</td>      <td>6.10</td>      <td>10.63</td>      <td>3.45</td>      <td>10.52</td>      <td>4.27</td>      <td>10.16</td>      <td>5.64</td>    </tr>    <tr>      <th>MD @ 11% Risk</th>      <td>12.49</td>      <td>6.91</td>      <td>11.67</td>      <td>3.97</td>      <td>11.49</td>      <td>5.42</td>      <td>11.11</td>      <td>5.90</td>    </tr>    <tr>      <th>MD @ 12% Risk</th>      <td>13.44</td>      <td>7.86</td>      <td>12.60</td>      <td>4.55</td>      <td>12.37</td>      <td>6.46</td>      <td>12.03</td>      <td>6.21</td>    </tr>    <tr>      <th>MD @ 13% Risk</th>      <td>14.35</td>      <td>8.77</td>      <td>13.29</td>      <td>4.76</td>      <td>13.20</td>      <td>7.33</td>      <td>12.92</td>      <td>6.50</td>    </tr>    <tr>      <th>RP</th>      <td>4.27</td>      <td>2.50</td>      <td>4.15</td>      <td>0.57</td>      <td>2.16</td>      <td>0.89</td>      <td>1.60</td>      <td>4.78</td>    </tr>    <tr>      <th>60/40-Equity/Bond</th>      <td>11.16</td>      <td>7.24</td>      <td>10.92</td>      <td>3.71</td>      <td>10.02</td>      <td>4.12</td>      <td>15.10</td>      <td>6.50</td>    </tr>  </tbody></table>




### Reference <a name="ref"></a>
- Choueifaty & Coignard (2008): Toward Maximum Diversification
