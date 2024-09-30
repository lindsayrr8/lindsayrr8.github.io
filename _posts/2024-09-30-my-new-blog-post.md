# Hypothesis Testing & Correlation Analysis with R

This week, we're biting into the meat of the statistics burger. We're still working with the statistical basics, but this time we'll be applying them with a few new formulas to do some simple analyses. As always, we'll be *letting R handle everything for us.*

To begin, let's explore **hypothesis testing.** Specifically, we'll be focusing on **p-values** and **one-tailed hypothesis testing.**

### To perform our first hypothesis test, we're given the following scenario:

> The director of manufacturing at a cookies company needs to determine whether a new machine is able to produce a particular type of cookies according to the manufacturer's specifications, which indicate that cookies should have a mean of 70 and standard deviation of 3.5 pounds. A sample of 49 cookies reveals a sample mean breaking strength of 69.1 pounds.

### To evaluate the data in this scenario, we can address the following tasks: <br />
**A.** State the null and alternative hypothesis <br />
**B.** Is there evidence that the machine is not meeting the manufacturer's specifications for average strength? Use a 0.05 level of significance <br />
**C.** Compute the p value and interpret its meaning <br />
**D.** What would be your answer in (B) if the standard deviation were specified as 1.75 pounds? <br />
**E.** What would be your answer in (B) if the sample mean were 69 pounds and the standard deviation is 3.5 pounds? <br />

Phenomenal. So, what are the null and alternative hypotheses and what are they talking about?

**A.** The **null hypothesis** is our original, starting hypothesis or "idea." You can think of "null" sort of like nothing, because we haven't changed anything or presented anything new yet. The **alternative hypothesis** is what we're looking to test against our original hypothesis to see which is correct. Seems straightforward, right? <br />
In this case: <br />
The null hypothesis is: the machineis producing cookies with an average weight equal to the manufacturer's specification (the circumstances we started with) <br />
The alternative hypothesis is: the machine is not producing ocokies according to the specification (the circumstances we're going to test for) <br /> 

