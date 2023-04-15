##

## Not (entirely) a BlackBox: Optimization Constraint Attribution


- [Introduction](#introduction)
- [The Lagrangian Dual Decomposition of MVO](#lagrangian)
- [Reference](#ref)



### Introduction? <a name="introduction"></a>

Let's face it. Though laying the foundation of modern portfolio theory with its profound economic meaning, Mean Variance Optimization (MVO) often behave somewhat like a black box in practice. Even the slightest adjustment to an existing MVO can lead to counterintuitive changes in the optimal portfolio, impeding further insight into the portfolio.

This complexity of MVO, in my view, arises from the use of variance as the risk measure. Working with MVO where variance is the risk measure is like working in the "reversed covariance matrix space" instead of the "plain vanilla space" that we are accustomed to. Even a small binding constraint on a single security can have a convoluted impact on all other securities through the covariance matrix. This complexity is further amplified in a full-sized MVO model with many constraints for regulation, risk management, or even investment betting.

Fortunately, constraint attribution can shed light on the situation. Essentially, it can decompose an optimal portfolio ($$x^{\star}$$) obtained from a full-sized optimization into the most basic unconstrained MVO portfolio ($$x_u$$) and various overlays that represent constraints ($$x_i$$) or additional terms in the utility function ($$x_j$$).

$$
\begin{aligned}
x^{\star} &= x_u + \sum_j x_j + \sum_i x_i
\end{aligned}
$$

With this decomposition, we can easily extend analysis to the decomposition of risk, return, and utility for every constraint, both ex-ante and ex-post. This makes the portfolio much more analyzable and provides valuable insights for decision makings in portfolio construction.

For this blog, I would like to breifly introduce this powerful technique of constraint decomposition. I will first explore the origins and intuition behind Lagrangian Dual decomposition and then delve into practical applications of constraint decomposition in portfolio optimization. 


### The Lagrangian Dual Decomposition of MVO <a name="lagrangian"></a>


### Reference <a name="ref"></a>
- Scherer & Xu (2007): The Impact of Constraints on Value-Added
- Bender, Lee & Stefek (2009): Decomposing the Impact of Portfolio Constraints
- Stubbs & Vandenbussche (2010): Constraint Attribution
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and current trends
