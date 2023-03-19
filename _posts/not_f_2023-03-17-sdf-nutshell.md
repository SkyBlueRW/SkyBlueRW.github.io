#

## Stochastic Discount Factor: a nutshell of asset pricing 


- [P = E(mx)](#introduction)
- [The origin](#ma)


### P = E(mx) <a name="introduction"></a>

It all starts with $$P_t = E_t(m_{t+1}x_{t+1})$$! 

At the heart of many interesting topics in finance such as factor pricing models, market anomalies, return preidiction, time variant risk premimum..etc lies this fundamental asset pricing formula. 

It is amazing that with such a neat equation based on few assumptions, one can price all future payoffs $$x_{t+1}$$ with a stochastic discount factor $$m_{t+1}$$. Through the len of the paradigm with stochastic discount factor, we can extend insights across asset classes from different perspectives such as macro, consumption, production， portfolio... 

Throughout this blog, I would like to kick off the discussion on the subject of asset pricing with a focus on stochastic discount factor. Where does it come from? what's the implication? how to allign it with real world? these are the questions we hope to address. 


### The Origin <a name="ma"></a>

There are actually several ways to get to the asset pricing formula. I will begin with the one that requires the fewest assumptions and gradually build upon it with more perspectives and assumptions. 

In its most general form, **Law of One Price** can garuantee the pricing formula. As long as portfolios with the same payoff have the same price, there exists such a random variable of stochastic discount factor that prices all payoffs. 

To gain some intuition, let's swtich to the state space of random variable. Remember that up to time t, the payoff $$x_{t+1}$$ of a security is a random variable with different potential realizations in future scenarios. We can express it explicitly in state space with a vector $$x = [x^{1},...x^{i}...x^{k}]$$, where each element in the vector represents a possible realized payoff in the corresponding scenario. 

Stacking all securities (1...n) in the market at time t together, we get a matrix $$X = [x_1, ... , x_n]^T$$, whose row space is the payoff space for time t+1. Any payoffs availble in the market lie in this row space. We can put Law of One Price in the same context as well: any two portfolios $$w_1$$ and $$w_2$$ with same payoff at t+1 ($$Xw_1 = Xw_2$$) should have the same price at time t ($$Pw_1 = Pw_2$$). 

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

Here we are. Starting from Law of one Price, we get to the pricing equation $$p = E(mx)$$ :) 

Let's halt here for a sec to think about the equation at hand.

We do not lose much generality in taking such a paradigm with stochastic discount factor. it is not exagerate to assume Law of One Price, a break of which implies profit without any risk. 

### 


### Another paragraph <a name="paragraph2"></a>
The second paragraph text


Deviation from Law of One Price. introduce of prob measure. risk premium

equivalent representation in beta 

equivalent of mv. apply for all rn.
rn
