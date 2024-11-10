# Additive Regression and Model Matrices with R

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
Note our two data sets: active treatment (`vas.active`) and placebo treatment `(vas.plac)`. The `act` data frame contains all the measurements for the active treatment group `vas.active`, with additional information about which subject the data comes from `subject`, what the treatment is (`treat = 1`), and the period `period`. Likewise, the `plac` data frame contains all the measurements for the placebo treatment group `vas.plac`, with the same additional information: subject (`subject`), treatment (`treat = 0`), and period (`period`).

## Spectacular. Now it's time to fit our additive model:
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

Alright, so our task is to generate model matrices. (If you're on your last surviving brain cell like I am, remember that a matrix is a two-dimensional data "table" which is set up in rows and columns.)

In `R`, a model matrix is a tool that contains all the values of your independent variables from your data. Essentially, we use it because it makes complicated statistical calculations simpler and easier to work with. And we like simpler and easier!

## Our first step is to set up the factors and variables as instructed:
```R
# Creates factor with 2 levels, each repeated 2 times, length 8
a <- gl(2, 2, 8)  
b <- gl(2, 4, 8)
# Creates factor with 2 levels, each repeated 4 times, length 8
# Sequence from 1 to 8
x <- 1:8        
# Concatenates 1 to 4, followed by 8 to 5
y <- c(1:4, 8:5)
# Generates 8 random values from a normal distribution
z <- rnorm(8)
```
**So what's happening here? Let's break it down.**

The `gl()` function in `R` generates factors by specifying levels and repetitions. For exmaple, `gl(2, 2, 8)` creates a factor `a` with 2 levels, each repeated until the total length is 8. The result looks like this on the inside: `a = 1, 1, 2, 2, 1, 1, 2, 2`

The line `gl(2, 4, 8)` does the same thing, but with 2 levels that are repeated 4 times until reaching a length of 8. On the inside, it looks like: `b = 1, 1, 1, 1, 2, 2, 2, 2`

After creating a sequence of 1 to 8, we assign `y` as a vector that combines `1, 2, 3, 4` with `8, 7, 6, 5`. Then, using our vector `z`, `rnorm()` generates 8 random numbers from a standard normal distribution. 

## Now, our task is to create two separate model matrices for the data:
**1.** 	z ~ a * b: Model with both main effects (a, b) and the interaction (a:b). <br />
**2.** 	z ~ a:b: Model with only the interaction term. <br />

Thankfully, this has already been provided for us, so we only need to fit the models. We'll also be assigning what we get back to objects that we can call later. **Let's set up each step separately to suit the requirements for the exercise**
```R
# Generate the model matrix for the full interaction model (a*b)
full_model_matrix <- model.matrix(~ a * b)
# View the model matrix for the full interaction model
print(full_model_matrix)

# Fit the full model (interaction and main effects)
full_model <- lm(z ~ a * b)
# View the summary stats for the full model
summary(full_model)

# Generate the model matrix for the interaction term only (a:b)
interaction_matrix <- model.matrix(~ a:b)
# View the model matrix for interaction only
print(interaction_matrix)  

# Fit the model with only the interaction term (a:b)
interaction_model <- lm(z ~ a:b)
# View the summary stats for the interaction-only model
summary(interaction_model)
```
Our resulting matrix includes 4 columns for intercept, main effect for `a`, main effect for `b`, and the interaction of `a:b`. All this is to show how these impact `z`. If any columns are dropped in the output we get, it implies that the interaction `a:b` or a main effect for either `a` or `b` isn’t providing unique information in the presence of other terms.

With our initial matrix created for the full interaction model, we can then create and examine subsequent models to compare how they overlap and measure in the presence or absence of the different conditions.

In other words:
- The first block represents the full model matrix.
- The second block represents checking the fit of the full model.
- The third block represents a secondary model matrix that covers only the interaction term (`a:b`).
- The fourth block checks the fit of that model for just the interaction term (`a:b`).

## We can start by interpreting a few insights from the output of our initial, full model matrix:
```R
> # Generate the model matrix for the full interaction model (a*b)
> full_model_matrix <- model.matrix(~ a * b)
> # View the model matrix for the full interaction model
> print(full_model_matrix)
  (Intercept) a2 b2 a2:b2
1           1  0  0     0
2           1  0  0     0
3           1  1  0     0
4           1  1  0     0
5           1  0  1     0
6           1  0  1     0
7           1  1  1     1
8           1  1  1     1
attr(,"assign")
[1] 0 1 2 3
attr(,"contrasts")
attr(,"contrasts")$a
[1] "contr.treatment"

attr(,"contrasts")$b
[1] "contr.treatment"
```
It looks like there was no redundancy or "singularity" in our output, so nothing was dropped.

So, let's get the summary stats and see how well the model fits:
```R
> # Fit the full model (interaction and main effects)
> full_model <- lm(z ~ a * b)
> # View the summary stats for the full model
> summary(full_model)

Call:
lm(formula = z ~ a * b)

Residuals:
      1       2       3       4       5       6       7       8 
-0.2135  0.2135 -0.3768  0.3768 -1.0315  1.0315 -0.3755  0.3755 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)  
(Intercept)   0.3587     0.5900   0.608   0.5761  
a2           -1.7252     0.8344  -2.067   0.1075  
b2           -0.9167     0.8344  -1.099   0.3336  
a2:b2         2.6045     1.1801   2.207   0.0919 .
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.8344 on 4 degrees of freedom
Multiple R-squared:  0.5923,	Adjusted R-squared:  0.2866 
F-statistic: 1.937 on 3 and 4 DF,  p-value: 0.2653
```
A few quick insights from this output can tell us about the fit of this model. Given that our multiple R-squared comes back as 0.5923, this suggests that the model explains only about 59% of the variance for `z`. That's a moderate fit. Our p-value of 0.2653 also suggests that the model as a whole is not statistically significant. That indicates that the relationship between the predictors `a`, `b`, and their interaction for `z` is weak.

## Brilliant. Let's move on to assessing the other model for the interaction only:
```R
> # Generate the model matrix for the interaction term only (a:b)
> interaction_matrix <- model.matrix(~ a:b)
> # View the model matrix for interaction only
> print(interaction_matrix)  
  (Intercept) a1:b1 a2:b1 a1:b2 a2:b2
1           1     1     0     0     0
2           1     1     0     0     0
3           1     0     1     0     0
4           1     0     1     0     0
5           1     0     0     1     0
6           1     0     0     1     0
7           1     0     0     0     1
8           1     0     0     0     1
attr(,"assign")
[1] 0 1 1 1 1
attr(,"contrasts")
attr(,"contrasts")$a
[1] "contr.treatment"

attr(,"contrasts")$b
[1] "contr.treatment"
```
This time, it looks like `a2` was dropped. Therefore, the second model has a singularity.

Right then, we can move on to checking the fit of this model from the summary:
```R
> # View the summary stats for the interaction-only model
> summary(interaction_model)

Call:
lm(formula = z ~ a:b)

Residuals:
      1       2       3       4       5       6       7       8 
-0.2135  0.2135 -0.3768  0.3768 -1.0315  1.0315 -0.3755  0.3755 

Coefficients: (1 not defined because of singularities)
            Estimate Std. Error t value Pr(>|t|)
(Intercept)  0.32134    0.59003   0.545    0.615
a1:b1        0.03734    0.83444   0.045    0.966
a2:b1       -1.68783    0.83444  -2.023    0.113
a1:b2       -0.87937    0.83444  -1.054    0.351
a2:b2             NA         NA      NA       NA

Residual standard error: 0.8344 on 4 degrees of freedom
Multiple R-squared:  0.5923,	Adjusted R-squared:  0.2866 
F-statistic: 1.937 on 3 and 4 DF,  p-value: 0.2653
```
In this case, our multiple R-squared comes back again at 0.5923, meaning that about 59.23% of the variability in `z` can be explained by the interaction between `a` and `b`. Likewise, the same p-value as before is also not statistically significant.

## Conclusion
Both models have essentially the same summary statistics. However, the first (full) model does not have singularities, while the second model (interaction term only) does have singularities. The model with singularities also makes interpreting coefficients inherently less reliable. Ultimately, the models only seem to have moderate explanatory power and do not indicate that `a` and `b` have a strong relationship with `z`. 
