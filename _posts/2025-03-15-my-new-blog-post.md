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

This time, I'll be working with a [free, public dataset from the historic Titanic disaster](https://www.kaggle.com/competitions/titanic/data) to demonstrate the harmony of simplicity and design in a multivariate analysis.

## Creating a Multivariate Analysis Using Tableau

Lately, I've spent a lot of time with `R`, but I enjoy challenging myself with different platforms and technologies, so I've chosen to complete this activity using Tableau Public.

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

For my analysis, I've used the existing variables: `Survived`, `Class`, `Sex`, and `Age`.






