# Week 4 4.2 Note
## Lecture 10: Normal Curve (Model)
---
## 1. Normal Curve
* Why is it important?
  * It approximates many _natural phenomenon_.
  * It can model data caused by _a large number of independent variables_.
> The __general__ normal curve (X) has __any mean and SD__.

> The __standard__ normal curve (Z) has __mean 0 and SD 1__.
* The normal curve formula is:
  * ![GNC Formula](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 4\Note Materials\GNC Formula.png)
## 2. Area under Normal Curve
* Approximating Histogram by a Normal Curve
  * If the normal curve fits the histogram, we can use __the area under normal curve__ as an approximation to __the area under the histogram__.
* How to calculate the area under a _standard normal curve_?
  * `pnorm()` works out the lower __tail area__.
    * ex. `pnorm(x, lower.tail=F)` works out the _right_ tail area (which is `upper tail`).
  * For _intervals_, we do `pnorm()-pnorm()`.
    * ex. `pnorm(0.8)-pnorm(0.3)` = area between 0.3 and 0.8
* How to calculate the area under a _general normal curve_?
  * `pnorm(x,y,z)`, where x is the _scale_, y is the _mean_, z is the _standard deviation_.
## 3. Special Properties of the Normal Curve
1. All normal curves satisfy the __68%-95%-99.7% rule__.
  * Which is:

| percentage of Data | Distance from Mean |
|--------------------|--------------------|
| 68%                | Within 1 SD        |
| 95%                | Within 2 SDs       |
| 99.7%              | Within 3 SDs       |

* Visually: ![68-95-99.7](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 4\Note Materials\68-95-99.7.png)
2. Any GN can be rescaled into SN.
  * Steps:
    1. standardize the __thresholds__ (data points) of the general  using __standard units__ (relevant points on the standard) = (data point - mean) / SD
    2. The new standard units are the thresholds of the new standard.

  * ex.1 ![rescale](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 4\Note Materials\rescale.png)

    ![rescale1](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 4\Note Materials\rescale1.png)

  * ex.2 ![rescale2](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 4\Note Materials\rescale2.png)

    ![rescale3](E:\All C Disk Disposal\USYD\课程\DATA1001 - Foundations of Data Science\Week 4\Note Materials\rescale3.png)
---
## Lecture 11: Measurement Error
---
## 1. Measurement
* An individual measurement often differs from the exact value.
  * Individual Measurement = Exact Value + Chance Error + Bias
## 2. Chance Error
* Measurement will always turn out differently due to _chance error_.
* To estimate the chance error, we __replicate__ the measurement under the same conditions and calculate the __standard deviation__.
## 3. Outliers
> Outliers: A small part of __extreme measurements__ in large series of measurements.
>
> *  Standard units (Distance from data from the mean) can tell the outliers.
## 4. Bias
> Bias (systematic error): __A constant amount__ added to or subtracted from __each measurement__.
* Bias can be deliberate or accidental.
---
## Lecture 12: Reproducible Reports
---
## 1. R Markdown
> R Script: A text file which saves the R code and comments "#".

> R Markdown: An authoring framework for data science which produces dynamic and interactive documents with R
* It combines:
  * Chunks of text
  * Embedded code
  * Latex
* Customize Code Chunk:
  * Echo = F: Don't show code (only show the output)
  * Eval = F: Don't evaluate result
* Put R code in text:
  * ex. Write:
    * This is an example `r 1+1`.
  * It will be rendered as:
    * This is and example 2.








​    