# Week 7 7.2 Note
## Lecture 19: Chance
---
## 1. The Prosecutor's Fallacy（检察官谬误）
> The prosecutor's fallacy is a statistical mistake that assumes the __chance of a random match__ _equal_ to the __chance of defendant's innocence__.
* __Low chance of matching the evidence provided, high chance that the person is guilty.__
* Example:
  - Fact:
    - Suppose there are 5 million people in Sydney.
    - A murder occurs with _DNA left_, and _a person matching_ that is arrested.
  - Faulty Arguments:
    - The chance of DNA match is _1 in 500000_ (very __small__).
    - So, the _chance_ that the arrested person is _guilty_ is very __high__.
  - Error in Thinking:

    | Type | DNA Match | DNA not Match |
    |------|-----------|---------------|
    |Guilty|1|0|
    |Innocent|9|4,999,990|
  - Note:
    - Only 1 person is guilty and has a DNA match.
    - No one (0) is guilty and has not matched the DNA.
    - If the chance of matching is 1/500000, then 10 people are expected to match (1 guilty, 9 innocent)
    - This leaves 4,999,990 people not matching.
  - Hence:
    - The chance that innocent person __has a DNA match__ is tiny.
      - P(DNA Match | Innocent) = 9/4,999,999
    - The chance that a DNA matched person is __innocent__ is high.
      - P(Innocent | DNA Match) = 9/10
    - P(DNA Match | Innocent) is __not equal__ to P(Innocent | DNA Match)
    - __So we can't say P(Guilty|DNA Match) is high for a DNA matched person.__
      - P(Guilty | DNA Match) = 1 - P(DNA Match | Innocent) = 1 - 9/4,999,999
## 2. Properties of Chance
> Chance (probability): the __percentage of time__ a certain event is expected to _happen_, if the same process is _repeated_ long-term.
* Basic Properties:
  1. Chances are between __0%__ (impossible) and __100%__ (certain).
  1. The chance of something equal to __100% minus its opposite (complement)__. —P(Event) = 1 - P(Complement Event)
  1. Drawing at __random__ means that a collection of objects have __the same chance of being picked__.
## 3. Conditional Probability
> Conditional Probability（条件概率）: the chance that __a certain event occurs__, given __another event has occurred__. —P(Event 1 | Event 2)
* Multiplication Principle: 
  * The probability of 2 events occur is __the chance of 1st event multiplied by the chance of 2nd event__, _given the 1st event has occurred.
  * __P(Event 1 and Event 2 Occur) = P(Event 1) x P(Event 2 | Event 1)__
> Independence（独立性）: 2 events are _independent_ if __the chance of 2nd given the 1st is the same as the 2nd__. —__P(2nd Event | 1st Event) = P(2nd Event)__
* Drawing randomly with _replacement_ ensures independence.
* P(Event 1 and Event 2 occur) = P(Event 1) x P(Event 2)
* Example: the rain yesterday is irrelevant to the rain today.
> Dependence（依靠性）: 2 events are _dependent_ if __the chance of 2nd given the 1st is not the same as the 2nd__. —P(2nd Event | 1st Event) not= P(2nd Event)__
* Drawing randomly without _replacement_ ensures dependence.
---
## Lecture 20: More Chance
---
## 1. Making Lists
* For simple chance problems, a good way to start:
  * Write a list of all outcomes
  * Count which outcomes belong to the event of interest.
    - This can lead to a simple way to summarize the outcomes, or use a probability rule.
    - This can also generalizing complicate problems.
* Example: Throw 2 dice. What is the chance of getting a total of 6 spots?
* Write a full list and count the outcomes:

  ![Outcomes](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 7\Note Materials\Outcomes.png)
* Summarize in a tree diagram:![Tree Outcomes](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 7\Note Materials\Tree Outcomes.png)
* Simulate using R:
```R
# Start the simulation:
set.seed(1)
totals = sample(1:6, 1000, rep = T) + sample(1:6, 1000, rep = T)
# Introducing commands:
# sample(): create the sample for simulation, each one represents a dice
# 1:6: the sample is from 1 to 6 (numbers on the dice)
# 1000: repeat the simulation for 1000 times
# rep = T: use replacement to make each simulation independent

# Create a table:
table(totals)
```
![Table](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 7\Note Materials\Table.png)

* So the chance of getting a total of 6 is 148/1000 = 0.148, very close to 5/36.
## 2. Addition Rule
> Mutually Exclusive（相互排斥）: 2 things are mutually exclusive if __one event prevents the other__.
* If 2 things are ME, then the chance of at least 1 occurring is __the sum of individual chances__.
* __P(At least 1 event occurs) = P(Event 1) + P(Event 2)__
---
## Lecture 21: Binomial Formula
---
## 1. Binomial Coefficients
* We can work out the exact chance of P by using the binomial model.
* Suppose we have n objects in a row, made up 2 types: x(type 1) and n - x(type 2):
  * __The number of ways of rearranging the n objects__ is given by the __binomial coefficient__: (__n!__)
  
    ![Binomial Coefficient](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 7\Note Materials\Binomial Coefficient.png)
* Example:
Show (6 2) = 15.
```R
choose(6, 2)
# Output:
15
```
## 2. Binomial Model
> Binary Trial: the case where only 2 things can occur (binary outcomes). So, __P(Event) = p and P(not Event) = 1 - p__.
* __If each trial is dependent (without replacement), then we cannot use binomial model.__
* Binomial Theorem:

  ![Binomial Theorem](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 7\Note Materials\Binomial Theorem.png)

  * Example: A fair coin is tossed 5 times. What is the probability of getting 3 heads?
  ```R
  # dbinom(x, y, z):
  # x - event: we want 3 heads (the event)
  # y - time: we toss it 5 times
  # z - the probability of getting a head is 50% (0.5)
  dbinom(3, 5, 0.5)
  # Output:
  0.3125
  ```