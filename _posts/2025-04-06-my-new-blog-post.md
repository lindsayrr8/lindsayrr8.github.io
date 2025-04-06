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

The first ``ggplot2`` visualization maintains Tufte's principles of labelling clearly and keeping a simple, clean graph with no extras. The font used is of a serif format, which Tufte likes to use for titles.

The second `lattice` visualization also maintains Tufte's principles for clear labeling and clean presentation. In this case, a sans serif font is used for the axis labels.

## Are you serif they're any different?

Both graphs are extremely similar, but from a technical and design perspective the small differences should be intentional choices. In truth, Tufte wouldn't mind either of these visualizations based solely on his visualization principles alone.

But here's a fun fact for you: if you weren't already aware, **"serif"** refers to the little ticks or "feet" at the ends of letters, while **"sans serif"** means a font doesn't have the little ticks/feet. An example of a popular serif font is Times New Roman, and an example of a popular sans serif font is Arial.

It's not a blanket rule, but generally speaking **serif fonts are not very ADA compliant.** This means that people who have certain visual impairments and disabilities can have a harder time reading serif fonts. For this reason, sans serif fonts are generally considered more ADA compliant and therefore preferable for a wider audience.

This doesn't mean that serif fonts are "bad" or a "wrong" choice. It simply means that as a visualization professional, you should always consider whoever your audience will ultimately be when you design something to be viewed by others.

## Final thoughts

Both graphs are fine by most standards, including Tufte's, but I tend to prefer the second `lattice` visualization in this case. It seems a little more compact and "cleaner" as well as utilizing a sans serif font. This makes it a little more accommodating for a wider audience.

`ggplot2` and `lattice` are very similar `R` packages. If I had to make a comparison between them, I'd say that `ggplot2` gives you a little more control and style options, while `lattice` feels more like base `R`. At the end of the day, if you portray the data clearly and accurately, then the method you use to do so is not of the most significant importance.

