# Tufte Principles of Data Presentation with ggplot2 and lattice

This week, I explored two different approaches to creating a dot-dash plot in `R` using the `ggplot2` and `lattice` packages.

Naturally in this case, these charts both visualize the same data in slightly different ways. The given sample of data we'll be looking into has to do with per capita budget expenditures from 1967 to 1977.

We'll be evaluating how well each of these visualizations implement **Edward Tufte's principles of clean and minimalist data presentation.**

## A brief overview of Tufte's principles:
*(paraphrasing, of course):*

- **Beware the data-ink ratio:** Make sure your visual shows the data first and avoids unnecessary design elements.
- **Label clearly:** labels should explicitly enhance understanding of the data in a way that avoids graphical confusion.
- **Chartjunk = bad:** Does it improve the viewer's understanding of the data rather than distract or confuse? If the answer isn't a "yes," then you should probably get rid of it.
- **Layer variables sparingly:** Meaning don't dump 25 variables into one chart. Keep the number of variables in one visualization as low and as simple as possible. If many variables are involved, create a series of complimentary visualizations that show the relationships.
- **Use comparison:** Because humans think in comparative terms. An isolated figure may not tell us much, but, for example, a steeply increasing line next to a steeply decreasing line creates context with which to interpret the information.
- **Don't distort the data:** Don't be that guy. Maintain your personal integrity alongside your data integrity.

## Comparing two visual approaches:

First, I created the initial visualization using `ggplot2` as I normally would:

![ggplot2-mod-11](https://github.com/user-attachments/assets/80ea6829-9473-4671-8a9b-2695c00b6f7b)

And then I created the same visualization using `lattice` to compare:

![lattice-mod-11](https://github.com/user-attachments/assets/35238071-afc0-4722-9db4-8feb220eb4ba)



