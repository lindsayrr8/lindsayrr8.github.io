# Hypothesis Testing, Confidence Intervals, & Correlation Analysis with R

This week, we're biting into the meat of the statistics burger. We're still working with the statistical basics, but this time we'll be applying them with a few new formulas to do some basic analyses. The topics covered will be slightly more advanced, but as always, we'll be *letting R handle everything for us.*

## To begin, let's explore hypothesis testing.
Specifically, we'll be focusing on **p-values,**  **one-tailed hypothesis testing,** and **two-tailed hypothesis testing** first.

### To perform our first hypothesis test, we're given the following scenario:

> The director of manufacturing at a cookies company needs to determine whether a new machine is able to produce a particular type of cookies according to the manufacturer's specifications, which indicate that cookies should have a mean of 70 and standard deviation of 3.5 pounds. A sample of 49 cookies reveals a sample mean breaking strength of 69.1 pounds.

### To evaluate the data in this scenario, we are asked to address the following tasks: <br />
**A.** State the null and alternative hypothesis <br />
**B.** Is there evidence that the machine is not meeting the manufacturer's specifications for average strength? Use a 0.05 level of significance <br />
**C.** Compute the p value and interpret its meaning <br />
**D.** What would be your answer in (B) if the standard deviation were specified as 1.75 pounds? <br />
**E.** What would be your answer in (B) if the sample mean were 69 pounds and the standard deviation is 3.5 pounds? <br />

Phenomenal. So, what are the null and alternative hypotheses and what are they talking about?

## A.
The **null hypothesis** is our original, starting hypothesis or "idea." You can think of "null" sort of like nothing, because we haven't changed anything or presented anything new yet. The **alternative hypothesis** is what we're looking to test against our original hypothesis to see which is correct. Seems straightforward, right? <br />

In this case: <br />
- The null hypothesis (H0) is: the machine is producing cookies with an average weight equal to the manufacturer's specification *(the circumstances we started with)* <br />
- The alternative hypothesis (H1) is: the machine is not producing cookies according to the specification *(the circumstances we're going to test for)* <br /> 

So, to make that less wordy with the use of statistical symbols: <br />
H0: μ = 70 <br />
H1: μ ≠ 70 <br />

*Reminder: The greek letter μ ("mew") represents the population mean.* <br />

## B.
Is there **evidence** that the machine is **not** meeting the manufacturer's specifications for average strength? (Use a 0.05 level of significance.) <br />
This is it, folks. This requires conducting a hypothesis test. Technically, we will be performing a **Z-test,** which is used to check if there is a difference between a sample mean and a population mean when the population standard deviation is known. <br />

Let's use the formula:<br />
$z = (x̄ – μ0) / (σ/√n)$

<br> which reads in english as:<br />
<br >*"Z test value = (sample mean - population mean) / (population standard deviation / square root of sample size)"*<br />

<br> ...and keep track of the values we know for each variable: <br />
x̄ (sample mean) = 69.1 <br />
μ (population mean) = 70 <br />
σ (standard deviation) = 3.5 <br />
n (sample size) = 49 <br />
α (significance level) = 0.05 <br />

### *Optional tips*
*If you're anything like me, then explanations really help to understand and memorize all these random letters and variables:* <br />
- *A "Z-test" gets its name from a "Z-score," which is itself a measure of how many standard deviations a sample statistic is from the population mean. The "Z" comes from what is referred to as the Z-axis, which is the horizontal axis on the bottom of the bell curve (the standard normal distribution.)*
- *You could strategize to remember x-bar (x̄) by process of elimination when recalling the other basic statistical symbols. Or, you could really stretch your imagination and imagine x wearing a cool hat because he's very important as the sample mean!*
- *"Mew" (μ) kind of looks like a funky capital letter "M," which you might associate with the word "mean." Being a capital letter, you might think to remember it as the population mean, which is the larger pool of data/source size than the sample mean would be.*
- *I like to remember "sigma" (σ) as the symbol for standard deviation by imagining the little "o" circle spinning around and around forever. But suddenly, the little line up top... deviates! (Well, that, or "s" for both "sigma" and "standard deviation."*
- *The sample size, little "n," you might associate with the word "number," as in the "number of units in the sample."*
- *"Alpha (α) is a measure of a level of uncertainty. For example, if our α is 0.05, then we'd say there's about a 5% chance we accidentally reject a true null hypothesis. It's not exactly equivalent, but you might think to associate the letter "a" with "approximate uncertainty" for significance level.* <br />


<br > ...Magnificent. Moving on. Now we simply **translate** this information into **code that R can understand** so it can perform the calculation. <br />

```R
xbar <- 69.1
mu <- 70
sigma <- 3.5
n <- 49

# Using the formula for z test
z <- (xbar - mu) / (sigma / sqrt(n))
```
Notice we've made use of another one of R's handy built-in functions: `sqrt()`, which, as you can guess, is used to calculate the square root of a number. (Who'd've thunk it?)

When we run this code, the calculation gives us the z-value. From the z-value, we can calculate the p-value. We'll use that to decide if there's **evidence** that the machine is **not** meeting the manufacturer's specifications.

Output:
```R
> print(z)
[1] -1.8
```

## C.
Now we'll compute the p-value and interpret its meaning. <br />

We can use the p-value to determine whether or not we should reject the null hypothesis because when the p-value is less than the value of **α** (our significance level), then there is significant evidence to conclude that the original hypotheses was incorrect. In this case, if our p-value is less than 0.05, then we will reject the null. <br />

***Remember the golden rule: When the p is low, we reject H0!***

So what do we need to do to get our p-value? We'll have to decide what kind of "tail" test we'll be doing. On the bell curve, a **one-tailed test** only checks specifically for an increase or a decrease in one direction. A **two-tailed test** checks for a change in both directions.

According to our alternative hypothesis (H1), which question are we asking? We didn't state if we think the cookie machine might be producing more or less than specification, just *if* it's producing something other than the manufacturer specified average (in either direction.)

Therefore, we'll be conducting a two-tailed test using R to suit our alternative hypothesis.

The formula for this is: <br />
$p\text{ }value = 2 * P(|test statistic| > |critical value|)$
<br > *With "test statistic" being our Z-score and critical value being the significance level (α)* <br />

And we can convert this into R code just like before:
```R
pvalue <- 2 * pnorm(-abs(z))
print(pvalue)
```
Here, we've made use of two more handy built-in R functions: `pnorm()` and `abs()`. As you might have guessed, `abs()` is short for absolute value, and this is precisely what this function does. Our other function, `pnorm()`, helps to find the Z-score. It does this by giving the area to the left of the bell curve. Then, it multiplies that times 2, which covers values on both the left and right side because the bell curve is symmetrical. *(The details can get a little more complicated, but basically, doing it this way ensures the calculation is always correct.)*

When we print our `pvalue` to the console, the output we get is:
```R
> print(pvalue)
[1] 0.07186064
```
Is our p-value less than our significance level (α)? It might be easy enough to look at and determine (0.05 < 0.07), but we can also have R check this with a few simple lines of code:
```R
# Declares the significance level value
alpha <- 0.05
# Asks: is pvalue less than the significance level?
pvalue < alpha
```
And the output we get is:
```R
> pvalue < alpha
[1] FALSE
```
Therefore, it seems our p-value is ***not*** less than our significance level α. Since the "p isn't low," we will **fail to reject H0** (our original/starting hypothesis.)

*(Remember: this is science! In science, we never "accept" something as true. We just fail to reject it as false!)*

## D.
D is for devil's advocate. What would our answer for (B.) be if if the standard deviation were specified as 1.75 pounds of cookies instead?

For this example, we can keep all of our values the same except sigma σ (the standard deviation.) If we update the value for `sigma` in our previous code, we can just run the exact same block again:
```R
xbar <- 69.1
mu <- 70
# Updated the value for sigma
sigma <- 1.75
n <- 49
alpha <- 0.05

# Using the formula for z test
z <- (xbar - mu) / (sigma / sqrt(n))
print(z)

pvalue <- 2 * pnorm(-abs(z))
print(pvalue)

pvalue < alpha
```
And this is the output we get:
```R
> print(pvalue)
[1] 0.0003182172
> pvalue < alpha
[1] TRUE
```
Aha, it seems this time our p-value (0.00) is way **less** than our significance level α (0.05). R agrees that it's TRUE, so you know the rule. *"If the p is low..."*

## E.
E is also for dEvil's advocate. What would our answer for (B.) be if the sample mean were 69 pounds and the standard deviation is 3.5 pounds? Let's tweak some of our variables again:
```R
# Updated xbar
xbar <- 69
mu <- 70
# Updated sigma again
sigma <- 3.5
n <- 49
alpha <- 0.05

# Using the formula for z test
z <- (xbar - mu) / (sigma / sqrt(n))
print(z)

pvalue <- 2 * pnorm(-abs(z))
print(pvalue)

pvalue < alpha
```
Then, the output we get is:
```R
> print(pvalue)
[1] 0.04550026
> pvalue < alpha
[1] TRUE
```
It seems 0.1 lb can really make a difference. Now, given that our p-value (0.04) is lower than our significance level (0.05), we **reject** our original hypothesis (H0).

# Cool. Onto Confidence Intervals
#### Quick review - what is that?
If you've already taken an introductory statistics course, you've probably heard the phrase: **"We are 95% confident that** the value we're looking for falls within a range between 'x' and 'y'."

Here's the thing. There are a lot of moving parts in nature which make it difficult to create a perfect prediction. But our math has gotten precise enough that we can corner an area of the system where things are likely to occur.<br />
In other words, we may not be able to predict an exact outcome, but we can tell you to a relative degree of certainty what's most likely to happen. In statistics, that's a **confidence interval.**

To start pinning down confidence intervals, we're given the following problem:
> If x̅ = 85, σ = standard deviation = 8, and n=64, set up 95% confidence interval estimate of the population mean μ.

### Alright, let's begin by setting up the values we know in R:
*(Note, to avoid confusing R, either clear out your R environment and console or use different variable names than we did before.)*
```R
xbar <- 85
sigma <- 8
n <- 64
# Confidence level 95%, so alpha (uncertainty = 5%)
alpha <- 0.05
```

A 95% confidence level means that we're 5% uncertain. Of that 5% uncertainty, it's **split** between the two tail ends of the bell curve. Therefore, each tail contains 2.5% (half) of the distribution of uncertainty. Since we're interested in the area of the bell curve that pertains to our 95% certainty, we can find the z-values for the left and right sides of this middle area, which mark its boundaries.

So, because they're symmetrical, we just need to find one side - and then we've got them both.

Lucky for us, R has more great functions cooked in that we can use to plug-and-play to get our z-value(s). In this case, we'll be using `qnorm()`.

We need o **find the z-score,** which corresponds to the value at the **boundary** on the tips of the tails before we dip into each of our 2.5% uncertainty zones. To do this, we need to look at the whole picture of the bell curve and **ask R for the value** that lies at 97.5% on one of the sides. *(Yes, 97.5%. Don't let "95%" confuse you - that doesn't refer to a number in the distribution. It refers to how certain we are. We want the number at the boundary of certainty.)*

This is the formula to find the **critical z-score:** <br />
$ z = qnorm(1-α/2)$ <br />

We could write the formula out literally like this in R:
```R
# Getting the critical z-score
z_half_alpha <- qnorm(1 - alpha / 2)
```
Or, personally, I find that difficult for a human to read and overly complicated. So the following code is equivalent and will return the exact same value, still using the `qnorm()` function:
```R
# Getting the critical z-score
z_half_alpha <- qnorm(0.975)
```

<br> In both cases of our code, we've told R to find the value at 97.5%. We're also using the same formula either way. <br />

R returns this output:
```R
> print(z_half_alpha)
[1] 1.959964
```
Fantastic, we have our number for our z-score.
## Now what do we do with it?
We're not done yet. We have our z-score. We need our shiny, finished confidence interval. There's a few more steps to get to that:

1) Calculate the **standard error**
2) Calculate the **margin of error**
3) Calculate the **confidence interval**
 
**1)** Starting with the standard error (the standard deviation of a sample population): <br />
We will plug the formula into R: <br />
SE = (σ / √n) <br />
In R, with our output:
```R
# Calculate the standard error
standard_error <- sigma / sqrt(n)
print(standard_error)
### Output:
> print(standard_error)
[1] 1
```
So our standard error is 1. Excellent. Onto next:

**2)** Again, take the simplified formula for margin of error (MOE), (the amount of random samping error): <br />
ME = `z_half_alpha` * `standard_error`
```R
# Calculate margin of error
margin_of_error <- z_half_alpha * standard_error
print(margin_of_error)
### Output:
> print(margin_of_error)
[1] 1.959964
```

### And at last, it's confidence interval time:
**3)** To recap, the confidence interval is the range within which you expect the actual population mean (μ) to fall. <br />
It's determined by subtracting and adding the margin of error to the sample mean, which represents both sides of the bell curve (positive and negative):
```R
# Calculate confidence interval
lower_bound <- xbar - margin_of_error
upper_bound <- xbar + margin_of_error
confidence_interval <- c(lower_bound, upper_bound)
print(confidence_interval)
### Output:
> print(confidence_interval)
[1] 83.04004 86.95996
```

Cool! We have our confidence interval values. Thanks, R! **Our confidence interval is ~(83.04, 86.96).**

# Now it's time for: Correlation Analysis
Wow, you made it this far (I'm sorry.) Brace yourself - it's time to start **plotting.** (No, I promise it really isn't that bad.)

We're given the following **data sets** and **prompt** to start out with our first correlation analysis: <br />

*Data Sets:*
> girls_goals <- c(4, 5, 6) <br />
girls_time_spend <- c(19, 22, 28) <br />
boys_goals <- c(4, 5, 6) <br />
boys_time_spend <- c(18.9, 22.2, 27.8) <br />

*Prompt:*
> The accompanying data are: x= girls and y =boys. (goals, time spend on assignment)  
a. Calculate the correlation coefficient for this data set _____ <br />
b. Pearson correlation coefficient _____ <br />
c. Create plot of the correlation <br />

## Here are the steps we can take to achieve this: <br />
1) Input the data into vectors
2) Create a data frame
3) Calculate the correlation coefficients
4) Plot the correlation

First, let's add the data to R:
```R
# Data sets
# x = girls
girls_goals <- c(4, 5, 6)
girls_time_spend <- c(19, 22, 28)
# y = boys
boys_goals <- c(4, 5, 6)
boys_time_spend <- c(18.9, 22.2, 27.8)
```

Next, let's cook these up as a data frame. This is simple enough; you just specify to R that you want to create a data frame by using `data.frame` as the data type specifier:
```R
# Combining the data into a data frame
df <- data.frame(
  girls_goals = girls_goals,
  girls_time_spend = girls_time_spend,
  boys_goals = boys_goals,
  boys_time_spend = boys_time_spend
)
```
Notice: We've started using `=` more now that we're working inside functions more often. Remember that in R, the `<-` arrow is typically used for variable assignment by convention, while `=` is typically used in the context of function arguments.

Now it's time to calculate our **correlation coefficients.**
## But what are correlation coefficients?
Essentially, a correlation coefficient is a value that represents how closely two variables correlate. In other words, it is a statistical measure that describes the type of **relationship between two variables.**

The **value** of a correlation coefficient ranges from -1 to 1.
- 1 means there is a perfect positive relationship (as one variable increases, so does the other)
- -1 means there is a perfect negative relationship (as one variable increases, the other decreases)
- 0 means there's no relationship at all between the variables

The **Pearson Correlation Coefficient** measures the **linear** relationship between two continuous variables.
It also ranges from -1 to 1. The meanings are also the same. <br />
*Remember: "continuous" means the variable can be an infinite number of values within a given range, such as time, temperature, etc.*

## Nice. How do we do this in R?
There's yet another pre-baked function for this task: `cor()`:
```R
# Calculating correlation coefficients
correlation_girls <- cor(girls_goals, girls_time_spend)
correlation_boys <- cor(boys_goals, boys_time_spend)
```
As for the Pearson Correlation Coefficients: R actually uses this method by default. But, we can also **explicitly specify which method** we want to use in the function arguments:
```R
# Specifying Pearson Correlation Coefficients
pearson_girls <- cor(girls_goals, girls_time_spend, method = "pearson")
pearson_boys <- cor(boys_goals, boys_time_spend, method = "pearson")
```

## Awesome - it's plotting time.
As you might expect, `plot()` is another very useful R function we will be employing for this task. The `plot()` function takes several **arguments** (some of which are optional):
```R
# plot() basic format: plot(x, y, ...)

### plot() function essential arguments:
# x = data for the x/horizontal axis
# y = data for the y/vertical axis

### plot() function optional arguments:
# main = title
# xlab = x-axis label
# ylab = y-axis label
# pch = shape of points on the plot; (pch 19 makes solid circles)
# col = sets color of points on the plot
# and more...
```

And we can (make R) get to work plugging in our data with `plot()` and a few optional arguments for clarity. (This was pretty painful to display properly at first, admittedly):
```R
# Data sets
# x = girls
girls_goals <- c(4, 5, 6)
girls_time_spend <- c(19, 22, 28)
# y = boys
boys_goals <- c(4, 5, 6)
boys_time_spend <- c(18.9, 22.2, 27.8)

# Create a scatter plot with girls' time on the x-axis and boys' time on the y-axis
plot(girls_time_spend, boys_time_spend,
     main = "Time Spent vs Goals: Girls vs Boys",
     xlab = "Girls' Time Spent (minutes) / Goals",
     ylab = "Boys' Time Spent (minutes) / Goals",
     pch = 19,
     col = "pink",
     xlim = range(c(girls_time_spend, girls_goals)),
     ylim = range(c(boys_time_spend, boys_goals)))

# Add boys' goals vs girls' goals to the same plot in blue with round points
points(girls_goals, boys_goals, pch = 19, col = "blue")
```
As you can see, I also had to use R's `points()` function, which is used to add points to an existing plot. That's how I got it all together as one, given the specifications. *Thank you internet for your help!*
![Image of girls and boys times, goals scatterplot]([URL_to_your_image](https://github.com/lindsayrr8/lindsayrr8.github.io/blob/main/_posts/Module_5_girls_boys_scatterplot.png?raw=true))
*Disclaimer: I am definitely not a front-end dev.*
