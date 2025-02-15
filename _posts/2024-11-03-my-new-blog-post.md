# Multivariate Analysis with R

Briefly, multivariate analysis is a statistical approach to **analyzing the relationships between multiple variables simultaneously.** This is especially useful when working with big datasets involving complex relationships.

To experiment with multivariate analysis with R, we're tasked with answering the following questions:
> **Question 1.** <br />
> Conduct ANOVA (analysis of variance) and regression coefficients on the data from data ("cystfibr") database. You can choose any variable you like to interpret. In the report, you need to state the result of coefficients and significance to any variables you like both under ANOVA and multivariate analysis. Please provide a specific interpretation of R results. <br />
> *and* <br />
> **Question 2.** <br />
> The secher data("secher") are best analyzed after log-transforming birth weight as well as the abdominal and biparietal diameters. Fit a prediction weight as well as abdominal and biparietal diameters. For a prediction equation for birth weight. How much is gained by using both diameters in a prediction equation? The sum of the two regression coefficients is almost identical and equal to 3. Can this be given a nice interpretation to our analysis?
Please provide step by step on your analysis and code you use to find out the result.
> 
As always, we'll be letting `R` handle all of the heavy lifting.
# Question 1.
To begin conducting an ANOVA and regression analysis on `cystfibr`, we first load it into our `R` library and take our initial look at it:
```R
# Load in cystfibr dataset
library(ISwR)
data("cystfibr")

# Inspect dataset
str(cystfibr)
```
And peeking at `cystfibr` reveals the following output:
```R
> # Inspect dataset
> str(cystfibr)
'data.frame':	25 obs. of  10 variables:
 $ age   : int  7 7 8 8 8 9 11 12 12 13 ...
 $ sex   : int  0 1 0 1 0 0 1 1 0 1 ...
 $ height: int  109 112 124 125 127 130 139 150 146 155 ...
 $ weight: num  13.1 12.9 14.1 16.2 21.5 17.5 30.7 28.4 25.1 31.5 ...
 $ bmp   : int  68 65 64 67 93 68 89 69 67 68 ...
 $ fev1  : int  32 19 22 41 52 44 28 18 24 23 ...
 $ rv    : int  258 449 441 234 202 308 305 369 312 413 ...
 $ frc   : int  183 245 268 146 131 155 179 198 194 225 ...
 $ tlc   : int  137 134 147 124 104 118 119 103 128 136 ...
 $ pemax : int  95 85 100 85 95 80 65 110 70 95 ...
```
It seems there are multiple variables at play that we could work with. Since we have our pick, let's go for `age`, `height`, `weight`, and `sex`. In this case, `age` will be the dependent (response) variable and the others are the independent (predictor) variables. In other words, we're going to try to predict `age` based on `height`, `weight`, and `sex`.

### To translate that into R, we'll be creating our linear model:
```R
# Fit a linear model
model <- lm(age ~ height + weight + sex, data = cystfibr)
```
Sweet. This looks pretty familiar by now. Then we simply pass our model to `anova()`:
```R
# ANOVA test 
anova_results <- anova(model)
print(anova_results)
```
...which gives us the output:
```R
 > print(anova_results)
Analysis of Variance Table

Response: age
          Df Sum Sq Mean Sq  F value    Pr(>F)    
height     1 526.76  526.76 145.4600 6.634e-11 ***
weight     1  11.44   11.44   3.1583   0.09003 .  
sex        1   0.00    0.00   0.0001   0.99283    
Residuals 21  76.05    3.62                       
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1                   
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
## Interpreting the ANOVA results:
- **Df (degrees of freedom):** Each predictor (height, weight, sex) has 1 degree of freedom, while the residuals have 21 degrees of freedom.
- **Sum Sq (Sum of Squares):** Height explains 526.76 of the variation in age, weight explains 11.44 of the variation, and sex explains 0.00, which indicates no variation in age associated with sex.
- **Mean Sq (Mean Square):** Again, for height it is 526.76, for weight it is 11.44, and for sex it is 0.00.
- **F value:** height has an F value of 145.4600, indicating a very strong relationship with age. Weight has an F value of 3.1583, which is weaker. Sex has a low F value of 0.0001, indicating no relationship.
- **Pr(>F) (P-value):** Height has a very small p-value of 6.634e-11, indicating that height is highly significant in predicting age. Weight has a p-value of 0.09003, which is marginally significant. Sex has a p-value of 0.99283, indicating that sex does not significantly affect age.

All this seems logical. Let's see what happens when we focus solely on our **coefficients** and **significance** with the `summary()` function:
```R
> # Check coefficients and significance
> summary(model)

Call:
lm(formula = age ~ height + weight + sex, data = cystfibr)

Residuals:
    Min      1Q  Median      3Q     Max 
-2.9270 -1.1129 -0.3369  0.8373  4.1802 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)   
(Intercept) -11.040546   5.204316  -2.121  0.04595 * 
height        0.142149   0.046302   3.070  0.00581 **
weight        0.098872   0.055856   1.770  0.09122 . 
sex           0.007107   0.781185   0.009  0.99283   
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1.903 on 21 degrees of freedom
Multiple R-squared:  0.8762,	Adjusted R-squared:  0.8585 
F-statistic: 49.54 on 3 and 21 DF,  p-value: 1.061e-09

> 
```

As for **Residuals:**
- These values indicate how the residuals are distributed:
- **Min:** -2.9270
- **1Q (First Quartile):** -1.1129
- **Median:** -0.3369
- **3Q (Third Quartile):** 0.8373
- **Max:** 4.1802
The distribution seems to be fairly symmetric, meaning the model fits the data well enough.

As for **Coefficients:**
- **(Intercept):**
**Estimate:** -11.040546
This is the predicted value of age when all independent variables (height, weight, sex) are zero. However, this interpretation is not practically meaningful because no one can have a height of -11 in the real world.
- **Significance:** p-value of 0.04595 indicates that the intercept is statistically significant at the 0.05 level.
- As for **height:** this tells us more of the same; it suggests that for each one-unit increase in height, age is expected to increase by approximately 0.142 years, holding weight and sex constant. In other words, height is a significant predictor of age. Who'd've thunk it?
- As for **weight:** weight is also suggests that for each one-unit increase in weight, age is expected to increase by about 0.099 years, holding height and sex constant. In other words, weight increases with age. That makes sense. At a p-value of ~0.09, there is not enough significance for interest.
- As for **sex:** it seems consistent throughout the data that sex does not have much to do with predicted age.

## Concluding thoughts:
The model shows that height is a strongly significant predictor of age, while weight may have a weak influence, and sex has essentially no influence. That checks out.

# Question 2:
For this, we're instructed to log-transform the birth weight, the abdominal, and the biparietal diameters, and build regression models using the "secher" dataset.

## To start, we'll import the requested dataset:
```R
# Load the dataset
data("secher")
# Initial view of dataset
head(secher)
```
Taking a look at its structure reveals what we're working with:
```R
> # Initial view of dataset
> head(secher)
   bwt bpd  ad no
1 2350  88  92  1
2 2450  91  98  2
3 3300  94 110  3
4 1800  84  89  4
5 2900  89  97  5
6 3500 100 110  6
```
## Cool. What is a log-transformation and why do we use it?
Essentially, a log-transformation means we take the **logarithm** of each value in a dataset, which **"compresses" large numbers** more than small ones. This helps when we have data with a wide range of values or a skewed distribution. Log-transforming makes the data more evenly distributed, so our analysis and predictions can become more reliable.

Lucky for us, `R` offers a pre-packaged `log()` function that we can use to do this quickly and easily.
```R
# Log transformation on variables
secher$log_bwt <- log(secher$bwt)
secher$log_ad <- log(secher$ad)
secher$log_bpd <- log(secher$bpd)
```
In English, these read: from the `secher` dataset, take the specified column and use `log()` to create a new column with the resulting values. Store the results in the original dataset in new columns that are named with "log" tacked on, respectively.

Splendid. Now that we've done that, we can run `head(secher)` to check out our result:
```R
> head(secher)
   bwt bpd  ad no  log_bwt   log_ad  log_bpd
1 2350  88  92  1 7.762171 4.521789 4.477337
2 2450  91  98  2 7.803843 4.584967 4.510860
3 3300  94 110  3 8.101678 4.700480 4.543295
4 1800  84  89  4 7.495542 4.488636 4.430817
5 2900  89  97  5 7.972466 4.574711 4.488636
6 3500 100 110  6 8.160518 4.700480 4.605170
```
...And there's our new columns. Well done.

## Now, we can use the data we calculated to create our new linear models.
The first one will be a simple **single-predictor model.** We will do one of each for both `log(ad)` and `log(bpd)`.
```R
# Create log ad predictor model
model_ad <- lm(log_bwt ~ log_ad, data = secher)
summary(model_ad)
# Create log bpd predictor model
model_bpd <- lm(log_bwt ~ log_bpd, data = secher)
summary(model_bpd)
```
Here, we're checking to see how well `log_bwt` can be predicted by either `log_ad` or `log_bpd`. And it results in the following output:
```R
> # Create log ad predictor model
> model_ad <- lm(log_bwt ~ log_ad, data = secher)
> summary(model_ad)

Call:
lm(formula = log_bwt ~ log_ad, data = secher)

Residuals:
     Min       1Q   Median       3Q      Max 
-0.58560 -0.06609  0.00184  0.07479  0.48435 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -2.4446     0.5103  -4.791 5.49e-06 ***
log_ad        2.2365     0.1105  20.238  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.1275 on 105 degrees of freedom
Multiple R-squared:  0.7959,	Adjusted R-squared:  0.794 
F-statistic: 409.6 on 1 and 105 DF,  p-value: < 2.2e-16
```
A brief, simple takeaway from this result is that a higher `log_ad` generally predicts a higher `log_bwt`. Since the p-value for log_ad is well below 0.05, we can say with high confidence that abdominal diameter is a significant predictor of birth weight in this model. Our low residual standard error value and R-squared value of about ~80% also indicate that our model is a good fit for the data.

As for `log_bpd`, we get the output:
```R
> # Create log bpd predictor model
> model_bpd <- lm(log_bwt ~ log_bpd, data = secher)
> summary(model_bpd)

Call:
lm(formula = log_bwt ~ log_bpd, data = secher)

Residuals:
     Min       1Q   Median       3Q      Max 
-0.36478 -0.09725  0.01251  0.07703  0.51154 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -7.0862     0.9062  -7.819 4.35e-12 ***
log_bpd       3.3320     0.2017  16.516  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.1488 on 105 degrees of freedom
Multiple R-squared:  0.7221,	Adjusted R-squared:  0.7194 
F-statistic: 272.8 on 1 and 105 DF,  p-value: < 2.2e-16
```
This boils down to a larger `bpd` generally predicting a higher `bwt`. The p-values here are also statistically significant. Our residual standard error is is slightly higher than the previous model, which still suggests that the model is a reasonably good fit. Our R-squared of about ~72% also shows that there is still a strong relationship, although not as high as in the previous model.

## Why not both?
Actually, we can do both. And it might give us a more accurate overall model. We can set it up like this:
```R
# Create model including both to predict log(bwt)
model_combined <- lm(log_bwt ~ log_ad + log_bpd, data = secher)
summary(model_combined)
```
Running the summary of our new, combined model results in:
```R
> summary(model_combined)

Call:
lm(formula = log_bwt ~ log_ad + log_bpd, data = secher)

Residuals:
     Min       1Q   Median       3Q      Max 
-0.35074 -0.06741 -0.00792  0.05750  0.36360 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -5.8615     0.6617  -8.859 2.36e-14 ***
log_ad        1.4667     0.1467   9.998  < 2e-16 ***
log_bpd       1.5519     0.2294   6.764 8.09e-10 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.1068 on 104 degrees of freedom
Multiple R-squared:  0.8583,	Adjusted R-squared:  0.8556 
F-statistic: 314.9 on 2 and 104 DF,  p-value: < 2.2e-16
```

## Interpreting the combined results:
The coefficients all seem to indicate statistical significance. The result is that both predictors are significant. In terms of residuals, the model shows that it is a good fit for the data.

The standard residual error value is small. The multiple R-squared and adjusted R-squared are also both about ~85%, indicating that the vast majority of the variance in `log_bwt` is explained by  the combined effects of `log_ad` and `log_bpd`.

The F-statistic's very low p-value also indicates that the model, including both predictors, significantly improves predictions of log_bwt compared to a model with no predictors. That's pretty strong support for the combined predictive power of `log_ad` and `log_bpd.`

## Concluding thoughts
- Both abdominal and biparietal diameters have a meaningful and statistically significant relationship with birth weight.
- The sum of the coefficients for `log_ad` (about 1.47) and `log_bpd` (about 1.55) is close to 3. This means that when they increase together, the combined effect on `log_bwt` is roughly a 3-unit increase per 1-unit increase in both predictors.
- Therefore, both variables contribute meaningfully and independently to the outcome.

