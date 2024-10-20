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
<br />

This means that the Estimate for our (Intercept) value 'a' is 19.206 and our Estimate value for our 'x' (Slope) is 3.269. Therefore, the relationship between variables X and Y is given when we plug those values into our equation: <br />

**y = 19.206 + 3.269x** <br />


## Question 2:
Here, we'll be applying more of the same approach with a few extras:
> *(The following question is posted by Chi Yau, the author of  R Tutorial With Bayesian Statistics Using Stan and his blog post regarding Regression analysis.)* <br />

> Problem -
> Apply the simple linear regression model for the data set called "visit" (see below), and estimate the the discharge duration if the waiting time since the last eruption has been 80 minutes.
> head(visit) 
  discharge  waiting 
1     3.600      79 
2     1.800      54 
3     3.333      74 
4     2.283      62 
5     4.533      85 
6     2.883      55 
> 
> Employ the following formula:
> *discharge ~ waiting* and data=visit)
> 
> **2.1** Define the relationship model between the predictor and the response variable. <br />
> 
> **2.2** Extract the parameters of the estimated regression equation with the coefficients function. <br />
> 
> **2.3** Determine the fit of the eruption duration using the estimated regression equation. <br />

### Okay, we have three different tasks to complete with this prompt.
#### For Question 2.1:
First, we'll define the relationship model and specify the variables, since we already know from the last exercise what those will be thanks to the formula: <br />

```R
# Create data frame for discharge duration and waiting time
visit <- data.frame(
  discharge = c(3.600, 1.800, 3.333, 2.283, 4.533, 2.883),
  waiting = c(79, 54, 74, 62, 85, 55)
)
# Viewing the data frame
head(visit)

# Define the linear relationship model
model <- lm(discharge ~ waiting, data = visit)
```

Here, we're inputting our data to `R` as two vectors within a data frame. Then, we use the `lm()` function again to create a linear model using the data from our discharge duration and waiting times. In this case, `discharge` is the response variable (Y) and `waiting` is the predictor variable (X), because our **hypothesis** is that: changes in waiting time (X) will lead to changes in the discharge duration (Y).

**Remember: Y is the response variable (in this case, `duration`) and X is the predictor variable (in this case, `waiting`.)**

Notice that this time, since we pulled our data from a data frame, our formula looks a little different on this line:
```R
model <- lm(discharge ~ waiting, data = visit)
```
What we see here is the same formula, only we've specified to `R` the data frame from which we're taking the data. In `R` speak, it says: "look for `discharge` and `waiting` in the data frame called `visit`."

Sweet. So, we have our data, we have linear regression model, and now it's time to get our coefficients.

Before, we used the `summary()` function that we're familiar with to get this information. That helped us understand what the model returns so we could interpret what we were looking at. But what if I told you there's an even simpler way to get the coefficients?

Yes, that's right. `R` has another handy-dandy built-in function for us: `coefficients()`
```R
# Create data frame for discharge duration and waiting time
visit <- data.frame(
  discharge = c(3.600, 1.800, 3.333, 2.283, 4.533, 2.883),
  waiting = c(79, 54, 74, 62, 85, 55)
)
# Viewing the data frame
head(visit)

# Define the linear relationship model
model <- lm(discharge ~ waiting, data = visit)
  
# Get the coefficients
coefficients <- coefficients(model)
# Call to view stored result
print(coefficients)
```
And the output we get from the `coefficients()` function is:
```R
> # Get the coefficients
> coefficients(model)
(Intercept)     waiting 
-1.53317418  0.06755757 
```
There's our X and our Y. I've stored what `R` returned as our coefficients to the variable `coefficients` so we can use them again easily.

#### Wonderful. We have our linear relationship model, our X and Y variables, our coefficients, and now we'll place them into an estimated regression equation:

**ŷ = -1.533 + 0.068 * X**

Note that yes, this is "y-hat," (another one of my favorite terms.) We use ŷ here because in statistics lingo, plain old 'y' is used to represent actual *observations,* while 'ŷ' is used to represent *predictions.*

#### Now it's time to check out the fit of the discharge duration using our estimated regression equation.

Our task is to do this given that the waiting time (X value) is 80 minutes. This is more of the same deal, only this time we're plugging in '80' for 'X' in the equation:

**ŷ = -1.533 + 0.068 * 80**

If you're mathematically ~~(or, in my opinion, sadistically)~~ inclined, you could calculate this by hand and the result would be the same. But let's have `R` handle it:
```R
# Create X value of '80' for waiting time
waiting_time <- 80

# Calculate predicted discharge duration with regression equation
predicted_dd <- coefficients[1] + coefficients[2] * waiting_time
# View result
print(predicted_dd)
```
In English, this reads across like our formula above. In `R` speak, it reads: "take the value in position 1 in `coefficients` plus the value in position 2 in `coefficients` times the value stored in `waiting_time`. Put that in the box called `predicted_dd`.

And here's our resulting output:
```R
> # View result
> print(predicted_dd)
(Intercept) 
   3.871431 
```
Wouldn't you know it, there's our Y value (Intercept)! That's all we've done: we've given `R` the parameters and it has predicted the Y value we should expect in our equation under those circumstances. Pretty neat.

## Question 3:
This question has to do with **multiple regression.** Here's the prompt we're given:
> We will use a very famous dataset in R called mtcars. This dateset was extracted from the 1974 Motor Trend US magazine, > and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973--74 models). <br />
>
> This data frame contain 32 observations on 11 (numeric) variables. <br />
>
> [, 1]	mpg	Miles/(US) gallon <br />
> [, 2]	cyl	Number of cylinders <br />
> [, 3]	disp	Displacement (cu.in.) <br />
> [, 4]	hp	Gross horsepower <br />
> [, 5]	drat	Rear axle ratio <br />
> [, 6]	wt	Weight (1000 lbs) <br />
> [, 7]	qsec	1/4 mile time <br />
> [, 8]	vs	Engine (0 = V-shaped, 1 = straight) <br />
> [, 9]	am	Transmission (0 = automatic, 1 = manual) <br />
> [,10]	gear	Number of forward gears <br />

Ah yes, there's `mtcars` again. If you're familiar with `R` already, you know this guy. If you're not, then prepare yourself, because you're going to know this guy very well. `mtcars` is a built-in dataset in `R` intended for playing around with functions, which is precisely what we're about to do.

Calling `mtcars` is simple enough. But we've been instructed to use only 4 of the variables found in this data frame: `mpg`, `disp`, `hp`, `wt`. Here's what that looks like in R:
```R
# Get 4 variables in mtcars
input <- mtcars[,c("mpg","disp","hp","wt")]
# View result
print(head(input))
```
We've got it, and I've stored just our selection to a new data frame called `input`.

Now we can create a multiple regression model using our data. In this case, the instructions tell us to use `mpg` as the response variable and `disp`, `hp`, and `wt` as the predictor variables.

### Hold on, what?
We're using 3 predictor variables? Yep. It's still a linear regression, as you'll see we'll still be using `lm()`. But there are **multiple predictor variables**, thusly make it a **multiple linear regression.** The equation doesn't get too much different either. On the math side, instead of one slope, now we have several (one for each predictor.) As always, we'll be letting `R` handle everything:
```R
# Get 4 variables in mtcars
input <- mtcars[,c("mpg","disp","hp","wt")]
# View result
print(head(input))

# Create the multiple regression model
model <- lm(formula = mpg ~ disp + hp + wt, data = input)

# Print to view results
summary(model)
```
Still looking pretty familiar, right? Here's what `summary` returns:
```R
> # Print to view results
> summary(model)

Call:
lm(formula = mpg ~ disp + hp + wt, data = input)

Residuals:
   Min     1Q Median     3Q    Max 
-3.891 -1.640 -0.172  1.061  5.861 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept) 37.105505   2.110815  17.579  < 2e-16 ***
disp        -0.000937   0.010350  -0.091  0.92851    
hp          -0.031157   0.011436  -2.724  0.01097 *  
wt          -3.800891   1.066191  -3.565  0.00133 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 2.639 on 28 degrees of freedom
Multiple R-squared:  0.8268,	Adjusted R-squared:  0.8083 
F-statistic: 44.57 on 3 and 28 DF,  p-value: 8.65e-11
```
### With that, it's time to interpret the results.
First, let's look at setting up our equation so we can see where to plug in the values `R` gave us. The format for the equation is the same as our previous linear regressions, just with multiple predictor variables (X):

**ŷ = a + b1 * `disp` + b2 * `hp` + b3 * `wt`**

In English, our formula reads: some predicted value = the (Intercept) plus the first coefficient times `disp`, plus the second coefficient times `hp`, plus the third coefficient times `wt`.

You can know which coefficient or 'b' is which because they go together with their neighbor; in this problem, 'b1' is the coefficient that corresponds with `disp`, which `R` has output for us under "`Coefficients:`". Likewise, coefficient 'b2' goes with `hp`, and coefficient 'b3' goes with `wt`. There's no guesswork involved.

Here's what that looks like if we isolate it out from the rest using the `coefficients()` function:
```R
> # View just the coefficients
> coefficients <- coefficients(model)
> print(coefficients)
  (Intercept)          disp            hp            wt 
37.1055052690 -0.0009370091 -0.0311565508 -3.8008905826 
```
### When interpreting these results, what we want to know is how well `disp`, `hp`, and `wt` predict a given car's `mpg`. This is what we find:
- For `(Intercept)`: this value (about 37.106) is what we get when the other variable values all = 0. In the real world, no car is going to have 0 displacement, horsepower, or weight. But in the math world, it helps to set a baseline for calculating things.
- For `disp`: this tells us that for each unit of `disp`, `mpg` is expected to decrease by 0.000937 units. At the same time, `hp` and `wt` remain constant (unchanged.) However, the p-value (listed under the Pr(>|t|) column in our summary) is 0.92851, making it not statistically significant. In English, this means `disp` doesn't have a meaningful effect on `mpg` in our model.
- For `hp`: this means each for additional `hp` unit, `mpg` decreases by 0.031157 units. Again, this is while `disp` and `wt` are constant. The resulting p-value for `hp`, 0.01097, is statistically significant, so `hp` has a meaningful negative effect on `mpg`.
- For `wt`: this result means for each additional unit of `wt`, `mpg` decreases by about 3.80 units, which in combination with our p-value of 0.00133 tells us that `wt` has a strong, negative impact on `mpg`.





