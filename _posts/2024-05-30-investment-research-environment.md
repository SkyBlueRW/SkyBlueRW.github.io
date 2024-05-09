#

## A Fun Try into Building an Integrated Research Environment

- [Where it begins](#beg)
- [How it is for the moment](#now)

### Where and how it begins <a name="beg"></a>

The idea emerged a couple of years ago when I started to have some research results and hoped to do more! Those 'hard liftings' like tracking on-going performance of existing reserach and clearning data for new research seem more and more repeatative and tedious. Hence my wondering - wouldn't it be amzing to have a system to scale on all of it?

Of course, I am not looking to develop a well optimized super system that can support all kinds of investment research. For one hand, research projects are distinct in their natures - different modeling is applied on various data sets to answer different questions of interest. More importantly, it's just too heavy as a personal hobby :). 

A lite version that summarizes some universal pieces across research projects to help me focus more on the fun part would already be enough! The dream is that those frequently used models and data sources are organized in modules easy for repeated use hence once an idea hit, I can quickly implement it into a calculation unit based on existing function and deploy it for check in historical simulation as well as onging monitor with easy configurations.


### How it is for the moment <a name="now"></a>

To me, the key of achieving the goal is about abstract functions, calculations and process that are likely to repeat, modularizing them into pieces and divide and conque.  More or less, the dream have come true, with the following design. 

![Structure](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/environment_structure.png)

The development of the environment actually took place seeminglessly along side the going of other research projects. A lot of times, it just took one more step on top of what is already required. For example, every time when looking into a portfolio construction model, it is quite likely that there involves steps of convex optimization and matrix operations. In this case rather than implementing it as a one shot deal, take a bit more time to have it abstracted as re-usable functions and classes in a package would save a lot effort the next time when a related topic is re-visited.  

Similarly, if there is a need to collect data from a new data source, I would always prefer to build a api to output data in a designed format and take extra care to use it in a point in time manner. Obviously it will take more time, while the benefit comes that the api can be used easily in one time research, historical simulation and ongoing monitor, faciliating the establish of a research environment. Also keep the input aligned in all the activities.


1. pre data - api
2. tools, likely use existing tools - modularization. Historical backtest. No gaurantee, but do
3. monitor new clues about effective paper trading. 


![System](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/system.png)

https://www.limina.com/blog/integrated-investment-management-solutions
https://www.linkedin.com/pulse/integrated-investment-management-structure-associated-mircea/


I have dedicated some time every once a while to the development of this system imagined in the next couple of years. There is a distinct kind of fun from the development than from a research project. In research, the excitement a lot of time is from finally understanding something or figuring out a solution, the aspiration arrives as a nice surprise after reading and verifying into the data. While when it comes to development, the joy of satisfaction arives gradually. With every line of new codes written, I feel I get a little bit close to this.
