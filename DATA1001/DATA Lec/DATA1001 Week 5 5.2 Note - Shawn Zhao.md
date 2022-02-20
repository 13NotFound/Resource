# Week 5 5.2 Note
## Lecture 13: Scatter Plot and Correlation
---
## 1. Bivariate Data
> __Bivariate data__ involves a _pair_ of variables.
## 2. Linear Association
> The __linear association__ between _2 variables_ describes how tightly the points _cluster_ around a line.
* If one variable tends to _increase_ with the other, then we have _positive_ association.
## 3. Correlation Coefficient
* How can we summarize a scatter plot?
  * Mean and SD of X (x, SDx)
  * Mean and SD of Y (y, SDy)
  * Correlation Coefficient (r)
* Centre and Spread of the Cloud
  * The __centre__ of the cloud is represented by the point of averages (x, y) (x and y here are means).

  * The __horizontal spread__ of the cloud is measured by _SDx_, we expect most of the points to fall with _2 SDs_ from x.

  * The __vertical spread__ of the cloud is measured by _SDy_, we expect most of the points to fall with _2 SDs_ from y.
  
  ![Centre and Spread](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\Centre and Spread.png)
> __Correlation Coefficient__ (r): A numerical summary which measures the _clustering_ around the line.
* It indicates the sign of strength of the linear association.
* Range: -1 to 1
  * If r is positive: the cloud slopes up.
  * If r is negative: the cloud slopes down.
  * More closer to +1 or -1: the points cluster more tightly.
* The population CC (rpop) is _the mean of the product of the variables_ in __standard units__.
* use `cor()` for CC calculation. ex. `cor (data$fheight, data$sheight)`
## 4. SD Line
> __SD line__ is the line that the points _cluster around_.
* It connects the point of averages (x, y) to (x+SDx, y+SDy for r > 0) or (x, y) to (x+SDx, y-SDy for r < 0)
---
## Lecture 14: Scatter Plot and Correlation
---
## 1. Scatter Plot Example
![Scatter Plot Example](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\Scatter Plot Example.png)

## 2. Properties of Correlation Coefficient
* When r=+1 or -1, all the points lie on a line (no cloud, perfect correlation)
* When r=0, the points don't fit around a line.
* CC is __scale invariant__ (won't change)
## 3. Misleading Correlations
* _Outliers_ can overly influence the CC.
  * Example:
  ```R
  # Add one outlier respectively to both data sets:
  CE1 = c(CE, 100)
  NW1 = c(NW, 20)
  # Calculate the CC of the original:
  cor(CE, NW)
  0.757917
  # Calculate the CC of the new:
  cor(CE1, NW1)
  0.5575432
  # The CC has changed a lot by outliers.
  ```
* Nonlinear association can't be detected by the CC.
* The same CC can arise from different data.
  
  * Example: [Anscombes Quartet](https://www.geeksforgeeks.org/anscombes-quartet/)
* Rates of averages tend to inflate the CC.
  > Ecological correlation (spatial correlation): the correlation between 2 variables that are group means or rates.
  
  * EC tend to overestimate the association between 2 variables.
* Small SDs can make the correlation _look_ bigger.
---
## Lecture 15: Regression Line
---
## 1. Regression Line
* To describe the scatter plot, we need to use the 5 summaries: x, y, SDx, SDy, r.
* The regression line connects (x, y) to (x+SDx, y+SDy)
* Command: `lm()` ex. `lm(NW~CE)`

![Compare Regression Line](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\Compare Regression Line.png)

## 2. The Graph of Averages
* Plot the average y for each x.
* If the GOA is a _straight_ line, that line is the _regression line_.
## 3. Prediction
* Baseline Prediction: 
  
  * Give a _certain value x_, a _basic_ prediction of y would be __the average of y over all the x values__.
* Prediction in a strip:
  
  * Give a _certain value x_, a _more careful_ prediction of y would be __the average of all the y values__ in the data corresponding to __that x value__.
* The Regression Line
  
  * Calculate the regression line, and insert the particular x value we will use.
* Predicting Percentile Ranks
  * If x is in a __certain percentile__ of all the x's, what percentile would we predict the corresponding y to be in?
  * Steps:
    1. Find the z score in the x direction: Zx.
    2. Find the predicted z score in the y direction: Zy=r*Zx
    3. Translate Zy back to the percentile in the y direction.
  * Example:
  ```R
  # Find the percentile using qnorm(), in this example the CE reading is at 90th percentile (90%):
  z_x = qnorm(0, 9)
  # Scale the CC and Zx:
  z_y = cor(CE, NW) * z_x
  # Translate to the y percentile using pnorm():
  pnorm(z_y)
  0.834303
  # Conclusion: When CE reading is at the 90th percentile, the NW reading is at the 83th percentile.
  ```
## 4. Mistakes in Prediction
* Extrapolating
  * If we make a prediction from x that is _not within the data range_, the prediction can be unreliable.

![Extrapolating](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\Extrapolating.png)

* Not Checking the Scatter Plot
  * We can have a high CC and then fit a regression line, but the data may not be linear (more appropriate to use a quadratic model).
---
## Lecture 16: Residual Plot
---
## 1. Residual
> Residual (prediction error): the __vertical distance__ (gap) of a point above and below _the regression line_.
* It represents the error between the actual value and the prediction: ei=yi-^yi, wherew yi is the actual value and ^yi is the prediction.
  * Example:
  ```R
  # Find the regression line:
  l = lm(NW-CE)
  # Use the 10th reading in NW data to minus the prediction (fitted.values):
  NW[10] - l$fitted.values[10]
  10
  -11.41741
  ```
  * Or more quickly:
  ```R
  l$residuals[10]
  10
  -11.41741
  ```
## 2. The RMS Error
* Represent the __average gap__ between the points and the regression line.

![RMS Error](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\RMS Error.png)

* Example:
```R
res = NW - l$fitted.values
sqrt(mean(res^2))
13.22338
```
* For Baseline Prediction:
  * The RMS error is __the SD__ for y.
* Speedy Way for Population RMS Error:

![RMS Quick Formula](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\RMS Quick Formula.png)

* Example:
```R
# For sample:
sqrt(1-(cor(CE, NW))^2)*sd(NW)
13.44196
# For population:
sqrt(1-(cor(CE, NW))^2)*sd(NW)*sqrt((length(CE)-1)/(length(CE)))
13.22338
```
* Special Cases
  * Perfect Correlation: r = +1 or -1
    * RMS Error = 0, as all points lie on the line.
  * r = 0
    * RMS Error = 0, as the regression line is no help in predicting y.
  * Smallest RMS Error
    * The smallest is for the regression line.
## 3. Residual Plot
* Graphs the residuals vs x.
* If the linear fit is appropriate for the data, it should show no pattern.
* Command: `lm$Residuals`
  * Example:
  ```R
  l = lm(NW-CE)
  plot(CE, l$residuals, ylab="residuals")
  ```
## 4. Vertical Strips
* If the VSs on the scatter plot show _equal spread_ in the _y_ direction, then the data is __homoscedastic__.
  
  * The RMS error can be used as a measure of spread for individual strips.
* If not, then the data is __heteroscedastic__.
  
  * The RMS error cannot.
* If _homoscedastic_, then we can use the __normal approximation__ within the VSs.
  * We consider the y within the strip as _y*_ with:
  
  ![VS Normal Distribution](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 5\Note Materials\VS Normal Distribution.png)
  
  * Example:
  ```R
  # Percentage of days that CE is above 90:
  length(which((CE>90)))/length(CE)
  0.09677419
  # Calculate the normal approximation:
  z=(90-mean(CE)/sd(CE))
  1-pnorm(z)
  0.0365018
  ```
---
## Lecture 17: Linear Regression Summary (given bivariate data)
---
* Steps:
1. Produce a scatter plot----does it look _linear_?
1. Produce a regression line: y = a + bx
1. Calculate the CC (r)----how strong is the _linear regression_?
1. Produce a residual plot----does it look _random_? Is linear model good?
1. Check assumptions----does the data look _homoscedastic_?
1. Perform predictions----predict y for given x and y within a VS