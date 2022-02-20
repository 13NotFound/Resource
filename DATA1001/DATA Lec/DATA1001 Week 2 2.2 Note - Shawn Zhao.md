# Week 2 2.2 Discover Note
## Lecture 4: Data and Qualitative Data
---
## 1. Australian Road Fatality Data
### · Domain Knowledge
Despite preventative measures such as *compulsory seat belts (from 1970)* and *school zones (2001)*, the number of road fatalities in Australia **continues to rise**.
* In 2015, 1,209 died in road fatalities, why?
* We are going to investigate data from the _Australian Bureau of Statistics (ABS)_ for Jan-Apr 2016.
>\* Data: __Information__ about the set of __subjects__ being studied (ex. road fatalities).
* Most commonly, data refers to the __sample__ (parts of the population), not the (entire) **population**.
* Different types of data: survey data, spreadsheet type data, MRI image data, etc.
>\* Initial Data Analysis (IDA): __A first general look__ at the data without formally answering the research questions.
* It can/may:
  * Help you to see whether the data can __answer your questions__.
  * Pose __other__ research __questions__.
  * Identify the __mean qualities__ of the  data.
  * **Suggest the population** from which a sample derives.
* What's involved?
  * Data Background: Check the __quality and integrity__ of the data
  * Data Structure: What __information__ has been __collected__?
  * Data __Wrangling__ (getting data __ready for analysis__): Scarping, cleaning, tidying, reshaping, splitting, combining
  * Data __Summaries__: Graphical and numerical
* For __qualitative and quantitative__ data, we focus on __structure & graphical__ summaries.
* Steps:
  * List 6 top rows of the dataset: `head(dataset)`
  * List x top row(s) of the dataset: `head(dataset,x)`
  * List the number of rows and number of columns: `dim(dataset)` - `dim` as dimension
  * List the names of the variables: `name(dataset)`
  * Classify variables: `str(dataset)` - `str` as structure
  * Isolate a variable: `data$variable`
  * See the length of a variable: `length(variable)`
  * Calculate the sum of a variable (quantitative): `sum(variable)`
  * Sort data in increasing order: `sort(variable)`
  * Sort data in increasing order: `sort(variable, decreasing=T)`
---
### · Structure of the Data
>\* Variable: Something that measures or describes some __attribute__ of the subjects.
* Types of Variables: 
  * __Qualitative/Categorical (Categories)__ (named as __factor__ in R)
    * Ordinal (ordered)
      * Binary (2 categories)
      * 3 + categories
    * Nominal (non-ordered)
      * Binary (2 categories)
      * 3 + categories
  * __Quantitative/Numerical (Measurements)__ (named as __num__ or __numeric__ in R)
    * Discrete (separated)
    * Continuous (continuum)
* Data with _p_ variables is said to have __dimension__ _p_.
  * Univariate: 1 variable
  * Bivariate: 2 variables
  * Multivariate: 2+ variables
>\# `str(data)`, _Structure of Data_
---
### · Graphical Summaries
* The aim of a GS is to best __highlight features__ of this data.
  * Pie chart is popular but not informative.
  * Try *Shiny Apps* (made by R Studio), present data in accessible ways
* Qualitative Data
>\# Bar plot (bar chart, bar graph): is a simple __summary__ of qualitative data.
>1. `Dayweek = data$Dayweek` _(select Dayweek variable from the whole data frame by `data$`)_
>1. `table(Dayweek)` _(Produce a __frequency table__ of fatalities per day of the week--__numerical__)_
>1. `barplot(table(Dayweek))` *(Produce a __bar chart__--__graphical__)* or `plot(table(Dayweek))` _(A simpler version)_
>1. Find out that fatalities are more common in Saturday.
>1. Statistical Thinking (15:33~16:10 in lec 4)
>#### # Double bar plot: 2 quantitative variables
>1. _Select_ `Dayweek` _and_ `Gender` _as variables:_
```R
Dayweek = data$Dayweek
Gender = data$Gender
```
>2. _Produce a **double frequency table** (contingency table):_
```R
data1 = table(Gender,Dayweek)
data1
```
>3. _Use_ `barplot(data1)` _to create a double bar chart (stacked or side-by-side)_
* Big Data
>#### \* Big Data: The __massive amounts of data__ being collected in fields. 
* Big data is __high dimensional__, as they are **more variables _p_ than subjects _n_**.
  * ex. Genomics data can have 3000000 variables.
* Big data requires more complex visualizations.
## 2. Summary
| 1 Qual          | 2 Qual          |
|-----------------|-----------------|
| Simple Bar Plot | Double Bar Plot |

| 1 Quant         | 2 Quant         |
| ----------------| ----------------|
| Histogram/Box Plot | Scatter Plot |

| 1 Qual + 1 Quant |
|----------------------|
| Comparative (side-by-side) Box Plot |
---
## Lecture 5: Quantitative Data
---
## 1. Australian Road Fatality Data (Continue)
### · Primitive Cleaning of the Data (Data Wrangling)
>\# `C` is the __cleaned__ version of the data: `data = read.csv("data/2016FatalitiesC.scv",header=T")`
## 2. Histogram
>\* Histogram __highlights the percentage of data__ in one class interval compared to another.
* It consists of a set of blocks representing the percentages by __area__.
* The area of the whole histogram is __100%__.
* The __horizontal__ scale is divided into __class intervals__.
* The __area__ of each block represents the __percentage of subjects__ in that class interval.
* The __height__ of each block measures __crowding__.
* Choices:
  * No need to add vertical scale.
  * We will mostly use the __density scale__:
  >\* Density Scale: _Height_ of Each Block = _%_ in the block / _Length_ of the Class Interval
  * For continuous data, we need an __endpoint convention__ for data points that __fall on the border__ of 2 class intervals.
    * If an interval contains the left endpoint but excludes the right endpoint, then an 18 year old would be counted in [18,21), not [0, 18).
    * In this case, 18 is the left endpoint, 21 is the right.
    * This is called "__left-closed and right-open__ (__[ )__)"
### · How to produce a histogram by Hand:
* #### 1. Construct the distribution table.
| Class Intervals | Number of Subjects in Interval | % | Height of Block |
|-----------------|--------------------------------|---|-----------------|
| [0,18)          | 29                             | 6.6 | 0.004         |
| [18,25)         | 72                             | 16.4 | 0.023        |
| [25,70)         | 259                            | 58.9 | 0.013        |
| [70,100)        | 80                             | 18.2 | 0.006        |
|                 | 440                            | 100 |               |
#### (Where __Height of Block__ = % per year)
* #### 2. Draw the horizontal axis and blocks.

### · The Speedy Way in R:
1. Read in data. (line 1)
2. Choose a variable. (line 2 - `Age` is the variable, select it by using `data%`)
3. Choose the class intervals. (line 3 - each number represents an endpoint of interval (0-18, 18-25, etc.) - `breaks=c(0,18,25,70,100)`)
4. Produce a distribution table. (line 4 - It means _"create a __table__ of __age__ __cut__ by __breaks__ that's __right__-open"_ - `table(cut(Age,breaks,right=F))`, `F` is False)
#### or:
4. Produce a histogram. (line 5, 6, 7 - `hist` is histogram, `br` means breaks, `freq=F` means produce the hist on the __density scale__, `xlab` is the name for horizontal/x scale, `ylab` is the name for vertical/y/density scale, and `main` is the title of the hist)

```R
data = read.csv("data/2016FatalitiesC.csv,header=T)
Age = data%Age
breaks=c(0,18,25,70,100)
table(cut(Age,breaks,right=F))
or: 
hist(Age,br=breaks,freq=F,right=F,
xlab="Age (in years)", ylab="% per year",
main=Histogram for Age of Road Fatality in Australia: Jan-June 2016")
```
### · Control for a Variable
1. Select female ages only (line 1), and male ages only (line 2)
2. Put the graphic output in `1` *row* with `2` *columns*
3. Produce a histogram of female ages (line 4) and male ages (line 5) both with density scale
```R
AgeF = data$Age[data$Gender=="Female"]
AgeM = data$Age[data$Gender=="Male"]
par(mfrow=c(1,2))
hist(AgeF,freq = F)
hist(AgeM,freq = F)
```
### · Common Mistakes of Histogram
1. Make the block heights **equal** to the percentages.
2. Use **too many** class intervals. (10-15 for maximum)
## 3. Box Plot
* Simple Box Plot
  * Useful for __comparing__ multiple __datasets__.
  * It plots the __median__, the middle 50% of the data in a box, and determines any outliers.
  ```R
  Age = data$Age
  summary(Age)
  par(mfrow=c(1,2))
  boxplot(Age)
  # to make the boxplot horizontally layout, add `horizontal=T`:
  boxplot(Age,horizontal=T)
  ```
* Comparative Box Plots
   * **Split up** a quantitative variable by a quantitative variable.
   ```R
   Gender = data$Gender
   summary(Age[Gender=="Female"])
   summary(Age[Gender=="Male"])
   boxplot(Age~Gender,horizontal=T)
   ```
## 4. Scattered Plot
  * Examine the __relationship__ between 2 quantitative variables.
  ```R
  Speedlimit = data$Speedlimit
  plot(Age,speedlimit)
  ```
---
  ## Lecture 6: Data Visualization
---
  ## 1. Price Point for a Diamond
  ### · Domain Knowledge
* Diamonds are the hardest known natural material and one of the world's major natural resources.
  * Australia has the largest reserves estimated at around 210 million carats.
* Diamonds are used for jewelry (30%, sales of US79 Billion in 2015) and industrial applications (70%).
  * The 59.6 carat Pink Diamond is currently the most expensive gemstone selling for $71.2 million in 2017.
* Pricing Diamonds: buyers need to investigate the price point as each diamond is unique.
  * Diamonds are graded by 4 qualities, known as the "4Cs":
    * Carat (weight)
    * Cut (quality of cut according to proportions, symmetry and polish)
    * Color (color-graded from D-colorless to Z-saturated)
    * Clarity (graded from flawless to inclusions)
### · Diamonds Dataset
* Include the prices and 9 other attributes of 54,000 diamonds.
```R
# Diamonds dataset is already in ggplot2:
install.packages("ggplot2")
library(ggplot2)
or:
install.packages("tidyverse")
library(tidyverse)
diamonds
# Look into its data structure:
str(diamonds)
```
### · Data Visualization (Data Viz)
* Graphical summaries on steriods.
* What determines a good data visualization?
  * Tell an interesting story in visual appealing way (require understanding on both data and design)
  * ex. What questions are we trying to answer?
  * What variables are we highlighting? ...
* What about poor?
  * Tell a story in a visually boring or distracting way (chartjunk)
* Bad?
  * Tell a misleading story *especially in an appealing way!)
### · ggplot2 (Grammar of Graphics Plot 2)
* ggplot allows you to **specify the individual building blocks** of your plot, and then combine them to create just about any kind of visualization you want.
  * The _aesthetic_ `aes` is what you can __see__. ex. position, outside color, inside color (fill), shape of points, etc.
  * The _geometric objects_ `geom_xxx` are the __actual marks__ we put on a plot.
  * The _facet_ is a __subset__ of the data.
* Steps to use:
  1. Install the package.
```R
install.packages("ggplot2")
library(ggplot2)
data = diamonds
```
  2. Check if the data is _tidy_.
  * the data needs to be in a __data frame__, with subjects as rows and variables as columns.
  > \# `head(data,2)`
  3. Check classification of variables.
  > \# `str(data)`
  4. __Sketch__ by hand
  * Sketch what you want to produce, labelling the variables.
  * Write the code.
  5. Run you ggplot and customise to improve visual design.
* Simple Barplot (1 qual)
```R
# Define x axis by 1 variable (cut):
p = ggplot(diamonds,aes(x=cut))
# Represent the data by bar chart:
p + geom_bar()
# Fill the chart with color by a 2nd variable (clarity):
p + geom_bar(aes(fill=clarity))
# Produce a side-by-side graph:
p + geom_bar(aes(fill=clarity),position="dodge")
```
* Histogram (1 quant)
```R
p1 = ggplot(diamonds,aes(x=price))
p1 + geom_histogram(aes(fill=cut))
# Change the width of the bar (bin)
p1 + geom_histogram(aes(fill=cut),binwidth=1000)
```
* Simple Scattered Plot (2 quant)
```R
# Define x axis as carat, y axis as price:
p2 = ggplot(diamonds,aes(x=carat,y=price))
# Represent data by points:
p2 + geom_point()
# Add 1 quant aesthetic: color by 3rd varaible (carat)
p2 + geom_point(aes(color=carat))
# Add 2 qual aesthetic: color by 3rd varaible (clarity), and 4th variable (shape):
p2 + geom_point(aes(color=clarity,shape=cut))
```






