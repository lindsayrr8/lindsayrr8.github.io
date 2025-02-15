# Creating a Visualization with Plotly, Python, and Jupyter Notebook

For this exercise, we are prompted to create a visualization using Plotly. To do so, we are given a basic time series dataset with two columns: "Average Position" and "Time."

**Plotly** (or Plot.ly) is a **free, open-source graphing library** that can be accessed with an internet browser. Under the hood, Plotly is a `JavaScript` library useful for creating interactive visualizations on the web. You might choose to use Plotly when you need to create dashboards, data exploration tools, or other interactive objects intended for web pages. Plotly also comes as a `Python` or `R` library, both of which are built on top of Plotly.js.

## Simple Tools for Simple Visualization Concepts
Two of the most **basic design elements** to keep in mind when creating data visualizations are: **"Part to Whole"** and **"Ranking."**

Simply put, "Part to Whole" visualizations are intended to show how individual parts contribute to a total of something. A common example of this kind of visualization would be a pie chart.

"Ranking" visualizations are intended to showcase order, meaning comparing items based on some specific value. A common example of a ranking visualization is a bar chart.

Plotly graphics can be useful for creating basic visualizations like these quickly and easily. Many publicly available templates exist on [**Plotly Chart Studio**](https://chart-studio.plotly.com/feed/#/) which can be freely edited to suit your specific needs. At the time of this blog posting, Plotly has suspended all new account creation until further notice, so editing a public template without the need for an account is exactly the approach we'll take.

## Using Plotly for Web Browsers
To start, I searched for a simple, public line chart using the search term "time series line graph." This type of graph is most suitable for visualizing the time series dataset we've been given.

I selected a template titled "line mode" and imported my dataset, assigning "Time" to the x-axis and "Average Position" to the y-axis under "Traces" in the "Structure" menu. With just a few clicks, I have my interactive time series graph that reveals data values at certain intervals when I mouse over any spot on my line.

**And here is the result** (PNG format):

<img width="390" alt="time series line graph module 5" src="https://github.com/user-attachments/assets/d2336ac1-5d88-46a8-a8f3-1bcc7404c54e" />

Unfortunately, without an account I can't directly export the `html` code with my new interactive graph, so I decided to recreate the graph in Python next using the Plotly Python package.

## Recreating The Line Graph with Plotly for Python
Here's a hot tip for you: most IDE's *(integrated development environments)* for writing code are not configured with creating data visualizations in mind. That's why scientific programming languages like `R` exist with their own proprietary development environments, like RStudio. As a result, it can be tricky to choose the right environment for creating visualizations, and headaches will insue if you don't.

There are tons of approachs to writing `Python,` but with visualizations in mind, I chose to complete this task using the available tools included with **Anaconda Navigator.** *(Yes, more snakes.)* Anaconda Navigator is a free, open-source GUI that you can think of as a collection of applications useful for scientific computing, visualizing data, and working with AI, all using `Python.`

In particular, with the spirit of Plotly's browser-based visualizing in mind, I chose to code my graph using **Jupyter Notebook.** Jupyter Notebook is another freebie interactive browser-based environment that is used by industry data scientists, analysts, researchers, and other information professionals. It differs from Plotly in that Jupyter is a little more technical. But as you will see, we will be using Plotly's `Python` package to recreate the graph utilizing Jupyter Notebook.

### After loading up Jupyter Notebook and creating a new file, we need to import a few necessary `Python` libraries:
```Python
# Use pandas for data analysis tools and excel file functions
import pandas as pd

# Use Plotly's python package
import plotly.express as px
```

Cool beans. The rest really is just a few simple steps. There's very little hard coding involved thanks to the wide availability of preset libraries available for `Python.`

The first step is to read in the dataset, which is in the format of an Excel file. Then we'll take a look at the resulting data frame:
```Python
# Set the file path for the Excel file from wherever you've stored it
file_path = "C:/Users/user/Desktop/thedataset.xlsx"

# Read the file into a data frame using pandas: pd.read_excel()
df = pd.read_excel(file_path)

# Display first rows to check out the data using pandas: df.head()
print(df.head())
```

Not so different from `R`, right? That's because many of these **basic data analysis concepts are consistent across different programming languages.** Take a look at our data frame:

```Python
  Unnamed: 0  Average Position  Time
0           1          0.176268   0.0
1           2          0.189679   0.2
2           3          0.219623   0.4
3           4          0.258176   0.6
4           5          0.325576   0.8
```

Very swanky. Now we're going to use the `px.line()` function from the Plotly Express package to plot the line:

```Python
# Create the line chart
fig_line = px.line(df, x = "Time", y = "Average Position",
                   title = "Average Position Over Time (Line Graph)",
                   labels = {"Time": "Time", "Average Position": "Average Position"},
                   markers = True)

# Show the line chart
fig_line.show()
```
And if we run it, we get this nifty result (PNG format):
![Plotly-Python-JupyterNotebook-linegraph](https://github.com/user-attachments/assets/0484d196-baa8-4512-930d-fee44e12b2eb)

Now, with the code in hand, we can use a simple function to write the new line graph to `html` format. That way, I can set it as an interactive object on this blog page.

To do that, I ran:
```Python
# Write graph to html format
fig_line.write_html("C:/Users/user/Desktop/interactive_graph.html")
```
And now, the object is fully interactible on this page ~*(infinite compatibility hurdles permitting):*~

<iframe src="[https://observablehq.com/embed/@your-username/your-notebook-id](https://static.observableusercontent.com/files/daa82ea66dbec2600a534acc2bcaee6c25f3c5ae653903612c9b11f719b61cd364c70ea26fbdcd6ecf2fc9f2ac3639e59f652c3ac8837d0c3f485fd8458d0bb9)" width="100%" height="600px"></iframe>



