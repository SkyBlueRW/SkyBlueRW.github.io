##

### Convex Optimization: a 101 refresh and further


- [Why should you care?](#introduction)
- [Convex Optimization: what and why?](#convex)
- [Reference](#reference)


#### Why should you care? <a name="introduction"></a>

It is likely that you will agree optimization has become an indispensable tool in the world of finance. Nowdays, it's common to see people using optimizers to decide allocation of resources (like portfolio construction or cash flow management), to determine parameters in model fitting (like regression), to ...

While you may be wondering why you should care about the details under the hood. With abundance of open-source and commercial optimizers available (cvx, mosek, ... the list can goes on and on lasting for more than a page) why shouldn't you simply choose one of them and let the professionals work their magic? How would it help to know a bit more about the details of this magic? Here are my answers 

- **Understanding optimization helps to transform a real world problem into an optimization problem**, which is the crucial first step. How you translate a real world problem into an optimization problem can make a significant difference in solving a real world problem with optimization method. Often, a plain vanilla conveyance  of the real world problem in mathematical language will lead to an unsolvable optimization problem (like risk parity optimization or maximum sharpe ratio optimization). You need to formulate your problem appropriately so that the optimizer can work efficiently.
- **Knowing optimization helps to carry on further analysis on solutions obtained**. It is not always easy to interpret the solution obtained from optimization. Sometimes you even get unintuive solutions (image what you will get from a mean variance optimization with historical mean as expected return). There are ways that helps to evaluate solutions and decision placed in optimization, such as constraint attribution in using Lagrangian decomposition. While knowing optimization is a prerequsite to that.
- **Knowing optimization helps to get a sense of the boundary**. Last but not least, optimzation is not a magical box that can always be solved. It is crutial to know whether an optimization can be solved and to what degree. Is it garuanteed to have a global optimum? Will local optimum provide a reasonable approximation if it's not? As far as I am concerned, there are a bunch of questions to ask yourself when looking into the arsenal of optimization methods during a project.


#### Convex Optimization: what and why? <a name="convex"></a>

I will take "agreed" as your response if you do not close the page yet :) 

Let's start with some refresh on the most important category (in my limited understanding) of optimization problem: convex optimization. 

**What is a convex optimization?** 

In short, convex optimization is the type of optimization in which we minimize a convex function within a convex set. Without loss of generality, a convex optimization can always be fomulated as the following problem where the objective function ($$f_0$$) and the constraint function ($$f_i$$ and $$h_i$$) are convex. The two sets of constraint functions ($$f_i$$, $$h_i$$) define a general convex set.

$$
\begin{aligned}
\min_x {f_0(x)} \\ 
f_i(x) &<= 0, \quad i=1...m\\
h_i(x) &= 0, \quad i=1...p
\end{aligned}
$$


 **why is it so special?**

It is such a special category of optimization that global optimum is guaranteed theoretically (let's ignore all the practical issues like numerical issue, scability issue, etc..). As long as we can formulate a real world problem in the above mentioned format, we are in a terrific position of solving it. 

To add a bit geometrical intuition. Imagine the convex objective function as a valley with increasing (to be more precise: non-decrease) slope in 2D. Finding the minimum point is like rolling down the hill. While the constraint set is like a fence restricting us in a defined area. We can go any point from the area to any other point in a straight line (convex set) hence we can continue rolling before we got to the minimum point.



#### Reference <a name="reference"></a>
- Boyd & Vandenberghe: Convex Optimization
- Cornuejols, Pena & Tutuncu: Optimization methods in Finance
