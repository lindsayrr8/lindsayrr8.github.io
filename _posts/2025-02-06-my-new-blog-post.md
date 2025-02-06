# Creating a Basic Time Series Visualization with Tableau

Having been introduced to Tableau in the previous posts, we are now tasked with creating a first basic **time series visualization.** We will accomplish this using a monthly modal time series dataset sourced from data.gov. The goal of this exercise is to understand some basic practices with Tableau for the purpose of visualizing a relationship between different variables over time.

## Objective:
The dataset contains 10 variables, of which we are instructed to select 6 for the visualization. From these 6 variables, we should conduct a basic analysis to identify meaningful trends.
<br ><br />
*A note on isolating the variables:*

Generally speaking, a best practice would be to **remove the unneeded variables** (data columns) in a copy of the original file before we begin. That way, we're being careful and efficient by importing only what's needed for the final analysis. However, if circumstances call for it, Tableau makes it possible to "remove" certain data from our analysis after we've already imported it. To do so, on the Data Source tab, you can right click a column with unneeded data and select "hide."

To begin, we can import the dataset, which comes to us cleaned and in the format of an excel spreadsheet. Tableau makes this easy to do. Once we've imported the dataset, we can **select 6 variables that seem most relevant for analysis.** Our variable options are:

- 5 Digit NTD ID
- Primary USA Code
- Primary USA City
- Primary USA Sq Miles
- Year
- Vehicle Revenue Miles
- Vehicle Revenue Hours
- Ridership
- Collisions with Motor Vehicle
- Collisions with Person

## Asking a Question for Analysis:

Now that we have the data, we can start asking questions that will lead us to discovering meaningful insights. There are many questions we might ask just looking at the overview of this dataset:

How many vehicles hit a car or a person each year, and how has that changed over time?
Are certain areas more prone to accidents than others? Has this changed over time?
What is the relationship between vehicle revenue, vehicle miles, and ridership trends over time?



