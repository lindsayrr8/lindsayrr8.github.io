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
Pretty simple, right? Much more readable, too. In a nutshell, the `table()` function takes one or more vectors and counts the occurrences of each unique value in a given column, depending on what you specify. Putting the data into a table like this is called **tabulating.**







Speaking of more vectors, we can also use `table()` to create a two-way table:
