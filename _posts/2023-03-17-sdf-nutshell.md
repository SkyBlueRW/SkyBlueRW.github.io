#

## Stochastic Discount Factor: a nutshell of asset pricing 


- [Introduction](#introduction)
- [The origin: as little as LOOP](#ma)
- [P = E(mx)](#im)
- [The modeling](#model)
    - [Beta Representation](#beta)
    - [Portfolio Representation](#port)

### Introduction <a name="introduction"></a>

It all starts with $$P_t = E_t(m_{t+1}x_{t+1})$$! 

At the heart of many interesting topics in finance such as factor pricing models, market anomalies, return preidiction, time variant risk premimum..etc lies this fundamental asset pricing formula. 

It is amazing that with such a neat equation based on few assumptions, one can price all future payoffs $$x_{t+1}$$ with a stochastic discount factor $$m_{t+1}$$. Through the len of the paradigm with stochastic discount factor, we can extend insights across asset classes from different perspectives such as macro, consumption, production, portfolio... 

Throughout this blog, I would like to kick off the discussion on the subject of asset pricing with a focus on stochastic discount factor. Where does it come from? what's the implication? how to allign it with real world? these are the questions we hope to address. 
 
There are actually several ways to get to the asset pricing formula. I will begin with the one that requires the fewest assumptions and gradually build upon it with more perspectives and assumptions. 


### The Origin: as little as LOOP <a name="ma"></a>

In its most general form, **Law of One Price** (LOOP later in the blog) garuantees the pricing formula. As long as portfolios with the same payoff have the same price, there exists such a random variable of stochastic discount factor that prices all payoffs. 

To gain some intuition, let's swtich to the state space view of random variable. Remember that up to time t, the payoff $$x_{t+1}$$ of a security is a random variable with different potential realizations in future scenarios. We can express it explicitly in state space with a vector $$x = [x^{1},...x^{i}...x^{k}]$$, where each element in the vector represents a possible realized payoff in the corresponding scenario. Here we assume finite (k) number of scenarios while all of this can extend to the continuous world as well(Riez Theorem).

Stacking all securities (1...n) in the market at time t, we get a matrix $$X = [x_1, ... , x_n]^T$$ (rank(X) = K <= n), whose row space is the payoff space for time t+1. Any payoffs availble in the market lie in this row space. We can put LOOP in the same context as well: any two portfolios $$w_1$$ and $$w_2$$ with same payoff at t+1 ($$Xw_1 = Xw_2$$) should have the same price at time t ($$Pw_1 = Pw_2$$). 

It's equivalent to saying that $$X(w_1 - w_2) = 0$$ leads to $$p (w_1 - w_2)$$ for any two portfolios $$w_1$$ and $$w_2$$. With a bit of linear algebra we know that price p has to be a member of the payoff space for such condition to hold. Hence there exists a vector $$q = (XX^T)^{-1}XP$$ such that $$P = Xq$$. Random variable q is all we need to price any securites in the market. We link the price at time t ($$p$$) and payoff at time t+1 ($$X$$) with a vector ($$q \in Row(X)$$) in the state space.

Technically, q is still not the stochastic discount factor m we have in the the pricing formula. A few modifications are required to bring in the expecatation calculation. We can continue the reasoning with an arbitrary probability measure $$\pi$$. Let's look into one security (one row of the $$P = Xq$$).

$$
\begin{aligned}
p_j &= [x_j^{1},...x_j^{i}...x_j^{k}][q^{1},...q^{i}...q^{k}]^T \\
&= \sum_{i}^k x_j^{i} q^{i} \\
&= \sum_{i}^k x_j^{i} \dfrac{q^{i}}{\pi^{i}} \pi^{i}\\
&= E^{\pi}(\dfrac{q}{\pi} x_j)\\
&= E^{\pi}(m x_j)
\end{aligned}
$$

Here we are with the pricing equation $$p = E(mx)$$ :)  To state it more formally, **there is always a unique stochastic discount factor in the payoff space $$m \in Row(X)$$ that prices all payoffs under LOOP**. 

It is worth noting that this SDF may not be the only one available. In cases where the payoff space does not span the entire future scenario set (**incomplete market**) we can simply go beyond the payoff space to obtain an alternative SDF ($$E(mX) = E((m+\epsilon)X) $$) by adding an arbitrary orthogonal component ($${\epsilon: E(\epsilon X)=0}$$).


### P = E(mx) <a name="im"></a>

Let's take a moment to consider the equation at hand and explore various representations that can be derived from it.

You may find the price equation familiar in terms of gross returns and excess return. We can simply divide both sides by p and transform the payoff into gross return ($$R$$):

$$
\begin{aligned}
1 &= E(m\dfrac{x}{p}) \\
1 &= E(mR) \\
\end{aligned}
$$

While excess return ($$R^{e}$$) is simply the difference of two returns, which provide a purer view on difference of risk.

$$
\begin{alinged}
1 - 1 & = E(m(R^{i} - R^{j})) \\
0 &= E(mR^{e})
\end{aligned}
$$

An intersting special case is the risk free return. For a risk free security, its gross return R is no longer a randon variable hence we have 

$$
\begin{aligned}
1 & = E(m)R^{f} \\
R^{f} &= \dfrac{1}{E(m)}
\end{aligned}
$$

Yet another insightful representation can be derived using the definition of covariance. With $$cov(m, R) = E(mR) - E(m)E(R)$$, we have

$$
\begin{aligned}
1 &= E(mR) =  E(m)E(R) + cov(m, R) \\
E(R) &= \dfrac{1}{E(m)} - \dfrac{cov(m, R)}{E(m)} \\
E(R) &= R^{f} - R^{f}cov(m, R)
\end{aligned}
$$

Here, the expected return is comprised of two distinct components. The first component is the risk-free rate, which accounts for the time value of investing. The second component is a risk adjustment that accounts for uncertainty regarding future returns. Notably, risk is measured as a covariance with the SDF. Any volatility that does not correlate with the SDF recevie no reward in expected return.

By taking one step of transformation, we arrive at a **single factor model representation** that enhances the notion of systematic risk. The exposure of risk is measured in terms of covariance with SDF while the risk premium, on the other hand depend on the volatility of SDF.

$$
\begin{aligned}
E(R^{i}) &= R^{f} + \dfrac{cov(R^{i}, m)}{Var(m)}(-\dfrac{var(m)}{E(m)}) \\
E(R^{i}) &= R^{f} + \beta_{R^{i}, m} \lambda_{m}
\end{aligned}
$$

We can also obtain a **portfolio perspecitive** via the Sharpe ratio bound. The powerful insight is that the maximum Sharpe ratio portfolios investors can obtain are perfectly correlated with the SDF. Hence it contains every bit of information in pricing as SDF does.

$$
\begin{aligned}
E(R^{i}) - R^{f} &= -R^{f}cov(m, R^{i}R)\\
\dfrac{E(R^{i}) - R^{f}}{\sigma(R^{i})} &= -corr(m, R^{i}) \dfrac{\sigma(m)}{E(m)} \\
|\dfrac{E(R^{i}) - R^{f}}{\sigma(R^{i})}| &<= \dfrac{\sigma(m)}{E(m)}
\end{aligned}
$$

Last but not least, in a complete market free of arbitrage opportunities. SDF is also equivalent to the unique **Risk Free Probability Measure**, where $$\pi^{\star} = \dfrac{m \pi}{E(m)}$$. Hence we extend the pricing formula to financial derivatives as well. 

$$
\begin{aligned}
p &= Xq \\
p_j &= \sum_{i}^k x_j^{i} q^{i} \\
&= \sum_{i}^k x_j^{i} \dfrac{q^{i}}{\pi^{i}} \pi^{i}\\
&= E^{\pi^{\star}}(x)
\end{aligned}
$$

It is truly remarkable that wihout much modeling yet, we can extend the pricing equation to these useful concepts already. Having access to different representations with different focuses is incredibly convenient in application. We can choose the representation that best suits our application and continue with further modeling. Moreover, the insights gained from one representation can be extended to all other representations since they are equivalent in the first place.


### The modeling <a name="model"></a>

As you might notice at the moment, though insitful, the pricing equation is highly general with limited structure imposed yet. It has enough generality to apply to different securities and perspectives, but it functions more as a paradigm than a fully-fledged model. To gain further insights, we need to introduce additional assumptions and structure to this foundation.

As suggested by Prof Cochrane in his book [Asset Pricing](https://www.amazon.com/Asset-Pricing-John-H-Cochrane/dp/0691121370/ref=sr_1_1?crid=3FZCYELEHP9YW&keywords=asset+pricing&qid=1679215995&sprefix=asset+pric%2Caps%2C293&sr=8-1), those structures and assumptions can be placed directly on SDF in the form $$m_{t+1} = f(data, parameter)$$. 

Asset pricing models are then summarized in these two equations. The first equation sets the empirical representation and common language that we hope to keep invariant across security markets and perspectives. With this prerequisite in place, we can unleash our imagination in economic reasoning with the second equation, while still maintaining a comparable language.

$$
\begin{aligned}
p_t &= E_t(m_{t+1}x_{t+1}) \\
m_{t+1} &= f(data, parameter)
\end{aligned}
$$



#### Factor Models <a name="beta"></a>


#### Portfolio Representation <a name="port"></a>




