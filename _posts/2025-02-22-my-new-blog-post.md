# Back to the Basics: Making Visualizations That Make Sense

In the modern day, there are many different tools and approaches available for creating data visualizations. With the enormous amount of complex data out there, it can sometimes be intimidating to decide where to even **start visualizing it.**

Disciplines like statistics and the arts offer us some general, **conventional guidelines.** Conventions like these exist for the same reason visual analytics exist: to help us communicate meaningful information. *(You will hear those words a lot in the realm of data science.)*

Making information meaningful is a bit of a philosophy of its own. It's an endeavor that is equal parts art and science, much like the discipline of data science itself. Based on both how our brains process information and how we expect standardized patterns that we've become accustomed to, there's a cluster of **techniques you can employ to make *"good"* visualizations.**

In the text *"Now You See It: Simple Visualization Techniques for Quantitative Analysis,"* and *"Now You See It: Simple Analytics Techniques for Quantitative Analysis,"* Few and Yau present a set of these **visualization principles.** Few emphasizes simplicity, clarity, and avoiding unnecessary decoration on visualizations. This practice would include avoiding complex or misleading visuals that hinder interpretation. Yau also endorses clarity, but further encourages exploration and storytelling with data. His approach considers the subjectivity of the context and the audience for the visualization.

## Creating a Basic Visualization Utilizing These Principles

With these princples in mind, we are **tasked with creating a basic visualization** using `R`. In this case, I'll be focusing more on the style than the code since I've covered `R` pretty extensively already on this blog.

To complete the activity, I've chosen to create a bar chart in line with both Few and Yau's recommendations. A bar chart will be simple, easy to interpret, and easy to style with different colors. I'll be using `R`'s preset `diamonds` dataset to create the bar chart. With it, I'll be comparing the average carat weight of the diamonds in the set by their relative clarity.

I'll set up my initial bar chart with the variables `carat` on the y-axis and `clarity` on the x-axis. This is because it's a standard practice to place categories (like clarity) on the x-axis and numerical values (like carat weight) on the y-axis. *(Humans are pretty good at evaluating things upright, but sideways can be a little weird for us.)*

![upright_bar_chart](https://github.com/user-attachments/assets/437a02cd-50ba-490b-95cb-b74bf478f137)


However, I'm a firm believer that showing bad examples is necessary to understand why good examples are "good" instead of me just telling you it is, so take a look at the difference for yourself:

![bar_chart_sideways](https://github.com/user-attachments/assets/7a7d08d9-064f-4bee-81cf-cf0ea2882cf1)


Did it take you a little longer to interpret the sideways bar chart than the upright one? This means your brain is working normally (congratulations!)

Yes, the second bar graph is interpreatable, but in the real world an extra few seconds of processing makes a difference ~~*(especially if you are a driver in Florida.)*~~ If you wanted to purchase a product or service from two different companies and you only had a few seconds to glance at each graph, which would you pick to spend your time and money on?

## Now, let's make the first chart better:
We'll approach this by adding some color to visually differentiate the `clarity` categories:

![diamonds_bar_chart_updated](https://github.com/user-attachments/assets/55d90ace-63ce-4d42-b0c5-3bc93ca581d9)


This updated visualization allows the viewer to quickly look at the chart and gain insights. It is simple, clear, and stylistic.

I chose a color spectrum from purple to very light blue to denote clarity. I avoided colors like red and green for *"bad"* and *"good,"* because that's not the point I'm trying to make here. I also avoided using brown or yellow since that could confuse the viewer with diamond color rather than clarity.

The visual key indicates that the most included diamonds are represented by dark purple, while the least included diamonds are a light blue, and flawless diamonds are a whiteish blue. This color pattern mirrors the visual relationship that real diamonds with inclusions have: more inclusions creates more visual "darkness," while fewer inclusions create a clear or whiteish appearance.

We know at a glance that the bigger the diamond carat weight, the more likely it is to have inclusions. We also know that most of the diamonds in the set feature inclusions, while the fewest diamonds are very very slightly included `VVS1` or flawless `IF`. These diamonds also tend to be a relatively small carat weight.
