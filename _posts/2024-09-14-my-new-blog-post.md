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

Right, then. This week, we're given our data set:

Set#1:  10, 2, 3, 2, 4, 2, 5<br>
Set#2:  20, 12, 13, 12, 14, 12, 15<br>

Our task is to compute the mean, median, and mode of these sets. Then we wil get to computing the range, interquartile, variance, and the standard deviation of the data sets. (We will talk more about those next.)

In my humble opinion, a great place to start would be to *let R handle everything.* We can begin by turning our lovely data sets into vectors that R can understand and work with:

`set_1 <- c(10, 2, 3, 2, 4, 2, 5)`<br>
`set_2 <- c(20, 12, 13, 12, 14, 12, 15)`<br>
