# Simple Exercises with Variance and Standard Deviation with R

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

With `sample_size`, we just designate a little box in R's memory for our sample size to sit in. Then, `sample` tells R to **grab a sample from our population** using the number we stored in `sample_size`. Storing the value this way is optional. You could just in plug a "2" instead if you really wanted to.

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

