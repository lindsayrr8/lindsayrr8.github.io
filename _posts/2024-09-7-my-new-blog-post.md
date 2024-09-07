## 9-7-24

#### This week in Advanced Statistics & Analytics, we're given the following snippet of R code to work with:

```R
assignment2<- c(6,18,14,22,27,17,22,20,22)
myMean <- function(assignment2) {return(sum(assignment2)/length(assignment2))}
```
*...and suddenly I find myself learning not only R, but html, markdown, and CSS for this blog, too!*

But since I'm all back end at this point, let's take a peek under the hood at what's going on here with R:

`assignment2` is a vector of numbers: `6,18,14,22,27,17,22,20, and 22.`
In R, **vectors** are one-dimensional arrays that can hold one data type, such as numeric, character, or logical data. (In other words, numbers, strings, or T/F values.)

To create a vector in R, you use the **combine function: c().**

```R
assignment2<- c(6,18,14,22,27,17,22,20,22)
```

Splendid. Now that we have our vector full of numbers, we can create our own new function called **myMean()** to calculate the average of these numbers.

We'll designate **myMean()** as the name for the nice box our function will sit in. *Doing this in R gives me the heebie-jeebies because `=` is conventionally used for **assignment** in pretty much every other language.* In R, `<-`, (which looks like a little left-facing arrow) is the standard assignment syntax on variables. The `=` still gets used, but it's more-or-less officially designated for functions.


