
## Navigating the Factor Zoo!

- [From Factors to Managed Portfolios](#portfolio)
- [The Classic](#classic)
- [The Bayesian Len](#bayes)
- [Reference](#ref)

Take a step back, audit.

Conditional expectation of future realized excess return.

machine learning helpful 1 prediction, 2 high dimension, 3 nonlinearity


General empirical asset pricing 
$r_{i,t+1} = E_t(r_{i, t+1}) + \epsilon_{i,t+1},  E_t(r_{i, t+1}) = g(x_{i,t})$


1. a most generic view of joint distribution of return and other variables
2. focus on return based on observable variables of conditional then DGP 
3. the loss function will be like this just like any other prediction problem if we do not inject any domain knowledge form finance and also starting point if we approach we machine learning techniques
4. We inject financial domain knowledge at least for two reasons. First the goal is ultimately building a portfolio with desired return risk profile. There is difference between this goal and a sucessful prediction. Secondaly, due to the nature of the financial market, high dimension with limited data. Also low signal to noise ratio.
5. We customize

a. The transition of view from security to portfolio representation. The low signal to noise ratio issue, diversifaction cornerstone of finance helps to extract truly meanigful information from portfolio. It's also reasonable as investment decision need to turn into actionable portfolios. 
b. focus on cross sectional. Still it's a hard problem. We further simplyfy by removing mean. The prediction of general market is a stand alone topic and we can focus on relative performance of securities. It's also reasonable when we look at long-short portfolio or overlay on top of a benchmark. 
c. 
