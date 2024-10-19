# Linear Regression with R

Linear Regression is an important concept in predictive analytics. But what do we use it for? ***Simple Linear Regression*** is a way to describe a relationship between two variables. Typically, we think of these two variables as a **dependent variable** and an **independent variable.** Equivalent terms that we'll be using for these variables are the **response and predictor variables,** respectively.

The word "regression" in this context literally refers to a measurement of a relationship between two variables. However, it might also make some sense to apply the alternate definition of regression here, which means to return to a previous or more basic state.

I like to associate it with the idea of untying a knot. When a shoelace, for example, is tied into a neat bow, someone just stumbling upon it for the first time might have difficulty figuring out where the knot begins and ends (or frankly, what the heck happened here.) Thankfully, with shoes as in mathematics, we've developed a process to untie the knot, making it simpler and easier to figure out how the knot works at each step in the process. That way, we can derive a reasonable explanation for how 'A' probably led to 'B.'

However, it's very important to note that linear regression **does not inherently describe a causal relationship.** The relationship it finds (or doesn't find) could indeed turn out to be causal in the real world, but at minimum, we can only know for certain from our initial analysis if the relationship is *correlational.* **That's what linear regression does: it describes correlation.** 

With that in mind, correlation can be either positive or negative. **Positive correlation** means that the relationship trends in an "upward" or positive pointing way (ex: 1, to 5, 10, 20+). Conversely, **negative correlation** means that the relationship trends in a "downward" or negative pointing way (ex: 1, -5, -10, -20+). Using linear regression, we look for a summary of this trending relationship in the form of a **best fitting line.** It is what it sounds like: a line that essentially follows the direction of the data.

Under the hood, this is accomplished by minimizing the sum of the squared distances between the line and the actual data points on a scatter plot. Thankfully, as always, *we will be letting R handle this for us.*

## This week, we're asked to evaluate several questions to demonstrate working knowledge of analyzing linear regression problems in R.

## Question 1:
> The datasets in this assignment: <br />
> 
> x <- c(16, 17, 13, 18, 12, 14, 19, 11, 11, 10) <br />
> y <- c(63, 81, 56, 91, 47, 57, 76, 72, 62, 48) <br />

> **1.1 Define the relationship model between the predictor and the response variable;** <br />
> **1.2 Calculate the coefficients** <br />

First thing's first: remember that "predictor variable" = independent variable and "response variable" = dependent variable.

So, we have our data sets and our tasks. First, let's let R handle finding the "relationship model" between the sets. We can do this using R's built-in `lm()` function ("lm" stands for linear model.")

```R

```
What are we looking at here? Let's break it down line by line.

In this case, the formula `Y ~ X` translates in English to: "response variable ('Y') is explained by ('~') the predictor variable ('X')." Computers really are short on words, aren't they? Note that 'Y' and 'X' represent their respective response/predictor variables by convention using this formula. In other words, when we're talking about `lm()`, 'Y' is always the response variable and 'X' is always the predictor variable.



