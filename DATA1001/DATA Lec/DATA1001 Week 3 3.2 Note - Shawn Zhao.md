# Week 3 3.2 Discover Note
## Lecture 7: Centre
---
## 1. Numerical Summaries
* Reduce all the date to __1 simple number__ ("statistic")
  * This loses a lot of information...
  * ...but allows __easy communication and comparison__.
* Major Features:
  * Maximum
  * Minimum
  * Centre (mean, median)
  * Spread (standard deviation, range, IQR)
## 2. Mean and Median
> Mean（平均数）: the average of the data.
* Mean = Sum of data/Size of data
* Commands:
```R
# Calculate the mean:
mean(data$Sold)
# To focus specifically on a variable/variables: 
mean(data$Sold[data$Type=="House" & data$Bedrooms=="4"])
# ↑ It means that only choose "houses" with "4" bedrooms in the data of all the property sold.
```
* Mean is the __balancing point__ in the data. On a histogram:
```R
# Create a histogram:
hist(data$Sold, main="Newtown Properties", xlab="Price (in 1000s)")
# Add a vertical (v) "green" (col=) line (adline) of mean:
abline(v=mean(data$Sold), col="green")
```

![Mean](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 3\Note Materials\Mean.png)

> Median（中位数）: the __middle data point__, when the data is ordered from _smallest to largest_.
* Median = 
  * the unique middle point (in an _odd_ sized dataset)
  * the average of the 2 middle points (in an _even_ sized dataset)
* Commands:
```R
# Order the data (ranked data):
sort(data$Sold)
# Measure the length:
length(data$Sold)
# Calculate the median:
median(data$Sold)
# To focus specifically on a variable/variables: 
median(data$Sold[data$Type=="House" & data$Bedrooms=="4"])
```
* Median is the __half way point__ in the data. On a histogram:
```R
# Create a histogram:
hist(data$Sold)
# Add a vertical (v) "purple" (col=) line (adline) of median:
abline(v=median(data$Sold), col="purple")
```

![Mean and Median](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 3\Note Materials\Mean and Median.png)

* Both on a boxplot:
```R
boxplot(data$Sold, main="Newtown Properties")
abline(v=mean(data$Sold), col="green")
abline(v=median(data$Sold), col="purple")
```

![Mean adn Median Boxplot](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 3\Note Materials\Mean adn Median Boxplot.png)

## 3. Robustness and Comparisons
> Robustness（顽健性）: The median is said to be __robust__ and is a good summary for skewed data as it is _not affected by_ __outliers__.
>
> #### Comparison: The difference between the mean and the median can be an indication of the __shape__ of the data.

| Data Types | Mean Compared to Median |
|------------|-------------------------|
| Symmetric | Same |
| Left Skewed | Smaller |
| Right Skewed | Larger |
---
## Lecture 8: Spread
---
## 1. Standard Deviation
* To measure the spread, we can calculate the `gaps`.
* Commands:
```R
# Measure all the gaps:
gaps = data$Sold - mean(Data$Sold)
# To check the maximum in the gaps:
max(gaps)
```
![Gaps](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 3\Note Materials\Gaps.png)

> #### RMS(Root Mean Square)（均方根）: the average of a set of numbers, regardless of the signs.
* Steps (in _S-M-R_ order): _square_ the numbers, then _mean_ the result, then _root_ the overall result:
* Commands:
```R
# Apply RMS to the gaps:
sqrt(mean(gaps^2))
```
> SD (Standard Deviation)（标准差）: measures the spread of the data.
* _Difference_ between RMS and SD: RMS is based on __population__, while SD is based on __samples__. So, SD may need to multiply `sqrt(n-1/n)` to make the result on population (n).
* Commands:
```R
# Calculate the standard deviation:
sd(data$Sold)
# Adjusting (to make the sd equal to RMS)
sd(data$Sold)*sqrt(55/56)

# Another convenient way by installing multicon package:
install.packages("multicon")
library(multcon)
popsd(data$Sold) # popsd means sd on population
```
## 2. Standard Units (Z Score)
* Standard Units = (data point - mean) / SD
* For many data sets, we find that roughly:

| percentage of Data | Distance from Mean |
|--------------------|--------------------|
| 68%                | Within 1 SD        |
| 95%                | Within 2 SDs       |
| 99.7%              | Within 3 SDs       |
> __Standard Unit__ of A Data Point = how many standard deviations are below the mean.
>
> #### IQR (Interquartile Range)（四分位距）: Range of the __middle 50%__ of the data.
* IQR = Q3 (3rd Quartile) - Q1 (1st Quartile)
  * The median is the 50% or 2nd quartile (Q2)
* Commands:
```R
# List all the quartiles of the data:
quantile(data$Sold)
# Calculate the IQR:
quantile(data$Sold)[4] - quantile(data$Sold)[2]
```
![IQR](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 3\Note Materials\IQR.png)

> IQR on a boxplot: The __length of the box__ in the boxplot, representing the span of __50%__.
* The __lower__ and __upper thresholds__ are a distance of 1.5 from the quartiles:
  * LT: Q1 - 1.5IQR
  * UT: Q3 + 1.5IQR
  
* Data outside these thresholds is considered an __outlier__ (Extreme reading).

  ![IQR Boxplot Visual](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 3\Note Materials\IQR Boxplot Visual.png)
## 3. Reporting
* IQR and median are both __robust__, so they are suitable for __skewed data__.

* We report in pairs: (mean, SD) or (median, IQR)
## 4. Coefficient of Variation
> CV (Coefficient of Variation)（变异系数）: __Combines the SD and mean++ into 1 summary.
* CV = SD/Mean
* Commands:
```R
m = mean(data$Sold)
sd = sd(data$Sold)
sd/m
```
---
## Lecture 9: Data Wrangling
---
> Data Wrangling: Whatever is needed to get the data for analysis, also known as data munging or data janitor work.
* Steps:
  * Sourcing data
  * Scarping data
  * Cleaning and tidying data
  * Reshaping data
  * Splitting data
  * Combining data
  * Summarising data