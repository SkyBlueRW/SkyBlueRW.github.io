## Bayesian len in factor zoo!

- [The "Big Hit"](#introduction)
- [Here Comes the Change](#change)
- [Reference](#ref)


### The "Big Hit" <a name="introduction"></a>

Bayesian model

In a frequentist view, too less data to construct a large model. 

benefit: flexible framwork to combine.  less vunerable to multiple testing, all parameters can be modeled together much easily. way more easier to work with large number of parameters. 

model for assessing factor replicability. hierarchical structure to model themes cross regions and regimes.


pool of information about alpha cross different samples. 

$$
\begin{aligned} 
&\text{Frequentist} \\
f_t&= \alpha + \epsilon_t \\
& \epsilon_t \sim N(0, \sigma^2) \\
\hat{\alpha} &= \bar{f_t}= \dfrac{1}{T}\sum_t f_t = \alpha + \dfrac{1}{T}\sum_t \epsilon_t \\
&\text{dimensional curse ...} \\
&\text{Bayesian} \\
\alpha &\sim N(0, \tau^2) ~~\text{(prior)}\\
\end{aligned}
$$

$$
\begin{aligned}
\mathbb{E}[X|Y,Z] &= \mu_x + (\Sigma_{XY}, \Sigma_{XZ}) 
\begin{pmatrix} 
\Sigma_{YY} & \Sigma_{YZ}  \\
\Sigma_{ZY} & \Sigma_{ZZ}  \\
\end{pmatrix}^ {-1} 
\begin{pmatrix}
Y-\mu_Y \\
Z-\mu_Z \\
\end{pmatrix} \\
Var(X|Y,Z) &= \Sigma_{XX} -  (\Sigma_{XY}, \Sigma_{XZ}) 
\begin{pmatrix} 
\Sigma_{YY} & \Sigma_{YZ}  \\
\Sigma_{ZY} & \Sigma_{ZZ}  \\
\end{pmatrix}^ {-1} 
\begin{pmatrix}
\Sigma_{XY} \\
\Sigma_{XZ} \\
\end{pmatrix} \\
\end{aligned} 
$$

$$
\begin{aligned}
E[\alpha|\hat{\alpha}]&=\dfrac{\tau^2}{\tau^2 + \sigma^2/T} \hat{\alpha}\\
Var[\alpha|\hat{\alpha}]&=\dfrac{\tau^2/T}{\tau^2 + \sigma^2/T}\Sigma^2
\end{aligned}
$$


heavy role of prior.

11
