##

## Not (entirely) a BlackBox: Optimization Constraint Attribution


- [Introduction](#introduction)
- [Reference](#ref)



### Introduction? <a name="introduction"></a>

It's time to face the reality. Though perhaps the most import discovery in modern portfolio theory, Mean Variance Optimization (MVO) often work like a black box in practice. Even the slightest adjustment in an existing MVO can lead to a counterintuitive change in the optimal portfolio, leading to blockers for further insight on the portfolio.

This complexity of MVO, in my understanding, arises from the use of variance. Working with MVO where variance is the risk measure is like working in the "reversed covariance matrix space" instead of the "plain vanilla space" that we are used to. Even a small binding constraint on a single security can impact all other securities in a convoluted way through the covariance matrix. This complexity is further magnified in a full-sized MVO model with a large number of constraints for regulation, risk management, or even investment betting.

The constraint attribution can shed light on the situation. Essentially the constraint attribution method can decompose an optimal portfolio obtained from a full sized optimization into the most basic unconstraint MVO portfolio and various overlays representing constraints or additional terms in utility function.

With this holding decomposition, we can extend decomposition of risk, return, and utility to every constraint placed from the perspective of both ex-ante and ex-post.

$$
\begin{aligned}
x^{\star} &= x_u + \sum_j x_j + \sum_i x_i
\end{aligned}
$$


shadow price weighted characteristic portfolio of each constraint

Problem

$$
\begin{aligned}
\max_x \quad &{\alpha^Tx - \frac{1}{2} \lambda x^TQx + \sum f_i(x)} \\
g_i(x) &<=0
\end{aligned}
$$

Lagrangian Dual Decomposition
- implied alpha
- active weight 

$$
\begin{aligned}
\lambda Qx^{\star} &= \alpha + \sum \bigtriangledown f_j(x^{\star}) - \sum \pi_i \bigtriangledown g_i(x^{\star}) \\
x^{\star} &= \frac{1}{\lambda} Q^{-1}\alpha + \sum \frac{1}{\lambda} Q^{-1} \bigtriangledown f_j(x^{\star}) - \sum \pi_i  \frac{1}{\lambda} Q^{-1}\bigtriangledown g_i(x^{\star}) \\
x^{\star} &= x_u + \sum_j x_j + \sum_i x_i
\end{aligned}
$$


**Further Analysis by projecting on alpha space**

$$
\begin{aligned}
x^{\star} &= x_u + \sum_j x_j + \sum_i x_i \\
&=x_u + \sum_j (\beta_{ju}x_u + x_{j,orthogonal}) + \sum_i (\beta_{iu}x_u + x_{i,orthognoal})  \\
&=(1 + \sum_j \beta_{ju} + \sum_i \beta_{iu}) x_u + (\sum_j x_{j, orthogonal} + \sum_i x_{i, orthogonal}) \\
\beta_{cu} &= \frac{x^{\star}Qx_u}{x_u^TQx_u} \\
\end{aligned}
$$

Tutuncu (2012): weight decomposition not intuitive due to correlation.


When the standard deviation constraint is binding. We can perform similar decomposition.

$$
\begin{aligned}
\frac{\pi^{r}Qx^{\star}}{\sqrt{x^{\star T}Qx^{\star}}} &= \alpha + \sum \bigtriangledown f_i(x^{\star}) - \sum \pi_i \bigtriangledown g_i(x^{\star}) \\
x^{\star} &= \frac{vQ^{-1}}{\pi^r} \alpha + \sum \frac{vQ^{-1}}{\pi^r}\bigtriangledown f_i(x^{\star}) - \sum \pi_i \frac{vQ^{-1}}{\pi^r} \bigtriangledown g_i(x^{\star})
\end{aligned}
$$


### Reference <a name="ref"></a>
- Scherer & Xu (2007): The Impact of Constraints on Value-Added
- Bender, Lee & Stefek (2009): Decomposing the Impact of Portfolio Constraints
- Stubbs & Vandenbussche (2010): Constraint Attribution
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and current trends
