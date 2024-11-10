# Additive Regression and Basic Model Matrices with R

This week, we're given the following prompt utilizing the `ashina` data frame in `R`:
> **Question 1.** 10.1 <br />
Set up an additive model for the ashina data, as part of ISwR package <br />
> This data contain additive effects on subjects, period and treatment. Compare the results with those obtained from t tests.

Putting it simply, an **additive model** is a statistical model where the effects of each independent variable on the dependent variable get added all together. This way you can look at how each variable individually impacts your results.

In statistics-speak, an additive model is a **nonparametric regression method.** This is something we use when we think there is some kind of relationship between variables, but we're not assuming the details. In fact, we can use this in cases where the relationship is unknown or nonlinear.

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
In English, our model says we're looking at the independent effects of the variables `subject`, `treat`, and `period` on the dependent variable `vas`.

Running the summary provides us with the output:
```R
> # Display a summary of the additive model
> summary(additive_model)

Call:
lm(formula = vas ~ subject + treat + period, data = full_data)

Residuals:
   Min     1Q Median     3Q    Max 
-48.94 -18.44   0.00  18.44  48.94 

Coefficients: (1 not defined because of singularities)
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -113.06      27.39  -4.128 0.000895 ***
subject2       51.50      37.58   1.370 0.190721    
subject3      121.50      37.58   3.233 0.005573 ** 
subject4       97.00      37.58   2.581 0.020867 *  
subject5      125.00      37.58   3.326 0.004604 ** 
subject6       31.50      37.58   0.838 0.415070    
subject7      119.50      37.58   3.180 0.006215 ** 
subject8      132.00      37.58   3.513 0.003142 ** 
subject9       80.50      37.58   2.142 0.049003 *  
subject10     116.00      37.58   3.087 0.007518 ** 
subject11     121.50      37.58   3.233 0.005573 ** 
subject12     154.50      37.58   4.111 0.000925 ***
subject13     131.00      37.58   3.486 0.003318 ** 
subject14     125.00      37.58   3.326 0.004604 ** 
subject15      99.00      37.58   2.634 0.018768 *  
subject16      80.50      37.58   2.142 0.049003 *  
treat         -42.87      13.29  -3.227 0.005644 ** 
period            NA         NA      NA       NA    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 37.58 on 15 degrees of freedom
Multiple R-squared:  0.7566,	Adjusted R-squared:  0.4969 
F-statistic: 2.914 on 16 and 15 DF,  p-value: 0.02229
```
## Interpreting these results
At first glance, there are a few takeaways:
- Many subjects (such as subject3, subject5, subject7, etc.) have p-values < 0.05, meaning their coefficients are statistically significant. This suggests individual differences in the `vas` scores across subjects.
- The treatment coefficient (treat) is also significant (p = 0.0056), suggesting that treatment has a notable effect on the outcome (`vas` score).
- `period` came back with "NA", which means it was either redundant or had no variation.
- Our multiple R-squared value came back as 0.7566, indicating that approximately 75.7% of the variability in `vas` scores is explained by the model (which is reasonably high.)
- However, the adjusted R-squared value came back as 0.4969, suggesting that the model might only explain around 49.7% of the variability in the data.

In other words, it seems the model has some explanatory power, but some predictors aren't significantly contributing to predicting the outcome.

## Running t-tests on the data:
To run t-tests on the two data sets, we simply use R's built-in `t.test()` function:
```R
# Compare the results with t-tests
# For active treatment vs placebo
t.test(vas ~ treat, data = full_data)
# For subjects' period effects
t.test(vas ~ period, data = full_data)
```
And running this block of code gives the results of our t-tests:
```R
> # Compare the results with t-tests
> # For active treatment vs placebo
> t.test(vas ~ treat, data = full_data)

	Welch Two Sample t-test

data:  vas by treat
t = 2.4699, df = 24.063, p-value = 0.02099
alternative hypothesis: true difference in means between group 0 and group 1 is not equal to 0
95 percent confidence interval:
  7.052494 78.697506
sample estimates:
mean in group 0 mean in group 1 
       -13.9375        -56.8125 

> # For subjects' period effects
> t.test(vas ~ period, data = full_data)

	Welch Two Sample t-test

data:  vas by period
t = -1.8995, df = 29.872, p-value = 0.0672
alternative hypothesis: true difference in means between group 1 and group 2 is not equal to 0
95 percent confidence interval:
 -64.613318   2.346651
sample estimates:
mean in group 1 mean in group 2 
      -47.05000       -15.91667
```

## Given this output, we have a few primary takeaways:

As for the treatment t-test:
- The t and p values returned as statistically significant, which indicates a noticeable difference in `vas` scores between the treatment and placebo groups.
- The mean vas score for the placebo group (group 0) is -13.94, and for the active treatment group (group 1), it’s -56.81. This implies that the active treatment generally has a lower `vas` score, which checks out with the additive model’s finding of a significant treatment effect.

And the placebo t-test showed:
- The t and p values seem to not be statistically significant. In other words, it suggests no significant difference between the `vas` scores over the two periods.
- There is some observable difference between the means, but not enough to warrant statistical significance. 

## Comparing the results of the additive model and the t-tests:
Overall, both the additive model and the t-test for treatment agree that treatment has a significant impact on `vas` scores. This supports the conclusion that treatment type (active vs. placebo) affects the outcome.

The additive model excludes period due to redundancy, while the t-test results show a lack of statistical significance. Both methods indicate that period does not meaningfully contribute to explaining the `vas` outcome, aligning in their conclusions about period.

# Question 2:
> 10.3. <br />
> Consider the following: <br />
> a <- g1(2, 2, 8) # Creates factor with 2 levels, each repeated 2 times, length 8 <br />
> b <- g1(2, 4, 8) # Creates factor with 2 levels, each repeated 4 times, length 8 <br />
> x <- 1:8 <br />
> y <- c(1:4, 8:5) <br />
> z <- rnorm (8) <br />
> 
> Note: <br />
> The rnorm() is a built-in R function that generates a vector of normally distributed random numbers. The rnorm() method takes a sample size as input and generates that many random numbers. <br />
> 
> Your assignment is to generate the model matrices for the models. <br />
> 
> z ~ a*b  #Model with interaction (a*b), <br />
> z ~ a:b  #Model with only interaction term (a:b)). <br />
> In your assignment, please discuss the implications. Please be reminded about the model fits and notice which models contain singularities. <br />
> *Hint:* <br />
> *We are looking for: model.matrix (~ a:b); lm (z ~ a:b)* <br />





