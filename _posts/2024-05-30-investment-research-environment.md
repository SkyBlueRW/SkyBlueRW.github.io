#

## A Fun Try into Building an Integrated Research Environment

- [Where it begins](#beg)
- [How it is for the moment](#now)
- [placehoder](#hold)

### Where and how it begins <a name="beg"></a>

The genesis of this endeavor sprouted a couple of years back when I found myself knee-deep in research, craving efficiency and scalability. The repetitive nature of tasks like data cleansing and performance tracking began to feel tedious, making me wonder: could there be a more streamlined approach?

Of course, I am not aiming to develop a universally optimized system to accomodate all investment research needs. Research projects vary significantly in thir requirements, making such an endeavor impractical as a personal hoby. 

Instead, a lightweight version that distills universal componenets across many different projects that I am interested in became my goal. The dream is a system where frequently used models, data sources and update processes are neatly organized into modules for each reuse. Hence onece an idea hit, I can quickly implement it into a calculation unit based on existing tools and deploy it for data update process for historical and on-going performance monitor.



### How it is for the moment <a name="now"></a>

To me, the crux of achieving this goal lies in abstraction and modularization—distilling reusable calculations and processes into manageable units. This dream has, to a large extent, materialized through following design and implementation.

![Structure](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/environment_structure.png)

The development of this environment seamlessly intertwined with ongoing research projects. Often, it merely required an additional step beyond project requirements. For instance, while delving into portfolio construction models, it usually involves common elements like matrix operations and convex optimization. Rather than treating them as isolated instances, I invested time in abstracting them into reusable functions or classes within organized packages. This foresight drastically reduces future efforts when similar topics resurface.

Following this thought, when integrating data from new sources, I would always prefer building standardized APIs to deliver data in a consistent format. Although this approach demands additional time initially, the long-term benefits are immense. These APIs become versatile tools, usable across various scenarios, from one-time research tasks to ongoing monitoring, thus fostering an integrated research environment with synchronized inputs.

The culmination of such abstractions comprises the first two components of my research environment: the Data API and Libraries of Models and Tools.

In the Data API, diverse data sources are wrapped within standardized modules and functions to yield aligned outputs. Here, special attention is paid to avoid lookahead bias, ensuring data is used appropriately in historical simulations after its release. Additionally, common data cleaning and merging methods—such as accounting statement preprocessing and calendar handling—are incorporated to expedite further data manipulation and usage across diverse applications.

Similarly, frequently used low-level calculations (e.g., numerical methods, statistical procedures) and high-level models (e.g., nowcasting, Black-Litterman allocation) are encapsulated within distinct packages under the Libraries section.

Together, these modules fulfill the initial half of my goal—enabling the reuse of previous code to accelerate the implementation of new ideas. Now, attention shifts to the latter half: apply relavant calculation to common scenarios with a data update pipeline. Regardless of the underlying models, they can be abstracted into a series of data calculation units dependent on each other. This module orchestrates the necessity of calculations, executes them accordingly, and logs the outcomes. For example, when developing a new alpha signal based on accounting statements, I can focus on the calculation aspect with the aid of APIs and libraries. Once calculations for a period are completed, with specified dependencies and frequencies, the module can generate historical and ongoing data.

Moreover, further subsequent calculations—such as historical long-short performance or strategy formulation—build upon this foundational data calculation layer.


### placehoder <a name="hold"></a>

This is the investment research environment I've envisioned. I have dedicated some time every once a while to the development of this system over the past couple of years. There's a unique satisfaction in the development process, distinct from research. In research, the thrill often stems from understanding or finding a solution. In contrast, the satisfaction of development grows gradually. With each line of code, I inch closer to realizing this vision.

![System](https://raw.githubusercontent.com/SkyBlueRW/SkyBlueRW.github.io/main/_posts/asset/system.png)

Some of the packages mentioned:

- [DataRepo](https://github.com/SkyBlueRW/DataRepo)
- [Backtest](https://github.com/SkyBlueRW/Backtest)
- [PortCon](https://github.com/SkyBlueRW/PortCon)

Build the wheel when you need it!
