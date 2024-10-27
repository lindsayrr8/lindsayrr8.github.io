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
Report on drug and stress level by using R. Provide a full summary report on the result of ANOVA testing and what does it mean. More specifically, report the following: Df, Sum, Sq Mean, Sq, F value, Pr(>F)
