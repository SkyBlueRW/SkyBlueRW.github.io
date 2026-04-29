
## Correlation

- [From Factors to Managed Portfolios](#portfolio)
- [The Classic](#classic)
- [The Bayesian Len](#bayes)
- [Reference](#ref)


Stock-bond correlation is one of the oldest topics in asset allocation, and it keeps coming back for a reason. 

For decades, bonds have played the role of natural diversifier in investors' portfolios, nurturing traditional allocations like the 60/40. Correlations also move slowly compared to returns or volatility, making them more stable estimate to anchor strategies like risk parity and maximum diversification.

But none of this is given as granted. Since the pandemic, stock-bond correlation has flipped positive for the first time in twenty years with a continuing momentum. The diversification a stock-bond portfolio is supposed to deliver is fading, and strategies that rely on stable correlations are under real pressure. It's a good time to revisit the old question.

There is no shortage of well rooted models for the estimation of correlation. DCC-GARCH decomposes a covariance matrix to volatility and correlation for their different dynamics. Regime switching and hierachical clustering models try to enhance and capture a nonlinear aspect of the association. Even a plain rolling sample correlation works reasonably well for the slow moving nature of correlation. But when I want to actually make sense of stock-bond correlation, the mental model I keep coming back to is from Ilmanen's 2003 paper.

The model starts from a surprisingly simple and intuive place: the discounted cash flow framework. Both stocks and bonds, like any other asset, are priced as the expected present value of their future cash flows.

$$
\begin{aligned}
P_{\text{stock}} &= E[\sum_{t=1}^{\infty} (\dfrac{1+G}{1 + Y_t + \text{ERP}_t})^t D] \\
P_{Bond} &= E[\sum_{t=1}^T \dfrac{C}{(1+Y_t)^t} + \dfrac{100}{(1+Y_T)^T}]
\end{aligned}
$$

The crux of stock-bond correlation just comes from the what they share and distinct in the cash flow and discounted rate! With a little bit simplification, a bond pays fixed coupon (C) while a stock pays a stream of uncertain dividends (D) that varies with economic growth (G). On the discounted rate side, stock and bond share a bond yield part (Y) while sotck also carries its unique equity risk premium (ERP).



- https://www.blackrock.com/us/financial-professionals/insights/bonds-offer-more-diversification
- https://research-center.amundi.com/files/nuxeo/dl/eb84a66b-ebac-4901-8d70-70f3ed02a0d4?inline=

1. Start with the original Ilmanen (2003) framework. Stocks and bonds are both valued by discounting expected cash flows. The original insight: stocks and bonds don't share their cash flows, but they do share a discount rate. So whichever channel is the louder source of news — cash flows or the shared discount rate — determines the sign of the correlation. This already explains the major US regime flips: cash-flow-dominated periods produce negative correlation, discount-rate-dominated periods (high or volatile inflation) produce positive correlation.
2. Add structure inside the discount rate. Decompose it into a shared component (real risk-free rate + expected inflation) and an asset-specific risk premium (term premium for bonds, equity risk premium for stocks, plus credit spread for corporates or sovereign/FX premia for EM). The shared piece is what Ilmanen treats as a single object; making the asset-specific pieces explicit lets you see when discount-rate news moves stocks and bonds together versus apart.
3. The decomposition explains the residuals. With the shared-vs-specific split, three patterns the simple model handles awkwardly fall out naturally:

Historical regime changes — which component was the dominant source of news at the time
Cross-country differences — Japan's near-zero correlation for two decades was the shared channel being switched off by ZIRP/YCC; EM's persistent positive correlation reflects sovereign credit and FX premia that are equity-correlated by construction
Instrument differences within a country — Treasuries-vs-equity, IG-corp-vs-equity, and EM-sovereign-vs-equity sit at structurally different correlation levels for reasons unrelated to regime
d. Linear


### Reference <a name="ref"></a>
- Antti Ilmanen (2003): Stock-Bond Correlation
- Brixton, Ilmanen etc (2023): A Changing Stock-Bond Correlation
