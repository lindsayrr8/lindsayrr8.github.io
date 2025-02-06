# Creating a Basic Time Series Visualization with Tableau

Having been introduced to Tableau in the previous posts, we are now tasked with creating a first basic **time series visualization.** We will accomplish this using a monthly modal time series dataset sourced from data.gov. The goal of this exercise is to understand some basic practices with Tableau for the purpose of visualizing a relationship between different variables over time.

## Objective:
The dataset contains 10 variables, of which we are instructed to select 6 for the visualization. From these 6 variables, we should conduct a basic analysis to identify meaningful trends.
<br ><br />
*A note on isolating the variables:*

Generally speaking, a best practice would be to **remove the unneeded variables** (data columns) in a copy of the original file before we begin. That way, we're being careful and efficient by importing only what's needed for the final analysis. However, if circumstances call for it, Tableau makes it possible to "remove" certain data from our analysis after we've already imported it. To do so, on the Data Source tab, you can right click a column with unneeded data and select "hide."

To begin, we can import the dataset, which comes to us cleaned and in the format of an excel spreadsheet. Tableau makes this easy to do. Once we've imported the dataset, we can **select 6 variables that seem most relevant for analysis.** Our variable options are:

```
• 5 Digit NTD ID
• Primary USA Code
• Primary USA City
• Primary USA Sq Miles
• Year
• Vehicle Revenue Miles
• Vehicle Revenue Hours
• Ridership
• Collisions with Motor Vehicle
• Collisions with Person
```

## Asking a Question for Analysis:

Now that we have the data, we can start asking questions that will lead us to discovering meaningful insights. There are many questions we might ask just looking at the overview of this dataset:

- How many of the vehicles combined hit a car or a person each year, and how has that changed over time?
- Are certain areas more prone to vehicular accidents than others? Has this changed over time?
- What is the relationship between vehicle revenue, vehicle miles, and ridership trends over time?

In this case, we're asked to create **1 visualization that analyzes 6 of the variables at once.** Therefore, the 6 most likely variables with quantifiable data to provide a general analysis are:
```
# The date value for scale
• Year

# The monetary service life of vehicles
• Vehicle Revenue Miles

# The clocked hours of vehicles' monitary service
• Vehicle Revenue Hours

# The number of people riding in the vehicles
• Ridership

# Accidents between service cars
• Collisions with Motor Vehicle

# Accidents involving a service car and a person
• Collisions with Person
```

I did not select the `"5 Digit NTD ID, Primary USA Code, Primary USA City, (and) Primary USA Sq Miles"` variables because their relationships are more relevant to specific individual variables and **less relevant for a general overview.**

For example, an analysis of `Ridership` per `5 Digit NTD ID` might tell us about a specific car's performance, but not about the dataset as a whole. As another example, while something like `Collisions with Motor Vehicle` in a `Primary USA City` might tell us meaningful information about accident rates in that specific place, it is much less likely to tell us about **trends in the dataset as a whole.**

## Creating the Visualization:
Having selected the 6 variables for analysis, we can begin creating a visualization that will help us identify general trends in the dataset.

To do this, I navigated to the "Sheet 1" tab that Tableau automatically generates. From there, I followed these steps:
> 1. From the available data fields on the left side of the screen, I selected `"Year"` and dragged it to the empty field for "columns" at the top of the blank workspace. A "ruler" with years from 2013-2020 should appear.
> 2. Next, I selected the fields `"Collisions with Motor Vehicle, Collisions with Person, Ridership, Vehicle Revenue Hours, (and) Vehicle Revenue Miles,"` and dragged those into the empty field for "Rows" at the top of the blank workspace. 5 stacked line graphs should appear.
> 3. Last, I changed the colors of each line so they are easier to visually differentiate.

And here is the result:
![Module4TimeSeriesAnalysis](https://github.com/user-attachments/assets/6bffc391-a18f-484e-9f99-3eba6f38fbd9)

## Analyzing the Results:
At first glance, it is easy to see that **each metric follows the same general trend in the data.** `Collisions with Motor Vehicle, Collisions with Person, Ridership, Vehicle Revenue Hours, (and) Vehicle Revenue Miles` all trend pretty statically between 2014 and 2018. Then, from the point between 2018 and 2019, every category trends consistently downward in numbers.





