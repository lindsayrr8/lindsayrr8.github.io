# Hypothesis Testing & Correlation Analysis with R

This week, we're biting into the meat of the statistics burger. We're still working with the statistical basics, but this time we'll be applying them with a few new formulas to do some simple analyses. As always, we'll be *letting R handle everything for us.*

To begin, let's explore **hypothesis testing.** Specifically, we'll be focusing on **p-values,**  **one-tailed hypothesis testing,** and **two-tailed hypothesis testing** first.

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
We've made it, folks. This requires conducting a hypothesis test. Technically, we will be performing a **Z-test,** which is used to check if there is a difference between a sample mean and a population mean when the population standard deviation is known. <br />

Let's use the formula: <br />
$z = (x – μ0) / (σ/√n)$
<br> ...and keep track of the values we know for each variable: <br />
x̄ (sample mean) = 69.1 <br />
μ (population mean) = 70 <br />
σ (standard deviation) = 3.5 <br />
n (sample size) = 49 <br />
α (significance level) = 0.05 <br />

*Optional tips - If you're anything like me, then explanations really help to understand and memorize all these random letters and variables:*
- *A "Z-test" gets its name from a "Z-score," which is itself a measure of how many standard deviations a sample statistic is from the population mean. The "Z" comes from what is referred to as the Z-axis, which is the horizontal axis on the bottom of the bell curve (the standard normal distribution.)*
- *You could strategize to remember x-bar (x̄) by process of elimination when recalling the other basic statistical symbols. Or, you could really stretch your imagination and imagine x wearing a cool hat because he's very important as the sample mean!*
- *"Mew" (μ) kind of looks like a funky capital letter "M," which you might associate with the word "mean." Being a capital letter, you might think to remember it as the population mean, which is the larger pool of data/source size than the sample mean would be.*
- *I like to remember "sigma" (σ) as the symbol for standard deviation by imagining the little "o" circle spinning around and around forever. But suddenly, the little line up top... deviates! (Well, that, or "s" for both "sigma" and "standard deviation."*
- *The sample size, little "n," you might associate with the word "number," as in the "number of units in the sample."*
- *"Alpha (α) is a measure of a level of uncertainty. For example, if our α is 0.05, then we'd say there's about a 5% chance we accidentally reject a true null hypothesis. It's not exactly equivalent, but you might think to associate the letter "a" with "approximate uncertainty" for significance level.*

...Magnificent. Now we simply translate this information into code that R can understand so it can perform the calculation.

```R
xbar <- 69.1
mu <- 70
sigma <- 3.5
n <- 49

# Using the formula for z test
z <- (xbar - mu) / (sigma / sqrt(n))
```
Notice we've made use of another one of R's handy built-in functions: sqrt(), which, as you can guess, is used to calculate the square root of a number. (Who'd've thunk it?)

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
Here, we've made use of two more handy built-in R functions: `pnorm()` and `abs()`. As you might have guessed, `abs()` is short for absolute value, and this is precisely what this function does. Our other function, `pnorm()`, calculates the area to the left of a Z-score (aka, the cumulative distribution function of a normal distribution.)

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
### Quick review - what is that?
