# The Statistical Basics in R: Mean, Median, and Mode

One thing that has always sat well with me about statistics is how simple and easy the very basic measures are. We all remember our old friends from grade school: mean, median, and mode. If you're like me, you can also remember trying to come up with a system to remember which one was which when test time came.

***Okay,***

- **Mean** - the *meanest* one with the most steps. You add up all the values then divide the total by the number of values...
- **Median** - the middle, like the median that divides the road,
- **& Mode** - which sounds like *"most..."* for the value that occurs most often...

...Many years of crying in algebra classes later, I'm delighted to personally thank Occam's Razor that R makes these basic statistical functions even simpler and easier. *(Well, sort of. Mostly. You'll see)*

### R comes pre-packaged with the following functions:
`mean()`, `median()`, and `mo--` *cough.* Um, actually. Sit down, we'll need to talk about that one later.

Moving on! Cool, cool. But what do any of these functions tell us? Why do they exist and why do we use them in statistics?

Thankfully, as with everything I love about computers, **mean, median, and mode are ways to take a complicated task and make it much, much simpler.**

All three of these functions are what are called **Measures of Central Tendency.** In essence, they cut down a lot of work on an (often large) data set and present a generalized summary the values found within it. It's called *"central"* because it quite literally has a spatial relationship that falls in the *"middle"* or most significant part of your data set. This is all part of what's called **descriptive statistics**, because in doing all this we're aiming to *describe* features of things we're getting data on.

### Right, then. This week, we're given our data set:

<u>Set#1:</u>  10, 2, 3, 2, 4, 2, 5<br>
<u>Set#2:</u>  20, 12, 13, 12, 14, 12, 15<br>

Our task is to **compute the mean, median, and mode of these sets.** Then we wil get to computing the **range, interquartile, variance, and the standard deviation** of the data sets. (We will talk more about those next.)

In my humble opinion, a great place to start would be to *let R handle everything.* We can begin by turning our lovely data sets into vectors that R can understand and work with:

```R
set_1 <- c(10, 2, 3, 2, 4, 2, 5)
set_2 <- c(20, 12, 13, 12, 14, 12, 15)
```
Fabulous. Now we just plug the vectors into R's built in `mean()` and `median()` functions:

```R
# Computing the means
mean(set_one)
median(set_two)

# Computing the medians
median(set_one)
median(set_two)
```
And here's our output when we run it:
```R
> mean(set_one)
[1] 4
> mean(set_two)
[1] 14
> median(set_one)
[1] 3
> median(set_two)
[1] 13
```

### Hold on, where is the mode()?

Okay. Bear with me. Yes, R does have a function called `mode()`. No, **it does not return the statistical mode.**
In R, `mode()` returns the "mode" in the sense of *type* of data in an object. This is the output we get if we try to use the function on our data sets:

```R
> mode(set_one)
[1] "numeric"
> mode(set_two)
[1] "numeric"
```

Um, why did they make that choice, you say? Even `Python` has a built in statistical mode function, you say?
Well, apparently you don't end up using the statistical mode very often later in the game. Yes, it can be useful for qualitative data. No, I don't know why they made the choice to reserve the word "mode" in a statistical programming language for something other than the statistical mode. Maybe Google it and good luck?

Anyway, recovering from that headache, we still need our statistical mode. It will be up to us to **create a custom function** in order to do that.

For sanity's sake, I'll call our new function `get_mode()`. This part was a little tricky at first. There are a lot of good tutorials online to help us accomplish this correctly (and I certainly used them.)
```R
# Creating a custom mode function
get_mode <- function(x) {
  freq_table <- table(x)
  max_freq <- max(freq_table)
 mode_values <- as.numeric(names(freq_table[freq_table == max_freq]))
  return(mode_values)
}
```
### Now, let's break down what's happening here.

Of course, we first assign a name to our function. With `function(x)`, we specify that the new thing we're creating will be a function that takes in a vector of values:
`get_mode <- function(x) {`

Then, the line `freq_table <- table(x)` will help R discover how many duplicates there are. Basically, R lays out all the values on a little table and makes a space to stick their corresponding counts with them (meaning how many times each unique value appears.)

Now it's mode time, folks! The line `max_freq <- max(freq_table)` uses R's `max()` function to figure out how many times the most frequent value appears in our little frequency table.

Finally, on our `mode_values <- as.numeric(names(freq_table[freq_table == max_freq]))` line, R is comparing the frequencies found in `freq_table` to `max_freq` and making sure it's correct.
Then, the `names()` function pulls out whatever is stored in the spot where R determines the highest frequency value is. Importantly, it does this by pulling out what's there as a character/string by default. Therefore, we need to make sure our data stays as a "numeric" type so we can continue doing calculations on it. This is what the `as.numeric()` function is doing.

Of course, as always, we return our result as a last step. Here's what we get when it's all put together:

```R
# Creating a custom mode function
get_mode <- function(x) {
  # Creates frequency table for the values
  freq_table <- table(x)
  # Finds the max frequency value from the table
  max_freq <- max(freq_table)
  # Pulls out that value and keeps it numeric
  mode_values <- as.numeric(names(freq_table[freq_table == max_freq]))
  return(mode_values)
}
```

Now we can call `get_mode()` to get the statistical mode for both of our data sets from above. It's about time.
```R
get_mode(set_one)
get_mode(set_two)
```
And our output looks like:
```R
get_mode(set_one)
> [1] 2
get_mode(set_two)
> [1] 12
```

All that work for the simplest measure of central tendency. At least R did it for us!

But we're not done yet.

Let's put all of our code together so far and then we can move on to the next few tasks:
```R

set_one <- c(10, 2, 3, 2, 4, 2, 5)
set_two <- c(20, 12, 13, 12, 14, 12, 15)

# Creating a custom mode function
get_mode <- function(x) {
  # Creates frequency table for the values
  freq_table <- table(x)
  # Finds the max frequency value from the table
  max_freq <- max(freq_table)
  # Pulls out that value and keeps it numeric
  mode_values <- as.numeric(names(freq_table[freq_table == max_freq]))
  return(mode_values)
}

# Getting the means
mean(set_one)
mean(set_two)

# Getting the medians
median(set_one)
median(set_two)

# Getting the modes
get_mode(set_one)
get_mode(set_two)

```
Okay, we have our mean, median, and mode.
## Now it's range, interquartile, variance, and standard deviation time!
