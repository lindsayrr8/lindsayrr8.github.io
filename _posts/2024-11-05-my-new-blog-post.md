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
## Question 1.
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

All this seems logical. Let's see what happens when we focus solely on our coefficients and significance with the `summary()` function:
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




