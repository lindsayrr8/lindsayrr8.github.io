# Comparing Time Series Visualizations Between Base R and ggplot2

This week, we're going to briefly cover some visual differences between plots using base R and ggplot2. Since I've already covered ggplot2 and some differences between it and base R on this blog, we're going to keep this brief and focus on the image rather than the code.

To do this, we'll be using the `economics` dataset that comes packaged in with RStudio, which showcases unemployment rates over time.

## Comparing the Methods
How does the same visualization differ with different types of graphs and different implementation methods? As we've seen before, base R and ggplot2 share their similarities and they each have their advantages.

To begin, I've chosen to group the dates in the `economics` dataset per 5 years. I'll also be highlighting peak years in dark red:

**Base R plot:**

![base-r-graph-1](https://github.com/user-attachments/assets/06357720-c460-4a74-9e4f-035280f1b129)


**And the same plot recreated with ggplot2:**

![graph-2-ggplot2](https://github.com/user-attachments/assets/ba3e3d4b-e633-4ebf-9397-198fcb572334)


Here base R looks a little cleaner while ggplot2 looks a little more detailed. In both cases, we can quickly and easily identify a pattern.

From at least 1965 to about 1975, unemployment followed a rising trend. From about 1975 to 2000, it oscillated and spiked fairly consistently about each decade. But between 2005 and 2015, and particularly around 2010, unemployment rates spiked and continued to remain higher than previous averages. It's reasonable to assume that the extreme spike around 2010 reflects the infamous 2008 recession.


### Will looking at the data in the form of other visalizations reveal additional insights? Let's find out.

Let's start with an example. We've all seen a very common economic visualization in the form of some variation of a sparkline. This one was made with `qplot()`, which is a part of ggplot2:

![qplot-graph-4](https://github.com/user-attachments/assets/b2f2a729-d866-407b-9f95-c2b055295edd)

And if we expand on this one using more of ggplot2's capabilities, it can be modified to look like this as well:

![spaghetti-plot-ggplot2](https://github.com/user-attachments/assets/246bd4f3-379c-4e1d-85cb-db083a90dbe1)


In line form rather than as bars, we can see more of the little variations as unemployment trends change over time. In the grand scheme of factors that influence highly complex metrics like unemployment, small fluctuations can sometimes be otherwise hidden warning signs. This becomes especially valuable when we move into the medium of predictive analytics.

But looking at the graphs, despite their additional complexity, we can still see the overall trends with relative ease. Unemployment peaks do tend to happen roughly around the mark of each decade, following a somewhat cyclical pattern.

The second graph, which plots both unemployment and the median unemployment duration, adds an additional layer of complexity. Here, you can see a direct relationship between high unemployment rates and longer periods of unemployment. This likely reflects compounding conditions resulting from fallout during economic events. But as is the trade off, with more complexity comes more challenge at interpretation.

One thing I find interesting about these graphs is the implications I'm made to think about from the limited information given. As I often mention here, the trade off with simplicity and ease of interpreting a visualization necessitates a loss of certain kinds of information.

While it isn't present on any of these visualizations, I'm left to consider the implications of experiencing multiple economic crises in one lifetime. Timing is a factor that can dramatically affect economic outcomes for many years after the fact.

## Visualization in Time Series Analysis
This exercise has demonstrated how visualization is an especially critical aspect of time series analysis. Visualizations like these graphs offer us the ability to capture both small fluctuations and important, overall trends in a dataset. The challenge lies with striking a balance between complexity and simplicity while navigating an inherent loss of information. They should therefore be carefuly crafted to convey the most necessary and relevant information, the discretion of which is up to the inquiring data analyst.
