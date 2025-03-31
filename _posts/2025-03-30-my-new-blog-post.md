# Comparing Visualizations Between Base R and ggplot2

This week, we're going to briefly cover some visual differences between plots using base R and ggplot2. Since I've already covered ggplot2 and some differences between it and base R on this blog, we're going to keep this brief and focus on the image rather than the code.

To do this, we'll be using the `economics` dataset that comes packaged in with RStudio, which showcases unemployment rates over time.

## Comparing the Methods
How does the same visualization differ with different types of graphs and different implementation methods? As we've seen before, base R and ggplot2 share their similarities and they each have their advantages.

To begin, I've chosen to group the dates in the `economics` dataset per 5 years. I'll also be highlighting peak years in dark red:

**Base R plot:**

![base-r-graph-1](https://github.com/user-attachments/assets/06357720-c460-4a74-9e4f-035280f1b129)


**And the same plot recreated with ggplot2:**

![graph-2-ggplot2](https://github.com/user-attachments/assets/ba3e3d4b-e633-4ebf-9397-198fcb572334)



