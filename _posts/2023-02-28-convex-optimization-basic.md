##

### Convex Optimization: a 101 refresh and further


1. [Why should you care?](#introduction)


#### Why should you care? <a name="introduction"></a>

It is likely that you will agree optimization has become an indispensable tool in the world of finance. Nowdays, it's common to see people using optimizers to decide allocation of resources (like portfolio construction or cash flow management), to determine parameters in model fitting (like regression), to ...

While you may be wondering why you should care about the details under the hood. With abundance of open-source and commercial optimizers available (cvx, mosek, ... the list can goes on and on lasting for more than a page) why shouldn't you simply choose one of them and let the professionals work their magic? How would it help to know a bit more about the details of this magic? Here are my answers 

- **Understanding optimization helps to transform a real world problem into an optimization problem**, which is the crucial first step. How you translate a real world problem into an optimization problem can make a significant difference in solving a real world problem with optimization method. Often, a plain vanilla conveyance  of the real world problem in mathematical language will lead to an unsolvable optimization problem (like risk parity optimization or maximum sharpe ratio optimization). You need to formulate your problem appropriately so that the optimizer can work efficiently.
- **Knowing optimization helps to carry on further analysis on solutions obtained**. It is not always easy to interpret the solution obtained from optimization. Sometimes you even get unintuive solutions (image what you will get from a mean variance optimization with historical mean as expected return). There are ways that helps to evaluate solutions and decision placed in optimization, such as constraint attribution in using Lagrangian decomposition. While knowing optimization is a prerequsite to that.
- **Knowing optimization helps to get a sense of the boundary**. Last but not least, optimzation is not a magical box that can always be solved. It is crutial to know whether an optimization can be solved and to what degree. Is it garuanteed to have a global optimum? Will local optimum provide a reasonable approximation if it's not? As far as I am concerned, there are a bunch of questions to ask yourself when looking into the arsenal of optimization methods during a project.
