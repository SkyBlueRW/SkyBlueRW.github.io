##

## Numerical Optimization: a 101 refresh and further


- [Why should you care?](#introduction)
- [Convex Optimization: what and why?](#convex)
- [Numerical algorithms to solve](#solve)
- [Duality: Further Insights](#dual)
- [Summary](#summary)


### Why should you care? <a name="introduction"></a>

It is likely that you will agree optimization has become an indispensable tool in the world of finance. Nowdays, it's common to see people using optimizers to decide allocation of resources (like portfolio construction or cash flow management), to determine parameters in model fitting (like regression), to ...

While you may be wondering why you should care about the details under the hood. With abundance of open-source and commercial optimizers available (cvx, mosek, ... the list can goes on and on lasting for more than a page) why shouldn't you simply choose one of them and let the professionals work their magic? How would it help to know a bit more about the details of this magic? Here are my answers 

- **Understanding optimization helps to transform a real world problem into an optimization problem**, which is the crucial first step. How you translate a real world problem into an optimization problem can make a significant difference in solving a real world problem with optimization method. Often, a plain vanilla conveyance  of the real world problem in mathematical language will lead to an unsolvable optimization problem (like risk parity optimization or maximum sharpe ratio optimization). You need to formulate your problem appropriately so that the optimizer can work efficiently.
- **Knowing optimization helps to carry on further analysis on solutions obtained**. It is not always easy to interpret the solution obtained from optimization. Sometimes you even get unintuive solutions (image what you will get from a mean variance optimization with historical mean as expected return). There are ways that help to evaluate solutions and decision placed in optimization. While knowing optimization is a prerequsite to that.
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

To add a bit geometrical intuition, imagine the convex objective function as a valley with increasing (to be more precise: non-decrease) slope in 2D. Finding the minimum point is like rolling down the hill. While the constraint set is like a fence restricting us in a defined area. We can get to any point from the area to any other point in a straight line (convex set) hence the journey does not stop until the target reached.

In addition, many real world problems can be formulated as convex optimization. For instance, in finance, we model investors' utility toward consumption with a cancave function to express the diminishing utility of consumption. Rational acts according to the maximization of the concave utility function (equivalent to minimization of a convex function) given budget constraint (convex, or more specifically affine set). Similarly, in model calibration, sum of suqared error is a widely used loss function to determin parameter estimates. One more example in portfolio construction, a traditional way to determine portfolio mix with mean and variance can also be modelled as convex optimization easily. 

It is an incredibly useful technique that has a wide range of applications.

### Numerical Algorithms to solve <a name="solve"></a>

With such an optimization problem at hand, we can easily feed it into one of the optimizers and get the optimal solution. However, it's imporant to note that optimizers offer various numerical algorithms to solve the problem, and the choice of algorithm can significantly impact the efficiency of the process. How to choose? It largely depends on questions such as whether the optimization is strongly convex, whether it is huge in dimensions, whether it is large in scale, or whether we have any knowledge of the first or second derivative of the objective function. 

For an optimization with strong convexity structure, the quest for global minimum actually boils down to the quest for local minimum. To find the local minimum, we can start arbitrarily from one X and march toward the direction with the most negative gradient iteratively hence the **Gradient Descent Algorithm**. One iteration of gradient descent is as shown below. $$\alpha$$ is the learning rate that controls how aggressivly do we want to update for one iteration. $$\triangledown f(x)$$ is the first order derivate that governs where to update along the feasible set. 

$$x_{k+1} = x_{k} - \alpha \triangledown f(x_{k})$$

Several strategies can improve this basic version of Gradient descent:
- We can use a **decayed learning rate** to improve the speed of convergence. Essentially to update with larger step size in the initial iterations and to reduce the step size gradually along the iterations for a careful search for the local minimum at later iterations.
- We can use **Gradient descent with moment** to fasten the process by smoothing out noise in derivatives and to jump beyond diminishing gradients. Basically, weighted average of derivatives in the last few iterations instead of the derivative of current step is used for the update of the iteration. The accumulation of derivatives from past few iterations can drag us from potential saddle point and speed up the process if there is a clear trend locally.
- We can further use **RMSprop** to normalize the direction of the derivative. Basically, we scale the derivative along each dimension by respective second moments hence we are moving further for dimensions with smaller historical variation and vice versa. 

Adding all 3 modifications together leads to the famous **ADAM** (Adaptive Momentum Gradient descent) algorithm, which is widely used in the fitting of machine learning models.

So far with various gradient descent algorithms, we have been exclusively focusing on the first derivatives of the objective function. We are actually searching for minimum via a local linear approximation. It is true that as long as we are dealing with a problem with reasonable convex structure, gradient descent can reliably gets the job done, It is not necessarily the most efficient way. Think about the linear approximation we are relying on, to ensure a reasonable local estimate, we will have to restrict us to a relatively small step size because higher derivatives will come into play as the step size gets larger. 

Incoporating second order derivatives (**Newton Method**) can potentially improve the efficiency further. With a second order approximation, the one step update can be as followed, where $$H(x_k)$$ is the hession matrix (second order derivatives). The Newton method can significantly improve the optimization efficiency especially when the objective function is curved. While it is important to note that in practice the computation of reversed hessian matrix can be really expensive when the dimmension of the problem is large. There is actually a tradeoff between more vs less in this decision. In real world, technical modifications (**quasi-Newton** method such as **BFGS** optimization, **Newton GC**, etc) are at our disposal to partly reduce the heavy computations required.

$$x_{k+1} = x_{k} - H(x_k)^{-1} \triangledown f(x_{k})$$

### Duality: Further Insights <a name="dual"></a>

Duality is the unavoidable next stop if we want to gain further insights. It looks a little ambiguous at first glance but makes a lot of sense in various aspects very quickly. In plain English, for a convex optimization in general form as detailed in the first section, duality is to find a lower bound function of the original objective function. The maximization of such a lower bound function leads us to the best lower bound and is called the dual problem of the original primal problem.

The questions now remain **how to get the dual problem** and **what's the point**. 

One way to get a dual problem is to start with the Lagrangian function as shown below. Take the Lagrangian multipler $$\lambda_i$$ and $$v_i$$ as decision variables with infimum with regard to x. 

$$
\begin{aligned}
L(x, \lambda, v) &= f_0(x) + \sum_i^m{\lambda_i f_i(x)} + \sum_i^p{v_i h_i(x)} \\
g(\lambda, v) &= inf_x L(x, \lambda, v)
\end{aligned}
$$

It's clear that $$g(\lambda, v) <= f_0(x)$$ as long as x is feasible ($$f_i(x) <=0, h_i(x) = 0$$) and $$\lambda >=0$$ hence the following dual problem as the best lower bound over the primal problem. 

$$
\begin{aligned}
\max_{\lambda, v} & {g(\lambda, v)} \\
\lambda & >=0
\end{aligned}
$$

The difference between the optimal dual value and the optimal primal value ($$f_0(x^{\star}) - g(\lambda^{\star}, v^{\star})$$) is called **Duality Gap**. Here is one more speciality of convex optimization: the duality gap of convex optimization is almost always (Slater Condition) 0. 

The dual problem is a powerful tool in various perspects.

First and foremost, the dual problem provides a way to do sensitivity analysis upon constraint values. Essentially, the optimal dual solution represents the marginal improvement on primal objective upon relaxation of respective constraint. This optimal dual solution usually has profound economic interpretations (price of resources in equilibirum state, utility improvement given one unit of budget change, etc..Carr & Zhu even have a book called [Convex Duality and Financial Mathematics](https://link.springer.com/book/10.1007/978-3-319-92492-2))

Second, it can be used to simplify complex optimization problems. Often, the dual problem of a complex optimization problem (I.E. L1 norm minimization) can be much simpler than the original problem, making it easier to solve or analyze. Furthermore, For complex optimization problems with strong duality (duality gap to be 0), even analytical solution becomes possible via KKT condition hence provides way more possibilities to carry on further analysis. 

Last but not least, it can be used to prove the optimality of a solution. By solving the dual problem and comparing its objective value with the objective value of the original problem, we can determine whether a given solution is optimal or at least close to optimal. A lot of optimizers out there are actually using the duality gap as a stop criteria to determine the convergence of the algorithm.


### Summary <a name="summary"></a>

With a focus on convex optimization and financial applications, we talked about the meaning, the solver algorithm, and duality of numerical optimizations. I hope you find it relavant and interesting upon reading. If you feel interested in delving deeper, I highly recommend the following books for further reference.

- Boyd & Vandenberghe: Convex Optimization
- Cornuejols, Pena & Tutuncu: Optimization methods in Finance

