##

## Numerical Optimization: a 101 refresh and further


- [Why should you care?](#introduction)
- [Convex Optimization: what and why?](#convex)
- [Numerical algorithms to solve](#solve)
- [Reference](#reference)


### Why should you care? <a name="introduction"></a>

It is likely that you will agree optimization has become an indispensable tool in the world of finance. Nowdays, it's common to see people using optimizers to decide allocation of resources (like portfolio construction or cash flow management), to determine parameters in model fitting (like regression), to ...

While you may be wondering why you should care about the details under the hood. With abundance of open-source and commercial optimizers available (cvx, mosek, ... the list can goes on and on lasting for more than a page) why shouldn't you simply choose one of them and let the professionals work their magic? How would it help to know a bit more about the details of this magic? Here are my answers 

- **Understanding optimization helps to transform a real world problem into an optimization problem**, which is the crucial first step. How you translate a real world problem into an optimization problem can make a significant difference in solving a real world problem with optimization method. Often, a plain vanilla conveyance  of the real world problem in mathematical language will lead to an unsolvable optimization problem (like risk parity optimization or maximum sharpe ratio optimization). You need to formulate your problem appropriately so that the optimizer can work efficiently.
- **Knowing optimization helps to carry on further analysis on solutions obtained**. It is not always easy to interpret the solution obtained from optimization. Sometimes you even get unintuive solutions (image what you will get from a mean variance optimization with historical mean as expected return). There are ways that helps to evaluate solutions and decision placed in optimization, such as constraint attribution in using Lagrangian decomposition. While knowing optimization is a prerequsite to that.
- **Knowing optimization helps to get a sense of the boundary**. Last but not least, optimzation is not a magical box that can always be solved. It is crutial to know whether an optimization can be solved and to what degree. Is it garuanteed to have a global optimum? Will local optimum provide a reasonable approximation if it's not? As far as I am concerned, there are a bunch of questions to ask yourself when looking into the arsenal of optimization methods during a project.


### Convex Optimization: what and why? <a name="convex"></a>

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

It is such a special category of optimization that global optimum is guaranteed theoretically. While practical issues such as numerical and scalability problems must be considered, formulating a real world problem in the above mentioned format allows for an terrific chance in finding the solution. 

To add a bit geometrical intuition, imagine the convex objective function as a valley with increasing (to be more precise: non-decrease) slope in 2D. Finding the minimum point is like rolling down the hill. While the constraint set is like a fence restricting us in a defined area. We can go any point from the area to any other point in a straight line (convex set) hence we can continue rolling before we got to the minimum point.

In addition, many real world problems can be formulated as convex optimization. For instance, in finance, we model investors' utility toward consumption with a cancave function to express the diminishing utility of consumption. Rational acts according to the maximization of the concave utility function (equivalent to minimization of a convex function) given budget constraint (convex, or more specifically affine set). Similarly, in model calibration, sum of suqared error is a widely used loss function to determin parameter estimates. One more example in portfolio construction, a traditional way to determine portfolio mix with mean and variance can also be modelled as convex optimization easily. 

It is an incredibly useful technique that has a wide range of applications.

### Numerical Algorithms to solve <a name="solve"></a>

With such an optimization problem at hand, we can easily feed it into one of the optimizers and get the optimal solution. However, it's imporant to note that optimizers offer various numerical algorithms to solve the problem, and the choice of algorithm can significantly impact the efficiency of the process. How to choose? it largely depends on questions such as whether the optimization is strongly convex, whether it is in huge dimension, whether it is large in scale, or whether we have any knowledge of the first or second derivative of the objective function. 

For an optimization with strong convexity structure, the quest for global minimum actually boils down to the quest for local minimum. To find the local minimum, we can start arbitrarily from one X and march toward the direction with the most negative gradient iteratively hence the **Gradient Descent Algorithm**. One iteration of gradient descent is as shown below. $$\alpha$$ is the learning rate that controls how aggressivly do we want to update for one iteration. $$\triangledown f(x)$$ is the first order derivate that governs where to update along the feasible set. 

$$x_{k+1} = x_{k} - \alpha \triangledown f(x_{k})$$

Several strategies can improve this basic version of Gradient descent:
- We can use a **decayed learning rate** to improve the speed of convergence. Essentially to update with larger step size in the initial iterations and to reduce the step size gradually along the iterations for a careful search for the local minimum at later iterations.
- We can use **Gradient descent with moment** to fasten the process by smoothing out noise in derivatives and to jump beyond diminishing gradients. Basically, weighted average of derivatives in the last few iterations instead of the derivative of current step is used for the update of the iteration. The accumulation of derivatives from past few iterations can drag us from potential saddle point and speed up the process if there is a clear trend locally.
- We can further use **RMSprop** to normalize the direction of the derivative. Basically, we scale the derivative along each dimension by respective second moments hence we are moving further for dimensions with smaller historical variation and vice versa. 

Adding all 3 modifications together leads to the famous **ADAM** (Adaptive Momentum Gradient descent) algorithm, which is widely used in the fitting of machine learning models.

So far with various gradient descent algorithms, we have been exclusively focusing on the first derivatives of the objective function. We are actually searching for minimum via a local linear approximation. It is true that as long as we are dealing with a problem with reasonable convex structure, gradient descent can reliably gets the job done, It is not necessarily the most efficient way. Think about the linear approximation we are relying on, to ensure a reasonable local estimate, we will have to restrict us to a relatively small step size because higher derivatives will come into play as the step size gets larger. 

Incoporating second order derivatives (**Newton Method**) can potentially improve the efficiency. With a second order approximation, the one step update can be as followed, where $$H(x_k)$$ is the hession matrix (second order derivatives). The Newton method can significantly improve the optimization efficiency especially when the objective function is curved. While it is important to note that in practice the computation of reversed hessian matrix can be really expensive when the dimmension of the problem is large. There is actually a tradeoff between more vs less in the decision. Technical modifications (BFGS optimization, Newton GC) are at our disposal to partly reduce the heavy computations required.

$$x_{k+1} = x_{k} - H(x_k)^{-1} \triangledown f(x_{k})$$

### Reference <a name="reference"></a>
- Boyd & Vandenberghe: Convex Optimization
- Cornuejols, Pena & Tutuncu: Optimization methods in Finance

