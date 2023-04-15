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

The optimization constraint decomposition roots in the first order dual condition that we briefly talked about in the [post](https://skybluerw.github.io/2023/02/28/convex-optimization-basic.html#dual). 

Without loss of generality, for a MVO in the following form where $$f_j$$ refers to addtional terms in the objective function representing penalty on transaction cost, preferrence for ESG ... and $$g_i$$ refers to direct constraint for risk managment, regulation ... etc

$$
\begin{aligned}
\max_x \quad &{\alpha^Tx - \frac{1}{2} \lambda x^TQx + \sum f_i(x)} \\
g_i(x) &<=0
\end{aligned}
$$

One of the necessary conditions that optimal portfolio $$x^{\star}$$ always meet is ($$\pi_i$$ is the shadow cost / Lagrangian Multiplier of the i-th constraint placed on the MVO)

$$
\begin{aligned}
\lambda Qx^{\star} &= \alpha + \sum \bigtriangledown f_j(x^{\star}) - \sum \pi_i \bigtriangledown g_i(x^{\star}) \\
\end{aligned}
$$

Keeping only the optimal portfolio at the left hand side gives us

$$
\begin{aligned}
x^{\star} &= \frac{1}{\lambda} Q^{-1}\alpha + \sum \frac{1}{\lambda} Q^{-1} \bigtriangledown f_j(x^{\star}) - \sum \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star}) \\
x^{\star} &= x_u + \sum_j x_j + \sum_i x_i \\
\end{aligned}
$$

where

$$
\begin{aligned}
x_u &= \frac{1}{\lambda} Q^{-1}\alpha \\
x_j &= \frac{1}{\lambda} Q^{-1} \bigtriangledown f_j(x^{\star}) \\
x_i &= -\sum \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star})
\end{aligned}
$$



### Reference <a name="ref"></a>
- Scherer & Xu (2007): The Impact of Constraints on Value-Added
- Bender, Lee & Stefek (2009): Decomposing the Impact of Portfolio Constraints
- Stubbs & Vandenbussche (2010): Constraint Attribution
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and current trends
