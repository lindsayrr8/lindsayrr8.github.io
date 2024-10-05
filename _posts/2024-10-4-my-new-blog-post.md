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
Then, using R's `mean()` function, we get our first statistic measure from the data:
```R
# Compute the mean of this population
mean_population <- mean(population)
print(mean_population)
```


