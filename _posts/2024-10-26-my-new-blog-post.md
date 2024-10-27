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
### Question 1:
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
#### Looks good. But what's happening here?

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







