
## Correlation

- [From Factors to Managed Portfolios](#portfolio)
- [The Classic](#classic)
- [The Bayesian Len](#bayes)
- [Reference](#ref)


Stock-bond correlation is one of the oldest topics in asset allocation, and it keeps coming back for a reason. 

For decades, bonds have played the role of natural diversifier in investors' portfolios, nurturing traditional allocations like the 60/40. Correlations also move slowly compared to returns or volatility, making them more stable estimate to anchor strategies like risk parity and maximum diversification.

But none of this is given as granted. Since the pandemic, stock-bond correlation has flipped positive for the first time in twenty years with a continuing momentum. The diversification a stock-bond portfolio is supposed to deliver is fading, and strategies that rely on stable correlations are under real pressure. It's a good time to revisit this old question.

There is no shortage of well rooted models for the estimation of correlation. DCC-GARCH decomposes a covariance matrix to volatility and correlation for their different dynamics. Regime switching and hierachical clustering models try to enhance and capture a nonlinear aspect of the association. Even a plain rolling sample correlation works reasonably well for the slow moving nature of correlation. But when I want to actually make sense of stock-bond correlation, the mental model I keep coming back to is from Ilmanen's 2003 paper.

The model starts from a surprisingly simple and intuive place: the discounted cash flow framework. Both stocks and bonds, like any other asset, are priced as the expected present value of their future cash flows.

$$
\begin{aligned}
P_{\text{stock}} &= E[\sum_{t=1}^{\infty} (\dfrac{1+G}{1 + Y_t + \text{ERP}_t})^t D] \\
P_{Bond} &= E[\sum_{t=1}^T \dfrac{C}{(1+Y_t)^t} + \dfrac{100}{(1+Y_T)^T}]
\end{aligned}
$$

The crux of stock-bond correlation comes down to what stocks and bonds share and what they don't in their cash flows and discount rates. With a bit simplification, a bond pays fixed coupon (C) while a stock pays a stream of uncertain dividends (D) that varies with economic growth (G). On the discounted rate side, stock and bond share a bond yield part (Y) while sotck also carries its unique equity risk premium (ERP).

Now things become much clearer. The shared yield Y sits in both denominators, moving stock and bond price in the same direction. That's what pushes correlation up. The other two pieces, growth G and the equity risk premium ERP, only show up in the stock formula. When G or ERP moves, stock and bond price starts to decouple, pushing correlation down.

The analysis would have ended neatly here if all these variables were exogenous and independent. But they're not. There are probably no variables more endogenous than bond yield and equity risk premium, since the concepts originated from valuation directly. Bond yield also co-moves with economic growth through channels like monetary policy, long term growth expectation and financial conditions. To go further, Ilmanen (2003) takes the analysis one level deeper, to two more fundamental drivers: growth and inflation.

Inflation builds into the bond yield Y directly. When inflation rises, Y rises, and the discount rate goes up for both stocks and bonds. Both prices fall together. So at times when inflation is the focus of the market, stock and bond prices tend to move in the same direction, which means high correlation. On the other hand, Growth works differently. Better growth lifts stock prices by raising expected dividends D. But it also lifts Y through monetary policy and long-term rate expectations, which hurts bond prices. So growth pushes stocks up and bonds down at the same time. At times when growth is the dominant story, stock and bond prices decouple, and correlation falls.

A quite straightforward and intuive mental model! What's even better? It turns out to explain a lot of what has happened and what's happening now. 

Looking at the beginning of the modern era, the last three decades of the 20th century were marked by huge inflation volatility. Two oil shocks in the 1970s pushed inflation sharply higher. Then Volcker came in and fought it with brutal rate hikes, kicking off two decades of declining inflation through the 1980s and 1990s as the Fed slowly rebuilt its credibility. Inflation was the loudest noise in the room throughout. No surprise that US stock-bond correlation stayed firmly positive over this period, ranging from +0.3 to +0.5.

Things started to change as we entered the 21st century. Deepening globalization brought in cheap goods supply from emerging market producers. With that tailwind, central banks earned enough credibility to keep inflation anchored around target. For the first time in a while, inflation stopped being a concern. Growth expectations took over as the main headline instead. The major events of the period, dotcom bubble, financial crisis, China slowdown, were all about growth. As the model would predict, we got 20 years of clean diversification from a negative correlation.

Things flipped again in the 2020s, triggered initially by the pandemic and sustained by the continuing deglobalization and geopolitical uncertainty. We're past the good old days when inflation wasn't a concern. As of Apr 2026, US CPI inflation is running at 3.3%, well above the 2% target and projected to be even higher. Inflation, the variable that touches everyone's daily life, is back as the dominant headline. No surprise we're in a new era of positive stock-bond correlation.

Brixton, Ilmanen et al. (2023) quantify this story by splitting the 1972 to 2022 history into growth and inflation regimes. The pattern is clear: inflation news moves stocks and bonds in the same direction, while growth news pushes them apart. They formalize this in a regression with three variables: growth volatility, inflation volatility, and the correlation between growth and inflation news. The model captures around 70% of the variation in US stock-bond correlation, with similar results across major developed markets.

![Image of Pyramid](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/refs/heads/main/_posts/asset/bond_stock_correlation_scenarios.png)

*Brixton, Ilmanen etc (2023): A Changing Stock-Bond Correlation*



### Reference <a name="ref"></a>
- Antti Ilmanen (2003): Stock-Bond Correlation
- Brixton, Ilmanen etc (2023): A Changing Stock-Bond Correlation
