#

## From Volatility to Maximum Drawdown


- [Introduction](#introduction)
- [Reference](#ref)

worst case scenario: buying at peak and selling at bottom

### Introduction <a name="introduction"></a>


$$
\begin{aligned}
r_t &= \mu + \sigma_t e_t \\
\sigma_t^2 &= \alpha_0 + \alpha_1 r_{t-1}^2\\
e_t &\sim N(0, 1) \\
\sigma^2 &= \dfrac{\alpha_0}{1-\alpha_1}
\end{aligned}
$$


### Reference <a name="ref"></a>

- Grossman & Zhou (1993): Optimal Investment Strategies for Controlling Draw-downs
