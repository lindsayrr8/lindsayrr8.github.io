# Hypothesis Testing & Correlation Analysis with R

This week, we're biting into the meat of the statistics burger. We're still working with the statistical basics, but this time we'll be applying them with a few new formulas to do some simple analyses. As always, we'll be *letting R handle everything for us.*

To begin, let's explore **hypothesis testing.** Specifically, we'll be focusing on **p-values** and **one-tailed hypothesis testing** first.

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
- *I like to remember "sigma" (σ) as the symbol for standard deviation by imagining the little "o" circle spinning around and around forever. But suddenly, the little line up top... deviates!*
- *The sample size, little "n," you might associate with the word "number," as in the "number of units in the sample."*
- *"Alpha

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
Now we'll compute the p-value and interpret its meaning.
**Remember the golden rule: When the p is low, we reject H0!**

