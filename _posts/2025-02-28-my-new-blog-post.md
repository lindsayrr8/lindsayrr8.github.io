# Distribution Analysis Visualizations: Where Do We Start?

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
ggplot(mtcars, aes(x=mpg)) + 
  geom_histogram(binwidth=2, fill="deepskyblue2", color="black") + 
  ggtitle("Distribution of MPG (Miles Per Gallon)")
```

And here is the result:

![module-7-blog-histogram-example-1](https://github.com/user-attachments/assets/9bec478c-6fdb-4d31-8c67-4a62df8b46d8)

Cool. Just taking a quick look at the chart reveals a lot of the cars in the set are clustered around the stats of 15-22ish mpg. *(These are older cars, after all.)*

The reason a histogram is a good way to check out your dataset's distribution is because **histograms can show multiple different characteristics,** including:
- shape/skew
- spread/dispersion
- outliers
- gaps or clusters

However, as you've surely noticed, not all data visualizations are created equal. Each has their own strengths and weaknesses such that it is often to your benefit to **generate multiple different kinds of visualizations to determine distribution.** The more information and accuracy for you, the better! *(Especially if it only takes you a few lines of code.)*

Histograms are great (I love them, actually.) But as with all visualizations, they have their downsides. For one thing, with histograms you're not seeing specific data points. It's also not always clear what is an outlier in the data. This could potentially become misleading.

Instead, let us approach the distribution for this dataset from another angle: by **creating a box and whisker plot** *(that name just tickles me.)*



