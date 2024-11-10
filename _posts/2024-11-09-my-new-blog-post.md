# Regression Modeling with R

This week, we're given the following prompt utilizing the `ashina` data frame in `R`:
> **Question 1.** 10.1 <br />
Set up an additive model for the ashina data, as part of ISwR package <br />
> This data contain additive effects on subjects, period and treatment. Compare the results with those obtained from t tests.

Putting it simply, an **additive model** is a statistical model where the effects of each independent variable on the dependent variable get added all together. This way you can look at how each variable individually impacts your results.

In statistics-speak, an additive model is a **nonparametric regression method.** This is something we use when we think there is some kind of relationship between variables, but we're not assuming the details. In fact, we can use this in cases where the relationship is **unknown** and **nonlinear.**

## To start with this exercise, we'll set up the model by preparing the data:
```R
# Load the ISwR package and the ashina dataset
library(ISwR)
data(ashina)
# Take a look at ashina
head(ashina)
str(ashina)
```
And running `head(ashina)` and `str(ashina)` gives the following output:
```R
> head(ashina)
  vas.active vas.plac grp
1       -167     -102   1
2       -127      -39   1
3        -58       32   1
4       -103       28   1
5        -35       16   1
6       -164      -42   1
> str(ashina)
'data.frame':	16 obs. of  3 variables:
 $ vas.active: int  -167 -127 -58 -103 -35 -164 -3 25 -61 -45 ...
 $ vas.plac  : int  -102 -39 32 28 16 -42 -27 -30 -47 8 ...
 $ grp       : int  1 1 1 1 1 1 1 1 1 1 ...
```
Simple. Now we just need to set up our data correctly so we can start comparing. The ideal way to do this is to convert the `subject` column to a factor (being categorical data). Then we'll combine the two data sets:
```R
# Convert the subject column to a factor
ashina$subject <- factor(1:16)
# Prepare the data frames for active treatment and placebo
act <- data.frame(vas = ashina$vas.active, subject = ashina$subject, treat = 1, period = ashina$grp)
plac <- data.frame(vas = ashina$vas.plac, subject = ashina$subject, treat = 0, period = ashina$grp)

# Combine the two datasets into one
full_data <- rbind(act, plac)
```
Note our two data sets: active treatment (`vas.active`) and placebo treatment `(vas.plac)`. The `act` data frame contains all the measurements for the active treatment group (`vas.active`), with additional information about which subject the data comes from (`subject`), what the treatment is (`treat = 1`), and the period (`period`). Likewise, the `plac` data frame contains all the measurements for the placebo treatment group (`vas.plac`), with the same additional information: subject (`subject`), treatment (`treat = 0`), and period (`period`).

Spectacular. Now it's time to fit our additive model:
```R
# Fit the additive model
additive_model <- lm(vas ~ subject + treat + period, data = full_data)

# Display a summary of the additive model
summary(additive_model)
```
In English, our model says we're looking at the independent effects of the variables (`subject`, `treat`, and `period`) on the dependent variable (`vas`).


