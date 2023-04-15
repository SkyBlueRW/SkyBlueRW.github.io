##

## Not (entirely) a BlackBox: Optimization Constraint Attribution


- [Introduction](#introduction)
- [The Lagrangian Dual Decomposition of MVO](#lagrangian)
- [Benchmark of Oppotunity Set + Overlay of Conviction](#meaning)
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

The optimization constraint decomposition stems from the first order dual condition that we talked about in the [post](https://skybluerw.github.io/2023/02/28/convex-optimization-basic.html#dual). 

Without loss of generality, for a MVO in the following form where $$f_j$$ refers to addtional terms in the objective function representing penalty on transaction cost, preferrence for ESG ... and $$g_i$$ refers to direct constraint for risk managment, regulation ... etc

$$
\begin{aligned}
\max_x \quad &{\alpha^Tx - \frac{1}{2} \lambda x^TQx + \sum f_i(x)} \\
g_i(x) &<=0
\end{aligned}
$$

One of the necessary conditions that optimal portfolio $$x^{\star}$$ always meet is given by:

$$
\begin{aligned}
\lambda Qx^{\star} &= \alpha + \sum \bigtriangledown f_j(x^{\star}) - \sum \pi_i \bigtriangledown g_i(x^{\star}) \\
\end{aligned}
$$

where $$\pi_i$$ is the shadow cost / Lagrangian Multiplier of the i-th constraint placed on the MVO.

By isolating the optimal portfolio on the left-hand side, we obtain:

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

The optimal portfolio is now the addition of 3 distinct components. The first component ($$x_u$$) is determined by expected return and variance. The second component ($$x_j$$) is determined by the gradient of the additional term in the objective function while the last component ($$x_i$$) is determined by shadow price, covariance and derivative of constraint function. 


Now the question remains: does such a decomposition make economic sense from the perspecitve of portfolio construction?


### Benchmark of Oppotunity Set + Overlay of Conviction <a name="meaning"></a>

Yes it does make sense in the context of portfolio construction. The economic meaning of the decomposition will become clear as we look into the content of each of the 3 component.

**Xu**

The first component $$X_u$$ is the solution to a MVO without any constraint. It is actually the mean variance efficient portfolio given accrute estimate of return and risk. 

$$
\begin{aligned}
\max_x \quad &{\alpha^Tx - \frac{1}{2} \lambda x^TQx} \\
&\Updownarrow \\ 	
x_u &= \frac{1}{\lambda} Q^{-1}\alpha \\
\end{aligned}
$$

Naturally from the first principle, such a portfolio with minimum restriction acts well as the benchmark. It is the portfolio that investors hold under an ideal scenario and represents the **opportunity set** out there available for investors. An investor who knows everything can make the most out of the financial makret with such a portfolio. 

While investors do not know every thing in real world. With limited understanding on the financial market, such a method trying to make everything out from financial market seems somewhat dangerous. In practice, most (if not all) investors will seal themselves in the relative safe zone to avoid unbearbale loss. 

That's when optimization constraints and additional term in objective function come into play. It should be noted that, such kind of restrictions will always lead to performance deterioration in the sense of ex-ante. After all the objective value would decrease as we shrink the feasible set of an optimization problem. While investors generally place such restriction in pursuit of better ex-post performance.

**Xj**

Adding additional terms in the objective function is one such protection. The basic MVO assumes that expected return and variance are the only two characteristics that investors care, which is a simplied mimicking of the real world. 

Obviously, we care more than just expected return and variance from a portfolio. In practice other features like higer moments, transaction cost, ESG preference and so on are often included in the objective fuction. 

The additional term will twist the optimal portfolio as an overlay ($$x_j$$) on the benchmark. Looking into this overlay. The magnitude of impact is positively related to the gradient of the function. It makes perfect sense. If such a term is very sensitive to the change in the portfolio weight, the inclusion of such a term lead to larger magnitude of impact on the portfolio. Vice Versa

$$
\begin{aligned}
x_j &= \frac{1}{\lambda} Q^{-1} \bigtriangledown f_j(x^{\star}) \\
\end{aligned}
$$

**Xi**

Another handy way to place restriction 

$$
\begin{aligned}
x_i &= -\sum \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star})
\end{aligned}
$$






### Reference <a name="ref"></a>
- Scherer & Xu (2007): The Impact of Constraints on Value-Added
- Bender, Lee & Stefek (2009): Decomposing the Impact of Portfolio Constraints
- Stubbs & Vandenbussche (2010): Constraint Attribution
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and current trends
