# Regression Modeling with R

This week, we're given the following prompt utilizing the `ashina` data frame in `R`:
> Question 1. 10.1 <br />
Set up an additive model for the ashina data, as part of ISwR package <br />
> This data contain additive effects on subjects, period and treatment. Compare the results with those obtained from t tests.

Putting it simply, an **additive model** is a statistical model where the effects of each independent variable on the dependent variable get added all together. This way you can look at how each variable individually impacts your results.

In statistics-speak, an additive model is a **nonparametric regression method.** This is something we use when we think there is some kind of relationship between variables, but we're not assuming the details. In fact, we can use this in cases where the relationship is both **unknown** and **nonlinear.**

To start with this exercise, we'll set up the model by preparing the data:
```R
# Load the ISwR package and the ashina dataset
library(ISwR)
data(ashina)
```
Simple. Now we just need to set up our data so we can start comparing. The ideal way to do this is to convert the `subject` column to a factor (being categorical data). Then we'll combine the two data sets:
```R
# Convert the subject column to a factor
ashina$subject <- factor(1:16)
# Prepare the data frames for active treatment and placebo
act <- data.frame(vas = ashina$vas.active, subject = ashina$subject, treat = 1, period = ashina$grp)
plac <- data.frame(vas = ashina$vas.plac, subject = ashina$subject, treat = 0, period = ashina$grp)

# Combine the two datasets into one
full_data <- rbind(act, plac)
```







