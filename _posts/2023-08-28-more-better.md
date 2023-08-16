#

## Combine Information for return forecast: The more the better?


- [Introduction](#introduction)
- [Reference](#ref)



### Introduction <a name="introduction"></a>


last BL, not mention calibration of variance related parameters. this blog talks about the calibration in practice. furthermore, this strategy of combine information underlying BL.

weighted average


calibration

- tau
- specifically omega
- specify omega in terms of tau for subjective view / Idozek. Active risk proportional
- boils down to shrink / with risk parity


strategy a challenge task, the hope rely on combine multiple information source. from a finance perspective, different information for different horizon. from a statistical perspective, return for high variance, diversified information bagging/ensemble. 

prior a special one 

implied confidence level

$$
\tau \Sigma
$$

as standard error of estimate of the implied equilibrium return 

$$
\begin{aligned}
\mu^{\star}_{100} &= \pi + \tau\Sigma P^T (P\tau \Sigma P^T)^{-1}(Q - P\pi)\\
\mu^{\star}_0 &= \pi
\end{aligned}
$$

$$
\begin{aligned}
x^{\star}_{100} &= (\lambda \Sigma)^{-1} \mu^{\star}\\
x^{\star}_0 &= (\lambda \Sigma)^{-1} \pi = x_0\\
\end{aligned}
$$



special forecast: the one consistent with benchmark/market portfolio

tau

BL think uncertainty in mean return is much smaller than uncertainty in return. tau should be small

### Reference <a name="ref"></a>

- Walters (2013): The Factor Tau in the Black-Litterman Model
- Walters (2007): The Black-Litterman Model in Details
- Idzorek (2007): A step-by-step guide to the Black-Litterman model
- Haesen, Hallerbach, Markwat & Molenaar (2017): Enhancing Risk Parity By Including Views
