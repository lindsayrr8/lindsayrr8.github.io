# ANOVA Testing with R

ANOVA is an important analysis concept. As the acronym might imply, **it stands for: "Analysis of Variance."**

ANOVA is a statistical test which is used to **determine if there are significant differences** between the means of three (or more) independent groups. The purpose is to assess whether the observed differences between the group means are due to random chance or if they have statistical significance.

## When do we use ANOVA?
Briefly, ANOVA is used when:
- Comparing more than two groups
- Examining one or more independent variables
- Testing for overall differences

### In this week's scenario, we can use ANOVA to evaluate the following prompt:
> Question 1 A researcher is interested in the effects of drug against stress reaction. She gives a reaction time test to three different groups of subjects: one group that is under a great deal of stress, one group under a moderate amount of stress, and a third group that is under almost no stress. The subjects of the study were instructed to take the drug test during their next stress episode and to report their stress on a scale of 1 to 10 (10 being most pain).

The data that was collected is displayed in this table:

| High Stress	| Moderate Stress |	Low Stress |
|---|---|---|
| 10 | 8 | 4 |
| 9 |	10 | 6 |
| 8 |	6 |	6 |
| 9 |	7	| 4 |
| 10 | 8 | 2 |
| 8 |	8 |	2 |
## Question 1:
> Report on drug and stress levels by using R. Provide a full summary report on the result of ANOVA testing and what it means. More specifically, report the following: `Df, Sum, Sq Mean, Sq, F value, Pr(>F)`

Alright. Let's approach this one step at a time. A good place to start will be to convert the information we've been given to `R` for analysis:
```R
# Do ANOVA test
# Create the data frame
stress_data <- data.frame(
  Stress_Level = factor(rep(c("High Stress", "Moderate Stress", "Low Stress"), each = 6)),
  Reaction_Time = c(10, 9, 8, 9, 10, 8, 8, 10, 6, 7, 8, 8, 4, 6, 6, 4, 2, 2)
)
```
### Looks good. But what's happening here?

First, we've taken the data we were given and stuffed it into a data frame for `R` to work with. Then, we've defined two columns for "Stress Level" and "Reaction Time."

For `Stress_Level`, we've specified to R that this data will be considered factors. This is very important for ANOVA testing, as it allows R to associate and compare values in an ordinal way (ex: one being higher or lower in value than another.)

We've also wrapped our new vector in with the `rep()` function, which helps to repeat each entry per stress level 6 times. If you notice from the original table, this is because we have 6 "reaction time" values for each level of stress ("High," "Moderate," and "Low.") You can play around with this, but the alterative to using the `rep()` function would be to type each of "High," "Moderate," and "Low" 6 times. I'd rather not, but here's what that would look like:
```R
# This is equivalent to using rep()
stress_data <- data.frame(
  Stress_Level = factor(c("High Stress", "High Stress", "High Stress", "High Stress", "High Stress", "High Stress",
                          "Moderate Stress", "Moderate Stress", "Moderate Stress", "Moderate Stress", "Moderate Stress", "Moderate Stress",
                          "Low Stress", "Low Stress", "Low Stress", "Low Stress", "Low Stress", "Low Stress")),
  Reaction_Time = c(10, 9, 8, 9, 10, 8, 8, 10, 6, 7, 8, 8, 4, 6, 6, 4, 2, 2)
```
Not very pleasing to the eye or to my nerves, so instead, we'll be proceeding with `rep()`, which again, does the exact same thing more conveniently.

Now we can perform ANOVA with just with just 1-2 lines of code using the `aov` function. Yes, really. (Thanks `R`!).
```R
# Performing ANOVA test
anova_results <- aov(Reaction_Time ~ Stress_Level, data = stress_data)
summary(anova_results)
```
You might recognize the `~` as indicating that we're building an analysis model. Remember that the `~` separates the dependent variable (in this case, `Reaction_Time`) from the independent variable (`Stress_Level`). In English, `Reaction_Time ~ Stress_Level` reads as: "see if `Stress_Level` has any effect on `Reaction_Time`." Lastly, `data = stress_data` tells `R` where to pull the data from (in this case, the data frame we created.)

Running the summary results in the output:
```R
> summary(anova_results)
             Df Sum Sq Mean Sq F value   Pr(>F)    
Stress_Level  2  82.11   41.06   21.36 4.08e-05 ***
Residuals    15  28.83    1.92                     
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```
### How do we interpret these results?
The information returned from our ANOVA test tells us:
- Df (degree of freedom): This represents the numer of levels in `Stress_Level` minus 1
- Sum sq (sum of squares): This represents the total variability in reaction times resulting from differences between groups
- Mean sq (mean square): This represents the average variability for each source (between and within groups)
- F valule: This is the test statistic for ANOVA. A higher F-value suggests greater likelihood that there is a statistically significant difference between group means
- Pr(>F) (the p-value): aka, the probability which is associated with the F statistic

### What this output tells us:
There are a few key takeaways here. Our p-value was calculated as 4.08e-05, which means 0.0000408. That's quite a bit lower than 0.05, which indicates there is statistical significance. In other words, it suggests a highly significant effect of `Stress_Level` on `Reaction_Time`. _(You could also observe the "`***`", which means "high degree of statistical significance" in R-speak. More stars = more significant.)_

Our F-value is also high (21.36). This indicates that the variance between groups (due to different stress levels) is much greater than the variance within groups (individual differences.)

A total breakdown of the results we got could be **summarized** by the following:
- Df: The result we got is 2. This is because there are three levels (High, Moderate, Low) of `Stress_Level`, so degrees of freedom = number of groups - 1 which is 3 - 1 = 2.
- Sum Sq: We got 82.11. This is the variability in reaction times that can be attributed to differences in stress levels.
- Mean Sq: We got 41.06. This is the Sum Sq divided by the degrees of freedom, which represents the average variation for `Stress_Level`.
- F value: We got 21.36. This statistic indicates the ratio of variation between groups (Stress levels) to the variation within groups (Residuals).
- Pr(>F): Again, this is the p-value, which represents the probability that the observed differences in reaction times are due to chance. In this case, it seems highly unlikely that they are explained by chance.

The **residuals** in our results consist of: `Df` (Degrees of Freedom), `Sum Sq` (Sum of Squares), and `Mean Sq` (Mean Square).

## Question 2:
We are instructed to complete the tasks for Question 2 given the following prompt:
> The zelazo data (taken from the R package called ISwR) are in the form of a list of vectors, one for each of the four groups. <br />
> <br > **2.1.** Convert the data to a form suitable for the user of lm, and calculate the relevant test. Consider t-tests comparing selected subgroups or obtained by combing groups. <br />
> <br > **2.2.** Consider ANOVA test (one way or two-way) for this dataset (zelazo) <br />

Okay, to get started, we need to load up the `ISwR` package in RStudio so we can start working with the `zelazo` dataset:
```R
# Install ISwR package if not already installed
install.packages(ISwR)
# Add to library
library(ISwR)
# Load in zelazo dataset
data("zelazo")
# Check out zelazo format
str(zelazo)
```
### Step 2.1: Convert the Data to a Suitable Format for lm()
Running `str(zelazo)` reveals that the `zelazo` object is typed as a list by default. The `lm()` function in R requires a data frame format. So, let’s **convert zelazo from a list to a data frame:**
```R
# Convert the zelazo list to a data frame suitable for lm()
zelazo_data <- data.frame(
  Group = factor(rep(c("active", "passive", "none", "ctr.8w"), 
                     times = c(length(zelazo$active), length(zelazo$passive), length(zelazo$none), length(zelazo$ctr.8w)))),
  Time = c(zelazo$active, zelazo$passive, zelazo$none, zelazo$ctr.8w)
)
```
### Wonderful. What's going on here?
To start, we're creating a new data frame called `zelazo_data`. Inside it, there are two columns. `Group` is the first column, which refers to the stress level for each observation. The second column is `Time`, which refers to the reaction times for each observation.

`Group` goes in typed as a factor so R can compare its values ordinally. Then, there's `rep()` again repeating each group name according to the number of values in each subgroup (using `length()`.)

Then, the line `c(zelazo$active, zelazo$passive, zelazo$none, zelazo$ctr.8w)` concatenates all individual vectors (active, passive, none, ctr.8w) into a single column.






