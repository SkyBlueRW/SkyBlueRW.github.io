
## Correlation

- [From Factors to Managed Portfolios](#portfolio)
- [The Classic](#classic)
- [The Bayesian Len](#bayes)
- [Reference](#ref)


Stock-bond correlation is one of those topics that never really gets old, and for good reason. It's a critical input into asset allocation.

For decades, bonds have entered investors' portfolios as the natural diversifier, nurturing traditional allocations like the 60/40. On top of that, correlations move slowly compared to returns and volatility, making them stable enough to anchor strategies like the famous risk parity and maximum diversification.

But none of this is guaranteed. Since the pandemic, stock-bond correlation has flipped positive for the first time in twenty years. It not only erodes the diversification a stock-bond portfolio is supposed to deliver, but also puts strategies that rely on stable correlations under real pressure. Feels like a good time to revisit the old question.




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
