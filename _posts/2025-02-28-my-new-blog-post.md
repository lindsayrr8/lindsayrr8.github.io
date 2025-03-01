# Distribution Analysis Visualizations: Where Do We Start?

So you have yourself a dataset and someone has tasked you with analyzing it for insights. Then, you're to create visualizations for the insights you collect to spare others the crunch time and the paperwork. Where do you begin?

Sometimes just viewing the structure or the first few rows of the dataset can give you an idea of what you're working with, but it is often quite insufficient for revealing trends in your data. This is where you'd **start running some statistical tests** - but in order to do so, you still need more information about the distribution of the data you're working with.

In other words,  **the distribution of your data significantly affects the type of statistical test you should use on it.**

## So, how do we approach figuring out the distribution of a dataset?

To give a simple demonstration, we're turning back to `R` and its built-in `mtcars` dataset.
