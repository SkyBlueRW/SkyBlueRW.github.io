##

## Not (entirely) a BlackBox: Optimization Constraint Attribution


- [Introduction](#introduction)
- [Reference](#ref)



### Introduction? <a name="introduction"></a>


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


### Reference <a name="ref"></a>
- Scherer & Xu (2007): The Impact of Constraints on Value-Added
- Bender, Lee & Stefek (2009): Decomposing the Impact of Portfolio Constraints
- Stubbs & Vandenbussche (2010): Constraint Attribution
- Kolm, Tutuncu & Fabozzi (2013): 60 Years of Portfolio Optimization: Practical Challenges and current trends
