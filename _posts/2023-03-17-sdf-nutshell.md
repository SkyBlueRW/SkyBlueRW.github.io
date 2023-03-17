#

## Stochastic Discount Factor: a nutshell of asset pricing 


1. [P = E(mx)](#introduction)
2. [The origin](#ma)


### P = E(mx) <a name="introduction"></a>

It all starts with $$P_t = E_t(m_{t+1}x_{t+1})$$! 

At the heart of many interesting topics in finance such as factor pricing models, market anomalies, return preidiction, time variant risk premimum..etc lies this fundamental asset pricing formula. 

It is amazing that with such a neat equation based on few assumptions, one can price all future payoffs $$x_{t+1}$$ with a stochastic discount factor $$m_{t+1}$$. Through the len of the paradigm with stochastic discount factor, we can extend insights across asset classes from different perspectives such as macro, consumption, production... 

Throughout this blog, I would like to kick off the discussion on the subject of asset pricing with a focus on stochastic discount factor. Where does it come from? what's the implication? how to allign it with real world? these are the questions we hope to address. 


### The Origin <a name="ma"></a>

There are actually several ways to get to the asset pricing formula. I will begin with the one that is based on mimimum assumption and gradually build upon it with more perspectives. 

In its most general form, as long as portfolios with the same payoff have the same price (Law of One Price), there exists such a random variable of stochastic discount factor that prices all payoffs. Let's swtich to the state space of random variable for some intuition. Remember that up to the point t, the payoff $$x_{t+1}$$ of a security is a random variable with different potential realizations in various scenarios. In state space, we can express it explicitly with a vector $$x = [x^{1},...x^{i}...x^{k}]$$, each of the element in the vector represents a realized payoff for a security in correspoding scenario. 

Stacking all securities in the market at time t, we get a matrix $$X = [x_1, ... , x_n]^T$$, whose row space is the payoff space for time t+1. Any payoffs availble in the market lie in this row space. Now with all these machineries we can put the **Law of One Price** in the context as well: any two portfolios $$w_1$$ and $$w_2$$ with same payoff at t+1 $$Xw_1 = Xw_2$$ should have the same price at time t $$Pw_1 = Pw_2$$. 

It's equivalent to say that $$X(w_1 - w_2) = 0$$ leads to $$p (w_1 - w_2)$$ for any two portfolios $$w_1$$ and $$w_2$$. It's easy to notice that price p has to be a member of the payoff space for such condition to hold. Hence there exists a vector $$q = (XX^T)^{-1}XP$$ such that $$P = Xq$$. With simple linear algebras we link the price at time t $$p$$ and payoff at time t+1 $$X$$. 



### Another paragraph <a name="paragraph2"></a>
The second paragraph text


Deviation from Law of One Price. introduce of prob measure. risk premium

equivalent representation in beta 

equivalent of mv. apply for all rn.
rn
