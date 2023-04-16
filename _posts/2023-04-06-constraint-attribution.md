##

## Not (entirely) a BlackBox: Optimization Constraint Attribution


- [Introduction](#introduction)
- [The Lagrangian Dual Decomposition of MVO](#lagrangian)
- [Benchmark of Oppotunity Set + Overlay of Investment Decission](#meaning)
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

The optimization constraint decomposition stems from the first order dual condition that we talked about in a previous [post](https://skybluerw.github.io/2023/02/28/convex-optimization-basic.html#dual). 

Without loss of generality, for a MVO in the following form where $$f_j$$ refers to addtional terms in the objective function representing penalty on transaction cost, preferrence for ESG ... and $$g_i$$ refers to direct constraint for risk managment, regulation ... etc

$$
\begin{aligned}
\max_x \quad &{\alpha^Tx - \frac{1}{2} \lambda x^TQx + \sum f_j(x)} \\
g_i(x) &<=0
\end{aligned}
$$

One of the necessary conditions (first order condition) that optimal portfolio $$x^{\star}$$ always meet is given by:

$$
\begin{aligned}
\lambda Qx^{\star} &= \alpha + \sum \bigtriangledown f_j(x^{\star}) - \sum \pi_i \bigtriangledown g_i(x^{\star}) \\
\end{aligned}
$$

It is simply the first order condition of the Lagrangian function where $$\pi_i$$ is the shadow cost / Lagrangian Multiplier of the i-th constraint placed on the MVO.

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
x_i &= - \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star})
\end{aligned}
$$

The optimal portfolio is now the addition of 3 distinct components. The first component ($$x_u$$) is determined by expected return and variance. The second component ($$x_j$$) is determined by the gradient of the additional term in the objective function while the last component ($$x_i$$) is determined by shadow price, covariance and derivative of constraint function. 


Now the question remains: does such a decomposition make economic sense from the perspecitve of portfolio construction?


### Benchmark of Oppotunity Set + Overlay of Investment Decision <a name="meaning"></a>

Yes it does make sense in the context of portfolio construction. As we examine the contents of each of the three components, the economic meaning of the decomposition become clear.

**Xu**

The first component $$X_u$$ is the solution to the most basic MVO without any constraints. It is actually the mean variance efficient portfolio given accrute estimate of return and risk. 

$$
\begin{aligned}
\max_x \quad &{\alpha^Tx - \frac{1}{2} \lambda x^TQx} \\
&\Updownarrow \\ 	
x_u &= \frac{1}{\lambda} Q^{-1}\alpha \\
\end{aligned}
$$

Naturally from the first principle, such a portfolio with minimum restriction acts well as the benchmark. It represents the **opportunity set** out there available for investors under ideal circumstances. An investor who knows everything can make the most out of the financial makret with such a portfolio. 

However, investors do not know every thing in real world. With limited understanding on the financial market, such a method trying to make out everything from financial market seems somewhat dangerous. In practice, most (if not all) investors will aim to stay in a relative safe subset to avoid unbearable loss.

To mitigate these risks, optimization constraints and additional terms in the objective function come into play. It should be noted that such restrictions often lead to a deterioration in performance ex-ante. However, investors generally place such restrictions in pursuit of better ex-post performance.

**Xj**

Adding additional terms in the objective function is one such protection. The basic MVO assumes that expected return and variance are the only two characteristics that investors care, which is a simplied mimicking of the real world. 

Obviously, we care more than just expected return and variance from a portfolio. Other features like higer moments, transaction cost, ESG preference and so on are often included in the objective fuction to represent corresponding invesment preferrence and decisions. 

These additional terms ($$\sum f_j(x)$$) will twist the optimal portfolio as an overlay ($$x_j$$) on the benchmark portfolio ($$x_u$$). Looking into this overlay, we can find that the magnitude of impact is positively related to the gradient of the function. It makes perfect sense. If  a term is very sensitive to the change in the portfolio weight, the inclusion of such a term should lead to larger magnitude of impact on the portfolio and Vice Versa.

$$
\begin{aligned}
x_j &= \frac{1}{\lambda} Q^{-1} \bigtriangledown f_j(x^{\star}) \\
\end{aligned}
$$


**Xi**

Another handy way to incorporate investment decisions into MVO is by directly imposing optimization constraints ($$g_i(x) <= 0$$). Common constraints like short sell constraint, exposure constraint...originated from effort on risk management, regulation, or even investment bet.

Similarly, the impact of the constratins on the portfolio can be summarized as an overlay portfolio ($$x_i$$). This overlay portfolio is determined by the shadow price of the constraint and the gradient of the constraint function where the shadow price represetns the sensitivity of objective value to constraint value (price of resources) and gradient of constraint function span that to the change of weight. Together, the product of these two measures determine the sensitivity of the objective value to the weight in a given constraint.

$$
\begin{aligned}
x_i &= - \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star})
\end{aligned}
$$

Due to another necessary optimal condition of [complementary slackness](https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions), the shadow cost of an unbinding constraint is always 0 hence overlay portfolios is non-zero only when corresponding constraint is binding. This is consistent with economic intuition as unbinding constraints do not impact the original portfolio.

For linear constraints, the overlay portfolio ($$x_i$$) has a further economic interpretation as **shadow price weighted characteristic portfolios**. $A_i$ represents the i-th linear constraint and the i-th column of matrix A, which can be any security characteristic factor exposure, industry membership, etc.

$$
\begin{aligned}
g(x) &= Ax <= 0 \\
&\Updownarrow \\ 	
x_i &= - \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star}) \\
&= \pi_i \dfrac{1}{\lambda} Q^{-1}A_i
\end{aligned}
$$ 

$$\dfrac{1}{\lambda} Q^{-1}A_i$$ is a scaled version of the characteristic portfolio for $$A_i$$. A characteristic portfolio is the minimum variance portfolio with unit exposure to corresponding characteristic. It contains all relavant information of $$A_i$$ in portfolio construction.

$$
\begin{aligned}
\min_x \quad &{ \lambda x^TQx} \\
s.t & A_i^T x_i = 1 \\
&\Updownarrow \\ 	
x &= \dfrac{1}{A_i^T Q^{-1}A_i} Q^{-1}A_i
\end{aligned}
$$

### Reference <a name="ref"></a>
- Scherer & Xu (2007): The Impact of Constraints on Value-Added
- Bender, Lee & Stefek (2009): Decomposing the Impact of Portfolio Constraints
- Stubbs & Vandenbussche (2010): Constraint Attribution
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and current trends
