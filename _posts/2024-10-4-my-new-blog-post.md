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

Then, using R's `mean()` function, we get our first statistic measure from the data:
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

Naturally, there are some rules about this that govern ensuring you're getting accurate numbers. But for the purposes of this exercise, we'll just be calculating a simple, small sample statistic using R's `set.seed()` and `sample()` functions:
```R

```
