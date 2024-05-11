#

## A Fun Try into Building an Integrated Research Environment

- [Where it begins](#beg)
- [How it is for the moment](#now)
- [placehoder](#hold)

### Where and how it begins <a name="beg"></a>

The idea emerged a couple of years ago when I started to have some research results and hoped to do more! Those 'hard liftings' like tracking on-going performance of existing reserach and clearning data for new research seem more and more repeatative and tedious. Hence my wondering - wouldn't it be amzing to have a system to scale on all of it?

Of course, I am not looking to develop a well optimized system that can support all kinds of investment research. For one hand, research projects are distinct in their natures - different analysis is applied on various data sets to answer different questions of interest. More importantly, it's just too heavy as a personal hobby :). 

A lite version that summarizes some universal pieces across research projects to help me focus more on the fun part would already be good enough! The dream is that those frequently used models and data sources are organized in modules easy for repeated use. Hence once an idea hit, I can quickly implement it into a calculation unit based on existing function and deploy it for check in historical simulation as well as onging monitor with easy configurations.


### How it is for the moment <a name="now"></a>

To me, the key of achieving the goal is about abstraction and modularization - to abstract calculations and process that are likely to be reused, modularize them into pieces for divide and conque.  More or less, the dream have come true, with the following design. 

![Structure](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/environment_structure.png)

The development of the environment actually took place seeminglessly along side with the going of other research projects. A lot of times, it just took one more step on top of what is already required. For example, every time when looking into a portfolio construction model, it is quite likely that there involves steps like matrix operations and convex optimization. In this case, rather than implementing it as a one shot deal, take a bit more time to have it abstracted as re-usable functions or classes in organized packages would save a lot of efforts the next time when a related topic is re-visited.  

Following the thought, if there is a need to collect data from a new data source, I would always prefer to build a standardized api to output data in a designed format and take extra effort to fetch it in a point in time manner. Obviously it will extra time, while the benefit comes that the api can be easily used in all kind of scenarios like one time research, historical simulation and ongoing monitor, faciliating the establish of an integrated research environment with aligned input in all the activities.

These kinds of abstraction conclude the first 2 components of my research environment - Data API and Libraries of Models and Tools.

In Data API, various data sources are wrapped around standardized modules and functions to output data in a more aligned format. As mentioned above, special attention here is paid to avoid the looking ahead bias - using data in historical simulation before it is available! Additionally, those commonly used methods to clean and merge data such as accounting statement preprocess, calendar handling, etc. Everything built here serves the prupose of outputing a pre-processed data set that can save as much time as possible for further data cleaning and can be used a variety of use cases.

Whereas those frequently used low level calculations like neumerical methods, statistical procedures, portfolio bactest and high level modelings like nowcast, black-litterman allocation, performance allocations are summarized accordingly in different pacakges under the library section. 

All these modules in data api and libraries fufill the first half of the goal. Previous codes can be used in large extend for a new idea hence fastening the implementation! Now it comes to the other part of the goal. Once there is some results in a project, it's usually the case that we want to check its performance in different scenarios. Like for a new portfolio construction method, get a function implemention of transforming input into a portfolio is just the first step, the logical next step is to have it calculated for different scenarios hincluding history and onging out of sample.

This demand is handdled in the last part of the data update module. Despite different models. They all can be abstracted in to a series of data calculation unit depending on each other that requires calculation upon certain event. A data update module that can check the necessity of calculation, call the calculation accordingly and save and logging the cauculation would be of tremendous help. For example, with this data update pipeline, when it comes to the development of a new alpha signal about accounting statement. I can focus on the calculation of this factor with the help of all apis and libraries. With the calculation figured out for one period, with configurations about the dependency of this calculation as well as calculation frequency, the package can calculate data for history and on-going.

Similary other further calculations on top of this factor calculation such as historical long short performance of this factor, a strategy using this factor etc are simply another additional layer of calculation. 

### placehoder <a name="hold"></a>

So this is the investment research environment that. I have dedicated some time every once a while to the development of this system imagined in the next couple of years. There is a distinct kind of fun from the development than from a research project. In research, the excitement a lot of time is from finally understanding something or figuring out a solution, the aspiration arrives as a nice surprise after reading and verifying into the data. While when it comes to development, the joy of satisfaction arives gradually. With every line of new codes written, I feel I get a little bit close to this.

![System](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/system.png)

- [DataRepo](https://github.com/SkyBlueRW/DataRepo)
- [Backtest](https://github.com/SkyBlueRW/Backtest)
- [PortCon](https://github.com/SkyBlueRW/PortCon)

Build the wheel when you need it!
