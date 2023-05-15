
#

## The news from ragged economic data

economic data special
ragged
different frequency

nowcast 
one side a cohesive stat framework to handle this raged different frequency

joint modeling of the dynamics of data with different frequency.

present forecast in an insightful way such that forecast of variable of interest is updated as weighted sum of news measured as different between realization and forcast of other variables. Formalization of work process hence easy to fit into investment decision process.

info arrive in an incremental manner


- [Introduction](#introduction)
- [Reference](#ref)


### Introduction <a name="introduction"></a>


$$
\begin{aligned}
\Omega_v &:\{x_{i, t_i}, t_i=1,2,...,T_{i,v}, i = 1,...,n \} \\
P[x_{i,t}|\Omega_v] &= E[x_{i,t}|\Omega_v] \\ 
E[x_{i,t}|\Omega_{v+1}] &= E[x_{i,t}|\Omega_v] + E[x_{i,t}|I_{v+1}] \\ 
I_{v+1, j} &= x_{j, T_{j, v+1}} - E[x_{j, T_{j, v+1}} | \Omega_v] \\
E[x_t|I_{v+1}] &= E[x_t I_{v+1}^T]{E[I_{v+1} I_{v+1}^T]}^{-1} I_{v+1}
\end{aligned}
$$

unexpected news

Gaussian


$$
\begin{aligned}
E[x_t|I_{v+1}] &= \sum_{j \in J_{v+1}} b_{j,t,v+1}(x_{j, T_{j,v+1}} - E[x_j,T_{j, v+1}|\Omega_v]) \\ 
\end{aligned}
$$

### Reference <a name="ref"></a>


- Banbura, Giannone & Reichlin(2010): Nowcasting
