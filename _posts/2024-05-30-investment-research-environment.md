#

## A Fun Try into Building an Integrated Research Environment

- [Where it begins](#beg)
- [How it is for the moment](#now)

### Where and how it begins <a name="beg"></a>

The idea emerged a couple of years ago when I started to have some research results and hoped to do more! Those 'hard liftings' like tracking on-going performance of existing reserach and clearning data for new research seem more and more repeatative and tedious. Hence my wondering - wouldn't it be amzing to have a system to scale on all of it?

Of course, I am not looking to develop a well optimized super system that can support all kinds of investment research. For one hand, research projects are distinct in their natures - different modeling is applied on various data sets to answer different questions of interest. More importantly, it's just too heavy as a personal hobby :). 

A lite version that summarizes some universal pieces across research projects to help me focus more on the fun part would already be enough! The dream is that those frequently used models and data sources are organized in modules easy for repeated use. Hence once an idea hit, I can quickly implement it into a calculation unit based on existing function and deploy it for check in historical simulation as well as onging monitor with easy configurations.


### How it is for the moment <a name="now"></a>

To me, the key of achieving the goal is about abstraction and modularization - to get calculations and process that are likely to be reused, modularizing them into pieces for divide and conque.  More or less, the dream have come true, with the following design. 

![Structure](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/environment_structure.png)

The development of the environment actually took place seeminglessly along side the going of other research projects. A lot of times, it just took one more step on top of what is already required. For example, every time when looking into a portfolio construction model, it is quite likely that there involves steps matrix operations and convex optimization. In this case rather than implementing it as a one shot deal, take a bit more time to have it abstracted a re-usable functions or classes in a package would save a lot effort the next time when a related topic is re-visited.  

Similarly, if there is a need to collect data from a new data source, I would always prefer to build a standardized api to output data in a designed format and take extra effort to use it in a point in time manner. Obviously it will take more time, while the benefit comes that the api can be used easily in all kind of scenarios like one time research, historical simulation and ongoing monitor, faciliating the establish of an integrated research environment with aligned input in all the activities.

These kinds of abstraction conclude the first 2 components of the research environment - Data API and Libraries of Models and Tools.

In Data API, various data sources are wrapped around standardized modules and functions to output data in a more aligned format. As mentioned above, special attention here is paid to avoid the looking ahead bias - using data in historical simulation before it is available! Additionally, those commonly used methods to clean and merge data such as accounting statement preprocess, calendar handling, etc. Everything built here serves the prupose of outputing a pre-processed data set that can save as much time as possible for further data cleaning and can be used a variety of use cases.

Whereas those frequently used low level calculations like neumerical methods, statistical procedures, portfolio bactest and more high level modelings like nowcast, black-litterman allocation, performance allocations are summarized accordingly in different pacakges under the library section. 

All these modules in data api and libraries fufill the first half of the goal, previous codes can be used in large extend for a new idea hence fastening the implementation! Now it comes to the second half of the goal. Once there is some results in a project, it's usually the case that we want to check its performance in different scenarios. Like for a new portfolio construction method, get the 



![System](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/system.png)





I have dedicated some time every once a while to the development of this system imagined in the next couple of years. There is a distinct kind of fun from the development than from a research project. In research, the excitement a lot of time is from finally understanding something or figuring out a solution, the aspiration arrives as a nice surprise after reading and verifying into the data. While when it comes to development, the joy of satisfaction arives gradually. With every line of new codes written, I feel I get a little bit close to this.

Build the wheel when you need it!
