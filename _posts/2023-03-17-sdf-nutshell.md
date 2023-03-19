#

## Stochastic Discount Factor: a nutshell of asset pricing 


- [P = E(mx)](#introduction)
- [The origin: as little as LOOP](#ma)
- [The Implication: the representation and common languange](#im)
    - [Beta Representation](#beta)
    - [Portfolio Representation](#port)

### P = E(mx) <a name="introduction"></a>

It all starts with $$P_t = E_t(m_{t+1}x_{t+1})$$! 

At the heart of many interesting topics in finance such as factor pricing models, market anomalies, return preidiction, time variant risk premimum..etc lies this fundamental asset pricing formula. 

It is amazing that with such a neat equation based on few assumptions, one can price all future payoffs $$x_{t+1}$$ with a stochastic discount factor $$m_{t+1}$$. Through the len of the paradigm with stochastic discount factor, we can extend insights across asset classes from different perspectives such as macro, consumption, production, portfolio... 

Throughout this blog, I would like to kick off the discussion on the subject of asset pricing with a focus on stochastic discount factor. Where does it come from? what's the implication? how to allign it with real world? these are the questions we hope to address. 
 

### The Origin: as little as LOOP <a name="ma"></a>

There are actually several ways to get to the asset pricing formula. I will begin with the one that requires the fewest assumptions and gradually build upon it with more perspectives and assumptions. 

In its most general form, **Law of One Price** (LOOP later in the blog) can garuantee the pricing formula. As long as portfolios with the same payoff have the same price, there exists such a random variable of stochastic discount factor that prices all payoffs. 

To gain some intuition, let's swtich to the state space of random variable. Remember that up to time t, the payoff $$x_{t+1}$$ of a security is a random variable with different potential realizations in future scenarios. We can express it explicitly in state space with a vector $$x = [x^{1},...x^{i}...x^{k}]$$, where each element in the vector represents a possible realized payoff in the corresponding scenario. 

Stacking all securities (1...n) in the market at time t, we get a matrix $$X = [x_1, ... , x_n]^T$$, whose row space is the payoff space for time t+1. Any payoffs availble in the market lie in this row space. We can put LOOP in the same context as well: any two portfolios $$w_1$$ and $$w_2$$ with same payoff at t+1 ($$Xw_1 = Xw_2$$) should have the same price at time t ($$Pw_1 = Pw_2$$). 

It's equivalent to saying that $$X(w_1 - w_2) = 0$$ leads to $$p (w_1 - w_2)$$ for any two portfolios $$w_1$$ and $$w_2$$. With a bit of linear algebra we know that price p has to be a member of the payoff space for such condition to hold. Hence there exists a vector $$q = (XX^T)^{-1}XP$$ such that $$P = Xq$$. We link the price at time t ($$p$$) and payoff at time t+1 ($$X$$) with a vector ($$q \in Row(X)$$). Random variable q is all we need to price any securites in the market. 

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


### The Implication: the representation and common languange <a name="im"></a>

Let's pause for a moment to sink in the equation at hand.

As you might noticed already, the equation is highly general with limited structure imposed yet. It has enough generality to apply to different securities and perspectives, but it functions more as a paradigm than a fully-fledged model. To gain further insights, we need to introduce additional assumptions and structure to this foundation.

As suggested by Prof Cochrane in his book [Asset Pricing](https://www.amazon.com/Asset-Pricing-John-H-Cochrane/dp/0691121370/ref=sr_1_1?crid=3FZCYELEHP9YW&keywords=asset+pricing&qid=1679215995&sprefix=asset+pric%2Caps%2C293&sr=8-1), those structures and assumptions can be placed directly on SDF in the form $$m_{t+1} = f(data, parameter)$$. 

Asset pricing models are then summarized in these two equations. The first equation sets the empirical representation and common language that we hope to keep invariant across security markets and perspectives. With this prerequisite in place, we can unleash our imagination in economic reasoning with the second equation, while still maintaining a comparable language.

$$
\begin{aligned}
p_t &= E_t(m_{t+1}x_{t+1}) \\
m_{t+1} &= f(data, parameter)
\end{aligned}
$$

The price equation can be extended to equivalent representations. You might find the one in gross return more familiar. 

$$
\begin{aligned}
1 &= E(m\dfrac{x}{p}) \\
1 &= E(mR) \\
\end{aligned}
$$

Also an intersting special case of risk free return. For a risk free security, its gross return R is no longer a randon variable hence we have 

$$
\begin{aligned}
1 & = E(m)R^{f} \\
R^{f} &= \dfrac{1}{E(m)}
\end{aligned}
$$

Return can be further decomposed into accormodation for time value and risk premium. With such a representation, it is clear that risk is defined as covariance with the SDF. 

$$
\begin{aligned}
1 &= E(m)E(R) + cov(m, R) \\
E(R) &= \dfrac{1}{E(m)} - \dfrac{cov(m, R)}{E(m)} \\
E(R) &= R^{f} - R^{f}cov(m, R)
\end{aligned}
$$



#### Beta Representation <a name="beta"></a>

#### Portfolio Representation <a name="port"></a>





### 


### Another paragraph <a name="paragraph2"></a>
The second paragraph text


Deviation from Law of One Price. introduce of prob measure. risk premium

equivalent representation in beta 

equivalent of mv. apply for all rn.
rn


