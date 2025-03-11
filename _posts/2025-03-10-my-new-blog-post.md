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

Thankfully, one option we have available to us is to create a **scatter plot matrix.** This can also be done using either base `R` or `ggplot2`, and we will do so to compare the two.

A scatter plot matrix is good for **comparing multiple numerical variables at the same time.** It is also a good place to start with exploratory data analysis because it allows you to create just one initial visualization rather than many combinations.

### Can you spot the difference?

The scatter plot matrix using base `R`:

![mod-8-matrix-base](https://github.com/user-attachments/assets/5e5c2ead-ed52-4f08-85d5-61af28fb77a4)

The scatter plot matrix using `ggplot2` *(and GGally):*

![mod-8-matrix-gg](https://github.com/user-attachments/assets/ab4cfc15-ca54-419c-b0e9-51875a42553c)

### There is a lot going on here: what does it all mean?

The scatter plot matrices require a little more interpretation than the simple scatter plots did. In this context, the matrix is something I'd use for myself as a researcher, but not necessarily something I'd present to an outside party looking for quick insights.

In this case, the `R` base matrix is the more simple and clearly understood visualization of the two. Despite the fact that there are no written, contextual axis labels, it is still possible to decipher what the plots represent in terms of overall patterns in the dataset. 

As for the `ggplot2` *(featuring GGally)* visualization, there is a lot going on and each plot is clearly visually distinct, but not in a way that is very meaningful. With different types of graphs used simultaneously in the absence of axis labels, it is difficult to interpret what the visualization is actually trying to tell us, especially in regards to each variable realtive to another.




