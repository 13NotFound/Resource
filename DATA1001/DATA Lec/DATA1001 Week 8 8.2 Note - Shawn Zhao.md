# Week 8.2 Note
## Lecture 22: Law of Averages
---
## 1. Chance Processes
* Every time you toss a fair coin, there is a __chance variability__:
  - Numbers of Head = Half the number of tosses + Chance Error
  - __Observed value = Expected Value + Chance Error__
> __Law of Large Numbers/Averages__: the proportion of heads become more stable as the __length of the simulation increases__ and approaches a fixed number called __relative frequency__.
* The chance error in the __number of heads__ is likely to be __large__, but __small__ relative to the __number of tosses__.
> __Gambler's Fallacy（赌徒谬论）__: For independent events, it is __wrong to assume the chance of observing an event over time__ even if it has not occurred for a long time.
  - As the number of tosses increases:
    - The absolute size of the chance error increases
    - The absolute percentage of the chance error increases
    - The proportion of event will coverage to the expected proportion.
## 2. Box Model
* A simple wat to describe __chance processes__.
* We need to know:
  - The __distinct numbers__ in the box ("tickets")
  - The __number__ of each tickets in the box
  - The number of __draws__ from the box
* Steps:
  - Think of the __box__ as a summary of the __population__
    - What's in there, and in what proportions.
  - Take __draws__ from the box to create the __sample__
  - Consider the _sum or mean_ of the _sample_
    - What is the expected value (EV)?
    - What is the observed value (OV)?
    - The _chance error_ is _OV - EV_, modelled by __standard error (SE)__.
![EV OV Example](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\EV OV Example.png)
## 3. Applying Box Model to gambling
* Concepts in gambling:
  - The _tickets_ represent the amount _won (+) and lost (-) in each play_.
  - The chance of _drawing a particular value_ is the chance of _winning that amount in 1 play_.
  - The number of _draws_ is the number of _plays_.
  - The _net gain_ is the _sum of the draws_.
* Example: Throw a fair dice 25 times.
  - Box Composition:
  ![Tossing Box Model](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Tossing Box Model.png)
  - Simulation:
  ![25 Tossing Simulation](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\25 Tossing Simulation.png)
* Example 2: Game
  - Model:
  ![Game Modeling](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Game Modeling.png)
  - Box Composition:
  ![Playing Box Model](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Playing Box Model.png)
  - Simulation:
  ![Playing Simulation](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Playing Simulation.png)
* Example 3: Roulette
  - Model:
  ![Roulette Modeling](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Roulette Modeling.png)
  - Box Composition:
  ![Roulette Box Model](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Roulette Box Model.png)
  - Simulation:
  ![Roulette Simulation](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Roulette Simulation.png)
---
## Lecture 2: The Box Model
---
## 1. Modelling the Sum/Mean of a Sample
* __Sum of draws__ from a box model with replacement:
  - ![Sum](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Sum.png)
  - SD of the box:
    - The result for SE is __square root law__ (sqrt(number of draws))
    - Box is a population so the SD of the box is __population SD__.
    - Calculations:
      1. Use `popsd()` in `multicon` package
      2. Formula: RMS(gaps) = Root of the Mean of the Square Gaps
      3. Shortcut: Simple __Binary Boxes__ only
      ![Shortcut](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Shortcut.png)
  - How does chance error _relate to_ standard error?
    - An OV is likely to be around its EV, with a __chance error similar to the SE__.
    - OVs are rarely more than 2 or 3 SEs away from the EVs.
  - Example: WWII Coin Tossing
    - Steps:
      ![SD of Tossing](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\SD of Tossing.png)
      ![EV, OV of Tossing](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\EV, OV of Tossing.png)
    
    - We say that __the chance error 67 is within 2 standard errors (SE = 50)__.
    
      ![In R](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\In R.png)
* __Mean of draws__ from a box model with replacement:
  - __Mean__ of the sample = __Sum__ of the sample / the __number__ of draws
  - ![Mean](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Mean.png)
  - Example: WWII Coin Tossing
    - Steps:
    ![Mean of Tossing](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Mean of Tossing.png)
    ![EV, SE of Tossing](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\EV, SE of Tossing.png)
## 2. The Normal Curve for Modelling
* For __large amounts__ of draws from the box, the __observed value__ of the Sum/Mean often __follows the normal curve__.
* Given a box model, we can work out EV and SE to model.
* Example: A coin is rolled _100 times_. What is the _chance of getting between 40 and 60 heads_?
  - Steps:
    ![Normal Box Model](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Normal Box Model.png)
    ![Normal EV, SE](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Normal EV, SE.png)
    ![Normal Sketching](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Normal Sketching.png)
    ![Normal Chance](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Normal Chance.png)
    ![Normal in R](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Normal in R.png)
    ![Normal Simulation](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Normal Simulation.png)
## 3. Using Box Model for Classifying and Counting
* Often we are just interested in 1 particular ticket in the box (binary box), which may summarize other tickets.
* Example 1: Toss a dice 100 times and count the number of 6s. The box would have one 1 (representing "6"), and five 0 (representing non "6")
* Example 2: Keno Classic
  - Steps:
    ![Keno](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Keno.png)
    ![Keno Box Model](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Keno Box Model.png)
    ![Keno EV, SE](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Keno EV, SE.png)
    ![Keno in R](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Keno in R.png)
    ![Keno Chance](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Keno Chance.png)
    ![Keno Simulation](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Keno Simulation.png)
---
## Lecture 24: Normal Approximation
---
## 1. The Probability Histogram
* 3 Types of Histogram:
  - Data Histogram `hist()`: 
    - Represents data by area
    - ![Data Histogram](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Data Histogram.png)
  - Probability Histogram: 
    - Represents chance by area
    - The __EV__ measures the __centre__ on x-axis.
    - The __SE__ measures the __spread__ on x-axis.
    - ![Probability Histogram 1](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Probability Histogram 1.png)
      ![Probability Histogram 2](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Probability Histogram 2.png)
  - Simulation (empirical) Histogram: 
    - Represents chance by area for a simulation of a chance process
    - Convergence: for repeated simulations of a chance process resulting in a sum, the simulation histogram of the observed values converges to the probability histogram
    - ![Simulation Histogram 1](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Simulation Histogram 1.png)
    - ![Simulation Histogram 2](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Simulation Histogram 2.png)
## 2. Central Limit Theorem（中心极限定理）
> Central Limit Theorem: When __drawing at random with replacement__ from a box, if the __sample size__ for the sum (or average) is __sufficiently large__, then:
* The __probability histogram__ for the sum (or average) will closely __follow the normal curve__.
* Even if the contents of the box does not.
* __More generally, the distribution (behavior of the chances) for the sum (or average) will closely follow the normal curve.__
* Example: Toss a pair of dice 10000 times and calculate the sum. What is the probability of getting a sum between 6 and 8?
  - Method 1:
    ![Method 1](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Method 1.png)
  
  - Method 2:
    ![Method 2 1](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Method 2 1.png)
    ![Method 2 2](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Method 2 2.png)
  
    ![Method 2 3](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Method 2 3.png)
  
  - Method 3:
  ![Method 3](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Method 3.png)
> Continuity Correction (for edges): to approximate a discrete distribution by the normal distribution (continuous), we __adjust the endpoints by 0.5__.
  - The normal curve is __missing part of the area calculated by the data histogram__. To remedy this we adjust by 0.5 either side.
    - Lower Threshold = 6 - 5.5, this has standard unit = -0.6 (approx)
    - Upper Threshold = 8 - 8.5, this has standard unit = 0.6 (approx)
  - To workout whether add of minus 0.5, __draw a sketch of the histogram__.
* Sample Size vs. Replicates
  - Increasing the __replicate__ will approach the __box distribution__.
  - Increasing the __sample size__ will approach the __normal curve__.
  - ![Replicate Example](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 8\Note Materials\Replicate Example.png)
