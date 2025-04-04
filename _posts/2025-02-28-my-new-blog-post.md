# Visualizations for Distribution Analysis: Where Do We Start?

So you have yourself a dataset and someone has tasked you with analyzing it for insights. Then, you're to create visualizations for the insights you collect to spare others the crunch time and the paperwork. Where do you begin?

Sometimes just viewing the structure or the first few rows of the dataset can give you an idea of what you're working with, but it is often quite insufficient for revealing trends in your data. This is where you'd **start running some statistical tests** - but in order to do so, you still need more information about the distribution of the data you're working with.

In other words,  **the distribution of your data significantly affects the type of statistical test you should use on it.**

## So, how do we approach figuring out the distribution of a dataset?

To give a simple demonstration, we're turning back to `R` and its built-in `mtcars` dataset. To do this, we will also be using the `ggplot2` `R` package.

*(As with most of my blog posts about visualization, this article will focus more on theory and technique than coding explanations. I have a bunch of those already available under my statistical analysis and `R` posts.)*

You will also be delighted to know that, yes, **data visualizations are the fastest and easiest way to figure out distribution.**

Often times when working with data visualizations, the process is not straightforward. You will likely have to experiment with multiple different kinds of visualizations until you land on one that is simplest and makes the most sense. That being said, **a very flexible place to start looking for distribution is with a histogram:**

```R
install.packages("ggplot2")  
library(ggplot2)

data(mtcars)

# Initial check of dataset
str(mtcars)
summary(mtcars)

# Create a histogram using the mtcars dataset
ggplot(mtcars, aes(x = mpg)) + 
  geom_histogram(binwidth = 2, fill = "deepskyblue2", color = "black") + 
  ggtitle("Distribution of MPG")
```

And here is the result:

![module-7-blog-histogram-example-2](https://github.com/user-attachments/assets/e03ecf96-c080-4a5c-8fa3-c6ff16d21de8)


Cool. Just taking a quick look at the chart reveals a lot of the cars in the set are clustered around the stats of 15-22ish mpg. *(These are older cars, after all.)*

The reason a histogram is a good way to check out your dataset's distribution is because **histograms can show multiple different characteristics,** including:
- shape/skew
- spread/dispersion
- outliers
- gaps or clusters

However, as you've surely noticed, not all data visualizations are created equal. Each has their own strengths and weaknesses such that it is often to your benefit to **generate multiple different kinds of visualizations to determine distribution.** The more information and accuracy for you, the better! *(Especially if it only takes you a few lines of code.)*

Histograms are great (I love them, actually.) But as with all visualizations, they have their downsides. For one thing, with histograms you're not seeing specific data points. It's also not always clear what is an outlier in the data. This could potentially become misleading.

Instead, let us approach the distribution for this dataset from another angle by **creating a box and whisker plot** *(that name just tickles me):*

```R
# Create box plot to show comparison
ggplot(mtcars, aes(x = factor(cyl), y = mpg)) + 
  geom_boxplot(fill = "deepskyblue2") + 
  ggtitle("MPG Distribution by Cylinder Count")
```

And here is the result:

![module-7-box-and-whisker-plot-example-1](https://github.com/user-attachments/assets/b72a40b1-4fa8-4954-a6e3-a81283d0c3c3)

Nice. Looking at the chart reveals the median mpg is about 26 for the most represented category of cars in the dataset (being those that are 4-cylinder and ~22 to 30 mpg), with the visual addition of a few weird little 8-cylinder outliers on the other end.

**A box and whisker plot is a good way to check the details of a distribution rather than its overall shape.** It's also pretty good at showing you the statistical "5-number summary" of the dataset, highlighting differences across categories. To give examples, from this visualization we can tell:
- the median/percentiles
- any outliers
- skewness and spread
- categorial information

## Can you see the difference?

Here's one primary observation for you. On the histogram, there's a huge bar that seems to imply lots of cars in the dataset get about 15 or fewer mpg. When we look at the box and whisker plot, we can see that in reality, very few cars truly get 15 or fewer mpg (even less so if we were to omit the outliers.) While the numbers on the graph are accurate, it is a bit visually confusing.

In fact, there are more cars between ~23-35 mpg in the set than there are <=15 mpg. But because those are represented by tiny bars and the cars <=15 mpg are represented by a big bar (and a stubby one), it looks to be more prominent in the dataset. Therein lies the mischief on the histogram, but that wasn't evident at first glance, was it?

If we run some code to check the numbers, we can even see that cars with 15 or fewer mpg only represent about ~19% of the total dataset while cars with 23 or more mpg represent ~22%:

```R
# Count cars with mpg <= 15
low_mpg_cars <- sum(mtcars$mpg <= 15)
# Total number of cars in dataset
total_cars <- nrow(mtcars)
# Calculate percentage
percentage_15 <- (low_mpg_cars / total_cars) * 100

# Count cars with mpg >= 23
high_mpg_cars <- sum(mtcars$mpg >= 23)
# Total number of cars in dataset
total_cars <- nrow(mtcars)
# Calculate percentage
percentage_23 <- (high_mpg_cars / total_cars) * 100

# Print results
cat("Number of cars with 15 or fewer mpg:", low_mpg_cars, "\n")
cat("Percentage <= 15 represented out of total cars:", round(percentage_15, 2), "%\n")

cat("Number of cars with 23 or more mpg:", high_mpg_cars, "\n")
cat("Percentage >=23 represented out of total cars:", round(percentage_23, 2), "%\n")

```
*Outputs:*

```R
> # Print results
> cat("Number of cars with 15 or fewer mpg:", low_mpg_cars, "\n")
Number of cars with 15 or fewer mpg: 6 
> cat("Percentage <= 15 represented out of total cars:", round(percentage_15, 2), "%\n")
Percentage <= 15 represented out of total cars: 18.75 %
> 
> cat("Number of cars with 23 or more mpg:", high_mpg_cars, "\n")
Number of cars with 23 or more mpg: 7 
> cat("Percentage >=23 represented out of total cars:", round(percentage_23, 2), "%\n")
Percentage >=23 represented out of total cars: 21.88 %
```

It sure doesn't look like that on the graph.

## So when do you use either one of these guys?

While this isn't an exhaustive list of distribution visualizations, there are some cases you can generally apply each of these to. A histogram is still probably the best way to see the overall shape of the distribution, while the box plot is proficient at showing details like spread and outliers. For best practice - use them both together!

## What would Few do?

Few, as in visualization expert Stephen Few of *"Now you see it: An Introduction to Visual Data Sensemaking,"* might appreciate the simplicity of these visualizations. He would likely also appreciate the use of grids to improve readability by contextualizing units of space on these graphs. But he might well also give the histogram a slap of disapproval due to some scaling issues. In particular, our histogram has some pesky problems with visually misrepresenting the data involving our <=15 mpg cars and >=23 mpg cars despite the numbers being accurate.

Few's argument is that good visualizations should make data clearer rather than being misleading. If the box and whisker plot can do that better than the histogram in this case, then Few wouldn't tell you to use the histogram. *(Really, he'd tell you to check your bin widths!)*
