# Tabular Data with R
Yes, it's exactly what it sounds like. Tabular refers to **"tables,"** as in data tables, which is what we'll be focusing on today.

### Why does tabular data matter?
There are several good reasons. Put simply, because it lets people easily see and do things quickly with the data. Additionally, it allows for the creation of relationships between different fields of data. This is especially important when you get into relational databases.

## To get a grip on tabular data, we'll be answering the following questions:
> From the given data frame:
> Generate (1) a one-way table for "purchased" and (2) a two-way table for "country" and "purchased."

The data frame we have to work with is:
```R
df <- data.frame(
  country = c("France", "Spain", "Germany", "Spain", "Germany", "France", "Spain", "France", "Germany", "France"),
  age = c(44, 27, 30, 38, 40, 35, 52, 48, 45, 37),
  salary = c(6000, 5000, 7000, 4000, 8000, 6000, 5000, 7000, 4000, 8000),
  purchased = c("No", "Yes", "No", "No", "Yes", "Yes", "No", "Yes", "No", "Yes")
```
Not very pleasing to the eye, if I'm honest. Just looking at the data in this form, it's cumbersome and time consuming to try to gleam insights about it.

## This is where tables come in.
