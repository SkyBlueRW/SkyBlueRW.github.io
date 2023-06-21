

#

## The "Maximum Diversification Frontier"

- [Introduction](#introduction)
- [MD Portfolio: the theoretical underpings](#why)
- [Reference](#ref)

  ### Introduction <a name="introduction"></a>


In the previous blog post [The Conviction Pyramid of Portfolio Construction](https://skybluerw.github.io/2023/04/01/pyramid-optimization.html#risk), we explored different portfolio construction methods based on various availability of market information. One such method we discussed (and I found very handy in quite some applications) is the Maximum Diversification (MD), which aims to achieve maximum diversification in terms of correlation. Such a method is a direct application of the notion of diversification for efficient risk premium harvest and provides much more flexibility in integrating optimization constraint compared to its closely related friend Risk Parity (RP). 

Further diving into MD, this blog post will take a closer look at its **application in strategic asset allocation**. We will explore the theoretical foundations and assumptions of consistent long-term balance between risk and return that underpin MD. More importantly, we will explore MD at various volatility targets to construct an achievable "Maximum Diversification Frontier" and examine its performance in the markets of US, Eurozone, Japan, and China.

Prepare to be intrigued as we reveal the fascinating interplay between MD and risk targets across the past decades in these four markets. The resulting "Maximum Diversification Frontier" unveils an ascending line,  illustrating the increasing realized risk and return at corresponding risk targets. Hence as a parrallel of the efficient frontier (probably also intersect under some makret conditions), I have the blog named as "Maximum Diversification Frontier".

![MD Frontier](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/MD_Frontier.png)


### MD Portfolio: the theoretical underpings <a name="why"></a>


theoretical underpinnings consistent long-term relationship between risk and return. 



![Historical Perf](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/historical_perf.png)

*Source: [Bankeronwheels.com](https://www.bankeronwheels.com/the-long-game-historical-market-returns-2022-expectations/)*


![Historical Perf](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/asset_class_history.png)

![CMA](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/BLK_CMA.png)
*Source: [www.blackrock.com](https://www.blackrock.com/institutions/en-us/insights/charts/capital-market-assumptions)*


<table border="1" class="dataframe">  <thead>    <tr>      <th></th>      <th colspan="2" halign="left">US</th>      <th colspan="2" halign="left">Eurozone</th>      <th colspan="2" halign="left">Japan</th>      <th colspan="2" halign="left">China</th>    </tr>    <tr>      <th></th>      <th>Annualized STD</th>      <th>Annualized Ret</th>      <th>Annualized STD</th>      <th>Annualized Ret</th>      <th>Annualized STD</th>      <th>Annualized Ret</th>      <th>Annualized STD</th>      <th>Annualized Ret</th>    </tr>  </thead>  <tbody>    <tr>      <th>MD @ 3% Risk</th>      <td>3.59</td>      <td>2.61</td>      <td>3.47</td>      <td>0.74</td>      <td>3.19</td>      <td>1.55</td>      <td>3.08</td>      <td>3.77</td>    </tr>    <tr>      <th>MD @ 4% Risk</th>      <td>4.77</td>      <td>3.01</td>      <td>4.52</td>      <td>1.06</td>      <td>4.20</td>      <td>2.13</td>      <td>4.10</td>      <td>4.17</td>    </tr>    <tr>      <th>MD @ 5% Risk</th>      <td>5.89</td>      <td>3.66</td>      <td>5.55</td>      <td>1.43</td>      <td>5.22</td>      <td>2.57</td>      <td>5.11</td>      <td>4.54</td>    </tr>    <tr>      <th>MD @ 6% Risk</th>      <td>7.01</td>      <td>4.13</td>      <td>6.57</td>      <td>1.83</td>      <td>6.25</td>      <td>2.97</td>      <td>6.12</td>      <td>4.89</td>    </tr>    <tr>      <th>MD @ 7% Risk</th>      <td>8.06</td>      <td>4.81</td>      <td>7.59</td>      <td>2.25</td>      <td>7.29</td>      <td>3.34</td>      <td>7.13</td>      <td>5.18</td>    </tr>    <tr>      <th>MD @ 8% Risk</th>      <td>9.01</td>      <td>5.32</td>      <td>8.61</td>      <td>2.64</td>      <td>8.34</td>      <td>3.68</td>      <td>8.14</td>      <td>5.43</td>    </tr>    <tr>      <th>MD @ 9% Risk</th>      <td>10.17</td>      <td>5.55</td>      <td>9.57</td>      <td>3.19</td>      <td>9.40</td>      <td>4.00</td>      <td>9.16</td>      <td>5.56</td>    </tr>    <tr>      <th>MD @ 10% Risk</th>      <td>11.29</td>      <td>6.10</td>      <td>10.63</td>      <td>3.45</td>      <td>10.52</td>      <td>4.27</td>      <td>10.16</td>      <td>5.64</td>    </tr>    <tr>      <th>MD @ 11% Risk</th>      <td>12.49</td>      <td>6.91</td>      <td>11.67</td>      <td>3.97</td>      <td>11.49</td>      <td>5.42</td>      <td>11.11</td>      <td>5.90</td>    </tr>    <tr>      <th>MD @ 12% Risk</th>      <td>13.44</td>      <td>7.86</td>      <td>12.60</td>      <td>4.55</td>      <td>12.37</td>      <td>6.46</td>      <td>12.03</td>      <td>6.21</td>    </tr>    <tr>      <th>MD @ 13% Risk</th>      <td>14.35</td>      <td>8.77</td>      <td>13.29</td>      <td>4.76</td>      <td>13.20</td>      <td>7.33</td>      <td>12.92</td>      <td>6.50</td>    </tr>    <tr>      <th>RP</th>      <td>4.27</td>      <td>2.50</td>      <td>4.15</td>      <td>0.57</td>      <td>2.16</td>      <td>0.89</td>      <td>1.60</td>      <td>4.78</td>    </tr>    <tr>      <th>60/40-Equity/Bond</th>      <td>11.16</td>      <td>7.24</td>      <td>10.92</td>      <td>3.71</td>      <td>10.02</td>      <td>4.12</td>      <td>15.10</td>      <td>6.50</td>    </tr>  </tbody></table>




### Reference <a name="ref"></a>
- Choueifaty & Coignard (2008): Toward Maximum Diversification
