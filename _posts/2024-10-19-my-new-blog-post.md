# Linear Regression with R

Linear Regression is an important concept in predictive analytics. But what do we use it for? ***Simple Linear Regression*** is a way to describe a relationship between two variables. Typically, we think of these two variables as a **dependent variable** and an **independent variable.** Equivalent terms that we'll be using for these variables are the **response and predictor variables,** respectively.

The word "regression" in this context literally refers to a measurement of a relationship between two variables. However, it might also make some sense to apply the alternate definition of regression here, which means to return to a previous or more basic state.

I like to associate it with the idea of untying a knot. When a shoelace, for example, is tied into a neat bow, someone just stumbling upon it for the first time might have difficulty figuring out where the knot begins and ends (or frankly, what the heck happened here.) Thankfully, with shoes as in mathematics, we've developed a process to untie the knot, making it simpler and easier to figure out how the knot works at each step in the process. That way, we can derive a reasonable explanation for how 'A' probably led to 'B.'

However, it's very important to note that linear regression **does not inherently describe a causal relationship.** The relationship it finds (or doesn't find) could indeed turn out to be causal in the real world, but at minimum, we can only know for certain from our initial analysis if the relationship is *correlational.* **That's what linear regression does: it describes correlation.** 

With that in mind, correlation can be either positive or negative. **Positive correlation** means that the relationship trends in an "upward" or positive pointing way (ex: 1, to 5, 10, 20+). Conversely, **negative correlation** means that the relationship trends in a "downward" or negative pointing way (ex: 1, -5, -10, -20+). Using linear regression, we look for a summary of this trending relationship in the form of a **best fitting line.** It is what it sounds like: a line that essentially follows the direction of the data.

Under the hood, this is accomplished by minimizing the sum of the squared distances between the line and the actual data points on a scatter plot. Thankfully, as always, *we will be letting R handle this for us.*

## This week, we're asked to evaluate several questions to demonstrate working knowledge of analyzing linear regression problems in R.

## Question 1:
> The datasets in this assignment: <br />
> 
> x <- c(16, 17, 13, 18, 12, 14, 19, 11, 11, 10) <br />
> y <- c(63, 81, 56, 91, 47, 57, 76, 72, 62, 48) <br />

> **1.1 Define the relationship model between the predictor and the response variable;** <br />
> **1.2 Calculate the coefficients** <br />

First thing's first: remember that "predictor variable" = independent variable and "response variable" = dependent variable.

So, we have our data sets and our tasks. First, let's let R handle finding the "relationship model" between the sets. We can do this using R's built-in `lm()` function ("lm" stands for linear model.")

```R
# Define the datasets
x <- c(16, 17, 13, 18, 12, 14, 19, 11, 11, 10)
y <- c(63, 81, 56, 91, 47, 57, 76, 72, 62, 48)

# Create a linear regression model
model <- lm(y ~ x)

# View the summary of the model
summary(model)
```
### What are we looking at here? Let's break it down line by line.

Did we really just create a linear regression model using basically 2 lines of code? Yes we did! (Thank you, `R`!)
```R
# Create a linear regression model
model <- lm(y ~ x)
```
In this case, the formula `Y ~ X` translates in English to: "response variable ('Y') is explained by ('~') the predictor variable ('X')." Computers really are short on words, aren't they? Note that 'Y' and 'X' represent their respective response/predictor variables by convention using this formula. In other words, when we're talking about `lm()`, 'Y' is always the response/dependent variable and 'X' is always the predictor/independent variable.

In `R`speak, `Y ~ X` is instructing `R` to predict 'Y' using 'X'.

We've talked about the `summary()` function in `R` before. Here's the output we get when we run it and instruct `R` to tell us what it found:
```R
Call:
lm(formula = y ~ x)

Residuals:
    Min      1Q  Median      3Q     Max 
-11.435  -7.406  -4.608   6.681  16.834 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)  
(Intercept)   19.206     15.691   1.224   0.2558  
x              3.269      1.088   3.006   0.0169 *
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 10.48 on 8 degrees of freedom
Multiple R-squared:  0.5303,	Adjusted R-squared:  0.4716 
F-statistic: 9.033 on 1 and 8 DF,  p-value: 0.01693
```
Look at all that tasty data! Just think of all the time this is going to save in the future. (I'm definitely thinking about that right now!)

### Now, how do we interpret these results?
#### For Question 1.1:
We already know that **this is a linear relationship model** because that's what `lm()` does. We also know that **Y is the response variable** and **X is the predictor variable.**

As for our `"Residuals:"`
- Min = The largest *negative* difference between the actual and predicted values.
- 1Q (1st quartile) = The point at which 25% of the residuals are below this value.
- Median = The middle residual (half the residuals are above, half below).
- 3Q (3rd quartile) = The point at which 75% of the residuals are below this value.
- Max = The largest *positive* difference between the actual and predicted values.
<br />

Cool. But then...
### How do we calculate the coefficients?
#### For Question 1.2:
Thanks to `summary()`, we have all the numbers we need already. Now we need to interpret them using **the regression equation:** <br />
**Y = a + bX + e**
###### *(Editing note: MathJax y u no parse equations. Also, I am not a front-end dev.)*

*Wait... that equation looks familiar...* Yes. Beginning algebra is back to haunt us. But thankfully all we have to do is plug and play since `R` has already done the heavy lifting.

The **coefficients** are the values that define the linear relationship between X and Y. In the output, there are two rows under `"Coefficients":` **(Intercept) which is 'a' and 'x' which is slope.** **These two are our coefficients.** Let's look at this snippet of the output again and interpret the information under Coefficients:
```R
Coefficients:
            Estimate Std. Error t value Pr(>|t|)  
(Intercept)   19.206     15.691   1.224   0.2558  
x              3.269      1.088   3.006   0.0169 *
---
```
**Starting with `(Intercept)`:**
- **Estimate** is value of 'a' in our regression equation. It's also the value of Y when X = 0. So, when X is 0, the model predicts that Y would be ~19.206.
- **Std. Error** measures the accuracy of the estimate. The bigger the standard error compared to the estimate suggests that our estimate might not be very precise.
- **t value** is a measure of how far the estimate is from 0 in terms of our standard errors. Higher values suggest more confidence in the estimate.
- **Pr(>|t|)** is our p-value. It tells us how likely it is that the intercept could be zero. That would mean there's no relationship at all between our variables. A high p-value (greater than 0.05) means that it's not statistically significant.

**Now, onto `x` (Slope):**
- **Estimate** is the value of 'b' in our regression equation. It tells us the slope of the line. Here we see that for every 1 unit increase in X, the value of Y increases by ~3.269 units.
- **Std. Error** measures the accuracy of the slope estimate. Again, a larger error suggests we lack precision and a smaller error value means our estimation is more precise.
- **t value** measures how far the slope is from 0 in terms of standard errors. Since it's bigger than 2, we can say the slops is statistically significant.
- **Pr(>|t|)** is the p-value, which tells us the probability that the slope could be zero. If it was 0, that would mean there's no relationship between X and Y. In this case, since our value is less than 0.05, it indicates that the relationship is statistically significant.

This means that the Estimate for our (Intercept) value 'a' is 19.206 and our Estimate value for our 'x' (Slope) is 3.269. Therefore, the relationship between variables X and Y is given when we plug those values into our equation:
$$
y = 19.206 + 3.269x
$$





