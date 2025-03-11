# Visualizing Correlation Analysis with ggplot2

I've talked about correlation analysis on this blog before. Today, we are going to **visualize it.**

As usual, since I've already covered correlation analysis and plenty of `ggplot2`, I will be focusing more on the visualization and theory aspects of this activity.

Creating a visualization to **explore correlation** between different variables is a quick and easy approach to spotting trends and patterns in data. There are several ways we can go about doing this, and I will be showcasing two of these.

## To begin, I'll create a basic scatter plot and add a line of best fit:

You know the deal with these, right? A scatter plot of data points will show us any clusters or directional trends, and a line of best fit will summarize that pattern.

To demonstrate, I'll be using `R`'s built in `mtcars` dataset *(yes, there she is again, it's mtcars.)* We'll be comparing a car's weight to its average MPG for the total number of cars in the dataset.

This can be achieved both using base `R` and the `ggplot2` package.

### Can you spot the difference?

The scatter plot using base `R`'s `plot()` function:

![mod-8-base-scatter-plot](https://github.com/user-attachments/assets/3a60bf15-2256-4352-a052-7977eede992e)

The scatter plot using `ggplot2`:

![mod-8-ggplot2-scatter-plot](https://github.com/user-attachments/assets/647154ca-d006-4330-8151-3248e7a1d0eb)


### These look really similar. So what?

Well spotted, but sometimes **little differences can have a big result.** Most notably, the `ggplot2` image is set on a grid while the base `R`'s plot is not. Look at each of the plots again. Do you find it slightly faster and easier to read the second plot? This is because the gridlines help to guide your eye, which adds context that helps to interpret the image quickly.

Pretty straightforward, yes? Few *(as in Visualization expert Stephen Few)* thinks so, too. Above all, (and you will hear this often,) an effective visualization is one that can be **clearly and easily interpreted.** As far as Few is concerned, you should nearly always be using a grid in your plotted visualizations.

### Interpreting what we see:

Just taking a quick glance at the plot, we can see that as a car's weight increases, its MPG performance decreases. In other words, **higher vehicle weight is negatively correlated with fuel economy.** This makes sense; more energy is required to move more mass. This example is typically pretty common knowledge, but it helps to illustrate the concept of visualizing relationshpis between variables on a scatter plot.

## So what about more complex relationships between variables?

The basic scatter plot with just 2 variables does look quite simple, but in reality, there are often many factors or "variables" acting on your data to produce a given outcome.

As in this case, weight is one, but not the only variable that has a relationship with the MPG a car sees. The `mtcars` dataset itself has 11 variables (or columns) associated with each car. **How do you visualize and explore relationships between so many variables at once?**

### Meet: the scatter plot matrix:

Thankfully, one option we have available to us is to create a scatter plot matrix. This can also be done using either base `R` or `ggplot2`, and we will do so to compare the two.

A scatter plot matrix is good for **comparing multiple numerical variables at the same time.** It is also a good place to start with exploratory data analysis because it allows you to create just one initial visualization rather than many combinations.

### Can you spot the difference?

The scatter plot matrix using base `R`:

![mod-8-base-matrix-v2](https://github.com/user-attachments/assets/80749377-3c1c-4e32-ba17-04d9ad8794b1)

The scatter plot matrix using `ggplot2` *(and GGally):*

![mod-8-ggplot2-scatter-matrix-v2](https://github.com/user-attachments/assets/f363f16b-03d8-4dad-90f0-3b7069377fc5)


## There is a lot going on here: what does it all mean?

The scatter plot matrices require a little more interpretation than the simple scatter plots did.

Looking at the `R` base matrix, it seems that MPG and weight have the expected negative correlation. We can also see that as horsepower increases, MPG decreases. And we can see that heavier cars tend to have more horsepower. All of these observations are consistent with well established and expected outcomes thanks to the laws of physics.

As for the `ggplot2` *(featuring GGally)* visualization, each plot is visually distinct, but not in a way that is very meaningful. With different types of graphs used simultaneously in the presence of differing units, it is **difficult to interpret** what the visualization is actually trying to tell us, especially in regards to each variable realtive to another.

In this case, the `R` base matrix is **the simpler and more clearly understood visualization** of the two. Despite the fact that there are few contextual axis labels and the scatter plot is not affixed to a visible grid, it is still possible to decipher what the plots represent in terms of overall patterns in the dataset. 

While the second image looks a little more interesting and utilizes gridlines, Few would tell you *not* to use it because it violates several of his **core visualization principles: clarity, efficiency, and accuracy.** He discourages the use of visual clutter, or unnecssary visual attributes that do not aid the delivery of the information in the visualization.

### What would Few do?

Few would tell you to stick to the base `R` scatter plot matrix, but add gridlines and regression lines to **improve visual clarity and readability.** Some additional axis labels wouldn't hurt our case either.

## What is the takeaway here?

**Sometimes, simpler is better.** This is especially true when it comes to the realm of data visualization. However, it is important to keep both context and your audience in mind. The first, simple scatter plot would likely be useful and easily understood by a third party, while the complex scatter plot matrix would be a more applicable tool for a researcher.

In the real world, you'll often need to experiment with multiple different kinds of visualizations until you strike the right balance for the information you're intending to convey. And as always, before you can begin creating your visualizations, you must ensure that you are asking a specific question that can be answered effectively.
