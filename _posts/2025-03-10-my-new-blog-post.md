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

As in this case, weight is one, but not the only variable that has a relationship with the MPG a car sees. The `mtcars` dataset itself has 11 variables (or columns) associated with each car. How do you visualize and explore relationships between so many variables at once?

### Meet: the scatter plot matrix:



