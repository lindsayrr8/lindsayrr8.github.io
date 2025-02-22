# Back to the Basics: Making Visualizations That Make Sense

In the modern day, there are many different tools and approaches available for creating data visualizations. With the enormous amount of complex data out there, it can sometimes be intimidating to decide where to even **start visualizing it.**

Disciplines like statistics and the arts offer us some general, **conventional guidelines.** Conventions like these exist for the same reason visual analytics exist: to help us communicate meaningful information. *(You will hear those words a lot in the realm of data science.)*

Making information meaningful is a bit of a philosophy of its own. It's an endeavor that is equal parts art and science, much like the discipline of data science itself. Based on both how our brains process information and how we expect standardized patterns that we've become accustomed to, there's a cluster of **techniques you can employ to make *"good"* visualizations.**

In the text *"Now You See It: Simple Visualization Techniques for Quantitative Analysis,"* and *"Now You See It: Simple Analytics Techniques for Quantitative Analysis,"* Few and Yau present a set of these **visualization principles.** Few emphasizes simplicity, clarity, and avoiding unnecessary decoration on visualizations. This practice would include avoiding complex or misleading visuals that hinder interpretation. Yau also endorses clarity, but further encourages exploration and storytelling with data. His approach considers the subjectivity of the context and the audience for the visualization.

## Creating a Basic Visualization Utilizing These Principles

With these princples in mind, we are **tasked with creating a basic visualization** using `R`. In this case, I'll be focusing more on the style than the code since I've covered `R` pretty extensively already on this blog.

To complete the activity, I've chosen to create a bar chart in line with both Few and Yau's recommendations. A bar chart will be simple, easy to interpret, and easy to style with different colors. I'll be using `R`'s preset `diamonds` dataset to create the bar chart. With it, I'll be comparing the average carat weight of the diamonds in the set with their relative clarity.



