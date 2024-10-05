# Simple Exercises with Variance and Standard Deviation Using R

## Question A.
To run a few simple statistics using R's selection of built in functions, we're presented with the following scenario:
> Consider a population consisting of the following values which represent the number of ice cream purchases during the academic year for each of five housemates:
8, 14, 16, 10, 11

### Using this information, we're asked to perform the following tasks with R: <br />
**a.** Compute the mean of this population. <br />
**b.** Select a random sample of size 2 out of the five members. <br />
**c.** Compute the mean and standard deviation of your sample. <br />
**d.** Compare the Mean and Standard deviation of your sample to the entire population of this set (8, 14, 16, 10, 11). <br />

To begin, we can take our dataset and plug the values into a vector:
```R
# Number of ice cream purchases in an academic year
# per each of five housemates
population <- c(8, 14, 16, 10, 11)
```
Our total population in this case is the five housemates, since that defines the boundaries of our group of interest. <br />

Then, using R's `mean()` function, we'll get our first statistical measure from the data:
```R
# Compute the mean of this population
mean_population <- mean(population)
print(mean_population)
```
Calling the population mean prints our results to the console:
```R
> print(mean_population)
[1] 11.8
```
### Now, it's sampling time!
In this case, we have a relatively small number of individuals in our population (5 people.) But most of the time in data science we'll be working with much bigger numbers. (For example, a population of 22.24 million people living in the state of Florida.)

As you might already know, this is where sampling becomes especially useful. Even if we could get ahold of every single person living in Florida for a survey (which is very unlikely,) it probably wouldn't be smart resource-wise to invest the time and money in doing so. Therefore, the idea behind sampling is that given a certain amount of sample data, **a sample group from the overall population will have similar characteristics as the rest of it.**

Naturally, there are some rules about this that govern ensuring you're getting accurate numbers. But for the purposes of this exercise, we'll just be calculating a simple, small sample statistic of the 5 housemates using R's `set.seed()` and `sample()` functions:
```R
# Select a random sample of size 2 from the population
set.seed(123)
sample_size <- 2
sample <- sample(population, sample_size)
print(sample)
```
What's happening here breaks down into a few basic steps. First, the `set.seed()` function will help R decide how to generate the numbers in order to **make the outcome reproducible.** This is because of the way computers handle generating "random" numbers. The concept can get complicated, but more or less, `set.seed()` is a function you'd want to use for running simulations under controlled conditions in order to make your results reproducible. But it's not necessarily a function you'd use when working with real-world data.

*(Note: even the "123" plugged into the function is arbitrary. It's just a common value used with `set.seed()`. But random number generation is a big concept to talk about - so big that it would derail the rest of our simple exercise. So we're moving on:)*

With `sample_size`, we just designate a little box in R's memory for our sample size to sit in. Then, `sample <- sample(population, sample_size)` tells R to **grab a sample from our population** using the number we stored in `sample_size`. Storing the value this way is optional. You could just in plug a "2" instead if you really wanted to.

Printing the result we get from R's calculation gives us this output:
```R
> print(sample)
[1] 16 14
```
Note that if we run this block of code multiple times, it always gives us this same output. That's the purpose of using `set.seed()`.

Now that we have our sample information, we can start doing calculations with it. We'll use R's `mean()` and `sd()` functions to get the mean and standard deviation for the sample:
```R
# Compute the mean and standard deviation of the sample
mean_sample <- mean(sample)
sd_sample <- sd(sample)
print(mean_sample)
print(sd_sample)
```
And here is what our ouput shows:
```R
> print(mean_sample)
[1] 15
> print(sd_sample)
[1] 1.414214
```

### Sweet. We have our sample statistics. Now it's time to compare them to the population:
```R
# Compare the mean and standard deviation of the sample to the population
sd_population <- sd(population)
print(mean_population)
print(mean_sample)

print(sd_population)
print(sd_sample)
```
Really quickly, we assigned the value R gets for the population standard deviation to a variable. Then, we compared the mean and standard deviations between the sample and population. Here's the output we get:
```R
> print(mean_population)
[1] 11.8
> print(mean_sample)
[1] 15
> print(sd_population)
[1] 3.193744
> print(sd_sample)
[1] 1.414214
```

### So, interpreting these results:
- The sample mean (15) is higher than the population mean (11.8).
- The sample standard deviation (1.41) is lower than the population standard deviation (3.19).

These results are expected because the sample data R selected have **variance** from the rest of the individuals in the dataset. In fact, R happened to sample the 2 largest values from the set. This illustrates the concept of **sampling variability**, meaning that little differences between individuals amount to differences in sample data compared to the overall population. In fact, if we hadn't used `set.seed()`, we would have gotten largely different results if we ran the code many times. This will eventually lead us to concepts like **sampling distribution** and the **Central Limit Theoreom (CLT)** to meaningfully evaluate differing sample outcomes. *(We will talk more about those soon!)*

Today, our sample outcome was also affected by our small sample size. This is due to the **Law of Large Numbers**, which essentially says the more data you get, the more accurate it is. In this case, because we have a small sample, we should be careful about making inferences or coming to conclusions about the overall population based on our sample data alone.


# Bodacious. It's time to move on to a quick mathematical concept about Sample Proportions.
## Question B.
To help demonstrate the concept, we're given the following questions:
> Suppose that the sample size n = 100 and the population proportion p = 0.95. <br />
> 
> 1. Does the sample proportion p have approximately a normal distribution? Explain. <br />
> 2. What is the smallest value of n for which the sampling distribution of p is approximately normal? 

Ok. To start, data check on what we know:
- The sample size (n) is 100
- The population proportion (p) is 0.95 <br />

A population proportion of 0.95 **means that 95% of the population is considered a "success"** for whatever the question is that we're asking about the population. The question itself doesn't even matter here, because the math rules are the same no matter what we ask in this case.

What we want to know is if the sample proportion, called "p-hat" and abbreviated with "p̂" *(yes, that name tickles me)* behaves like a normal distribution. Recall that **a normal distribution is one that is roughly bell-shaped,** aka, symmetric about the mean.

### So, what's the rule for "normal?"
With humans, it's hard to say. With statistics, thankfully, there are some simple checks: <br />
*The sample proportion is normal if:* <br />
n * p ≥ 5 (enough successes) <br />
n * q ≥ 5 (enough failures) <br />
*where:* <br />
q = 1 - p = 0.05 (this means 5% of the population is a "failure) <br />

In English, this means in order to have enough successes/failures in our sample, the number of successes/failures needs to be at least 5.

### Lovely. We can use these formulas to evaluate the scenario we were given: <br />
Condition for successes: <br />
 n * p = 100. So, 100 * 0.95 = 95 <br />
(number in sample (n = 100) times the number of the population proportion (p = 0.95) == 5 or more than 5? Yes, 95 > 5. <br />

Condition for failures: <br />
n * q = 100 * 0.05 = 5 <br />
(number for proportion of failures (q) is calculated: q = 1 - p = 1 - 0.95 = 0.05) <br />
n * q = 100 * 0.05 = 5
(number in sample (n = 100) times number for proportion of failures (q = 0.05) == 5 or more than 5? Yes, 5 = 5.)

So, if our success condition = `TRUE` and our failure condition = `TRUE`, then we have met both conditions to qualify as "normal."

