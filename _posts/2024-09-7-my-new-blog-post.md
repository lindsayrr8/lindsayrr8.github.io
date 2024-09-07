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

`myMean <- function(assignment2) {return(sum(assignment2)/length(assignment2))}`

We'll designate `myMean()` as the name for the nice box our function will sit in. Doing this in R gives me the *heebie-jeebies* because `=` is conventionally used for variable **assignment** in pretty much every other language.
In R, `<-`, (which looks like a little left-facing arrow) is the standard assignment syntax. The `=` still gets used, but it's more-or-less designated for use *inside* functions.

Our new function `myMean()` pulls in the data stored in `assignment2` and makes use of another pre-cooked function that comes packed in with R: the `sum()` function. This guy, `sum(assignment2)`, is calculating the sum of all the elements stored in `assignment2` for us.

Then, with a good ol' `/`, R will divide the result by `length(assignment2)`. That guy is computing the number of elements in the `assignment2` vector so we don't have to!

Thusly, we have `sum(assignment2)/length(assignment2)`, which divides the sum of our vector by the number of elements in it... AKA, the average (mean)!

At last, the `return()` function tells R what to come back with whenever our `myMean()` function is called.

## (Thanks, science!)

