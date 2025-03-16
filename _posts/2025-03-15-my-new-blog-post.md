# Principles of Design and Multivariate Analysis Visualization with Tableau

Relationships between different variables in your data can often be complex. It follows that sometimes figuring out how to visualize those relationships quickly and concisely can be a challenge. Circumstances can differ drastically, so there isn't one best solution, but one rule to follow is that the simplest approach is often the best *(and you will hear me say that often.)*

That said, when creating any visualization, there are a few basic **principles of design** you can keep in mind to incorporate into your work:

1. **Alignment** - Creates an "invisible connection" or continuity between elements that are not close to each other.
2. **Repetition** - colors, shapes, fonts, textures, and other stylistic choices can appear frequently to create association and consistency.
3. **Contrast** - using opposite elements (like big or small shapes, thick or thin lines, bright or dark colors, etc.) to highlight or emphasize something.
4. **Proximity** - grouping similar elements together helps to create a sense of a relationship or focal point.
5. **Balance** - balance can be symmetrical or asymmetrical, but it doesn't have to mean "same."

~~*Wow, it's just like being back in art school again! I knew I picked the right field.*~~

Lucky for us, modern technology comes with a lot of these design principles already baked in.

This time, I'll be working with a [popular, public dataset from the historic Titanic disaster](https://www.kaggle.com/competitions/titanic/data) to demonstrate the harmony of simplicity and design in a multivariate analysis. A multivariate analysis is often a good way to visualize outcomes of complex relationships within datasets involving multiple variables.


## Creating a Multivariate Analysis Using Tableau

Lately, I've spent a lot of time with `R`, but I enjoy challenging myself with different platforms and technologies, so I've chosen to complete this activity using Tableau Public *(and to keep my SQL polished.)*

Opening the data in Excel reveals a dataset with 12 columns and 892 rows, which are labeled as follows:
```
# Passenger number
Passenger

# Survival status with a value of 0 or 1
Survived

# Passenger class with a value of 1, 2, or 3
Pclass

# The person's full name
Name

# The person's sex as male or female
Sex

# The numerical age of the person
Age

# Number of siblings or spouses aboard
SibSp

# Number of parents or children aboard
Parch

# Their associated ticket number
Ticket

# The amount paid for the ticket
Fare

# Their assigned cabin, if applicable
Cabin

# Their port of embarkation (Southampton, Cherbourg, or Queenstown)
Embarked

```

For my analysis, I've opted to use the existing variables: `Survived`, `Class`, `Sex`, and `Age`.

The titanic disaster happened in 1912, well over 100 years ago. It's common knowledge in the modern day that at the time of the event, women and children were given priority in a limited number of lifeboats that were tragically left under-filled. There was also disparity in the economic class of passengers who survived versus those who perished.

(Note: a commonly stated figure is that there were over 2,200 people aboard the Titanic, so this dataset represents a sample of about 892, not the total population.)

To begin **examining how these relationships are distributed** under closer inspection, I've created a basic bar chart visualization that shows all male versus all female survivors, organized by their passenger class:

<img width="428" alt="males-vs-females-by-class-titanic" src="https://github.com/user-attachments/assets/a857de69-b27f-4d83-a30a-56c6e5faee3e" />

In this case, I've used the typical color pattern of pink for females and blue for males because it's so common that it's immediately visually interpretable. *(But you may not always want to go the route of old cliches.)*

From the first glance at the graph, the majority of female survivors is evident. It's also evident that between the three groups of passenger classes the most first class females survived.

The majority of male survivors came from the third class, but this makes sense given that the third class is the largest majority represented by all passengers in the dataset. What's intriguing is that nearly as many first class men survived as third class. In other words, first class men, despite being a minority of total passengers on board, had a disproportionately higher rate of survival than the majority of third class male passengers:

<img width="367" alt="number-of-all-passengers-by-class-titanic" src="https://github.com/user-attachments/assets/0c38f279-92fd-42ea-b8ef-acf977c25ec8" />

To further put that into perspective, I've put a comparison of survivors versus perished per class next to each other:

<img width="553" alt="survived-vs-perished-per-class" src="https://github.com/user-attachments/assets/433d9e68-280b-4f48-b482-e6414ccff450" />

These findings reflect the commonly held knowledge about the Titanic disaster. They also provide a general overview of how passengers fared in each category.

## Evaluating more specific research questions:

But I'm going to zoom in more and evaluate if and how outcomes differed for the children aboard versus the adults. (To do this, I'll be creating some additional calculated fields.) Naturally, adults represented the majority of passengers on board, and in this dataset, children represent a small minority of just 113 individuals:

<img width="312" alt="total-adults-vs-total-children-titanic" src="https://github.com/user-attachments/assets/a40e600f-b912-4732-86b3-d899eacef2f1" />

What I'd like to find out is if there is any major disparity in class or gender among the children on board from this dataset. So keeping with the theme of bar graphs and presentation colors, I created another visualization to compare male versus female survival rates per each class:

<img width="442" alt="gender-and-class-of-child-survivors" src="https://github.com/user-attachments/assets/fb07bca7-c608-4b43-8b3e-71f359843df9" />

From the graph, it seems there were more female child survivors than male. It also seems that the lower the passenger class, the more likely a female child was to survive. It is most probable that this reflects the overall distribution of the data, with more passengers in general being from the third class.

Checking the distribution of those who perished, these assumptions seem to follow:

<img width="461" alt="children-perished-per-class-and-gender-titanic" src="https://github.com/user-attachments/assets/961b857a-0a1c-4d41-9ecb-c7d66652ce87" />

Interestingly, it seems that zero male children from the first class and zero female children from the second class perished based on the data in this dataset.

But in order to verify if female children were likely given priority over male children in lifeboats, we'd need to see how this distribution compares to the total overall distribution of children. (For example, were there more boys than girls on board?)

Creating a visualization to see the distribution of all boys versus all girls on board, it seems that the answer is unfortunate:

<img width="355" alt="gender-of-total-children-titanic" src="https://github.com/user-attachments/assets/72ae144a-b8d0-4577-9e7c-9e01ca43c3f6" />

Boys and girls are almost equally distributed, with there being just 3 more total boys than girls in the dataset. But significantly more female children survived than male children. This indicates that priority was given to women and female children, and men and male children were left behind.

## The Concluding Analysis

Comparing the numbers we've observed overall, I've created two final visualizations that show survival rates for adults versus children per class, and adults versus children per class grouped by gender:

<img width="480" alt="titanic-survivors-vs-perished-by-age-class" src="https://github.com/user-attachments/assets/3a4c3fc4-ac81-4fa7-8a66-e9171588fea3" />

<img width="488" alt="titanic-survivors-vs-perished-by-age-gender-class" src="https://github.com/user-attachments/assets/96549fc6-0b54-4db7-bef8-529d57dbbb40" />

In the first visualization, we can see that the majority of Titanic casualties were in third class. This checks out given that the majority of passengers were in third class and other circumstances gave preference to passengers in higher classes.  Among children, the majority survived, but only by a margin of about 9 individuals. About half of the children still did not survive.

Looking at the second visualization, it confirms that the group that experienced the most casualties was in third class men. This also checks out given that most men were made to stay behind. We can also see that the majority group of women who survived were women of first class. Among children, boys were the most disproportionately represented in casualties while the majority of girls survived. Looking at the distribution and context of data, this seems to be somewhat intentional.

Presented this way, keeping up with the theme of bar charts and specific color coordination to represent different variables, I've tried to apply some of the basic design principles discussed earlier to make this information more digestible. Visualizations don't always need to be exciting or different. Sometimes a simple, clear approach gets the message across, and at the end of the day - that's the point.

## Final thoughts

Thinking about the horrible disaster of the Titanic and the many preventable casualties there, including those of young children, is not an enjoyable undertaking. However, if we don't think about it then we can't learn from it.

I'm reminded that every day, all over the world, there are researchers working hard to analyze all kinds of information that many of us have the luxury of living without thinking about. I'm grateful to the people who are doing the dirty work that keeps the rest of us safe.

As an aspiring data scientist (as well as a person,) I will always prefer an unfortuante truth to a comfortable fallacy.

*(This post is dedicated to my best friend of 16 years who has been a lifelong Titanic fanatic. Hi, Kendrix!)*
