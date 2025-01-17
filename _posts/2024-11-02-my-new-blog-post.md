# Tabular Data with R
Yes, it's exactly what it sounds like. Tabular refers to **"tables,"** as in data tables, which is what we'll be focusing on today.

### Why does tabular data matter?
There are several good reasons. Put simply, because it lets people easily see and do things quickly with the data. Additionally, it allows for the creation of relationships between different fields of data. This is especially important when you get into relational databases.

## To get a grip on tabular data, we'll be answering the following questions:
> _From the given data frame:_
> 
> **Question 1:** <br />
> Generate (1) a one-way table for "purchased" and (2) a two-way table for "country" and "purchased." <br />
> 
> **Question 2:** <br />
> Generate a contingency table, also known as rx C table, using the mtcars dataset. <br />
> **2.1** Add the addmargins() function to report on the sum totals of the rows and columns of "mtcars_df" table <br />
> **2.2** Add prop.tables() function, and report on the proportional weight of each value in the "mtcars_df" table <br />

## Question 1.
The data frame we already have to work with is:
```R
df <- data.frame(
  country = c("France", "Spain", "Germany", "Spain", "Germany", "France", "Spain", "France", "Germany", "France"),
  age = c(44, 27, 30, 38, 40, 35, 52, 48, 45, 37),
  salary = c(6000, 5000, 7000, 4000, 8000, 6000, 5000, 7000, 4000, 8000),
  purchased = c("No", "Yes", "No", "No", "Yes", "Yes", "No", "Yes", "No", "Yes")
```
Not very pleasing to the eye, if I'm honest. Just looking at the data in this form, it's cumbersome and time consuming to try to gleam insights about it.

## This is where tables come in.
Thankfully, R makes this very easy for us. We can use the `table()` function to put the data in a format that is more readable and useful to us.

A **one-way table** is a very basic kind of table that we can start with to display this data coherently:
```R
# Create one-way table for "purchased"
one_way_table <- table(df$purchased)
print(one_way_table)
```
Doing so yields the output:
```R
> print(one_way_table)

 No Yes 
  5   5 
> 
```
Pretty simple, right? Much more readable, too. Putting the data into a table like this is called **tabulating.**

In a nutshell, the `table()` function takes one or more vectors and counts the occurrences of each unique value in a given column, depending on what you specify.

And speaking of more vectors, we can also use `table()` to create a **two-way table:**
```R
# Create two-way table for "country" and "purchased"
two_way_table <- table(df$country, df$purchased)
print(two_way_table)
```
Which gives us the output:
```R
> print(two_way_table)
         
          No Yes
  France   1   3
  Germany  2   1
  Spain    2   1
> 
```
Nice. As you can see, a one-way or a two-way table have different applications and can tell us different things depending on what we'd like to know about our data. In other words, a two-way table lets you see relationships between two variables, while a one-way table summarizes only one variable.

## Question 2.
## Here, we'll be generating a contingency table using the mtcars dataset. 
Yep, there's `mtcars` again. And we're even given a starting point in `R`:
```R
data(mtcars)
mtcars_df <- table(mtcars$gear, mtcars$cyl, dnn = c("Gears", "Cylinders"))
```
Which, by default, outputs the table:
```R
> mtcars_df
     Cylinders
Gears  4  6  8
    3  1  2 12
    4  8  4  0
    5  2  1  2
```
## Question 2.1:
The instructions say to: add the addmargins() function to report on the sum totals of the rows and columns of the "mtcars_df" table.

Okay, fortunately for us there's also a function for that. To do so, we can use `addmargins()`:
```R
# Add margins to show row and column totals
mtcars_df_with_margins <- addmargins(mtcars_df)
print(mtcars_df_with_margins)
```
And if we check out the result, this is what we get:
```R
> print(mtcars_df_with_margins)
     Cylinders
Gears  4  6  8 Sum
  3    1  2 12  15
  4    8  4  0  12
  5    2  1  2   5
  Sum 11  7 14  32
```
## Question 2.2:
From here, we can: add the `prop.tables()` function and report on the proportional weight of each value in the "mtcars_df" table, as instructed.
```R
# Proportional table for mtcars_df
mtcars_df_prop <- prop.table(mtcars_df)
print(mtcars_df_prop)
```
Which gives the output:
```R
> print(mtcars_df_prop)
     Cylinders
Gears       4       6       8
    3 0.03125 0.06250 0.37500
    4 0.25000 0.12500 0.00000
    5 0.06250 0.03125 0.06250
```
Looking much better than when we started, right? This is just a basic taste of how powerful analyzing tabular data can be with R.

## Interpreting the results:
A few glances at the data can tell us several things:
- Cars with 3 gears and 8 cylinders occupy the largest proportion of the data set at 37.5%.
- Cars with 4 gears and 4 cylinders are also common, making up 25%.
- There are no cars that have 4 gears and 8 cylinders. This definitely checks out.
