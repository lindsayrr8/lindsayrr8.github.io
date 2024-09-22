# An Intro to Probability Theory with R

This week, we have a few different tasks ahead of us as we master the basics of **Probability Theory.**

As a quick recap:
- Probability predicts the likelihood of an event to occur.
- In Statistics, probability is represented by a value between 0 and 1.


### To begin evaluating probability, we’re given the following table:

|    |    |    |
|----|----|----|  
|    | B  | B1 |
| A  | 10 | 20 |
| A1 | 20 | 40 |

From this table, we're given the prompt:
### What is the probability of:
1. Event A
2. Event B
3. Event A or B
4. P(A or B) = P(A) + P(B)? (True or False)

To begin thinking about this problem, we should calculate the **total** number of observations in this case.
<br>Total:  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 10 + 20 + 20 + 40 = 90<br />

**1.** Event A refers to the first row of the table. If we read this row across, we find that the total for row A is 10 + 20 = 30. Therefore, **the probability of Event A is:**
<br>$$P(A \mid B) =  \frac{30}{90} = 	\frac{1}{3}$$<br />
We can write this result as a decimal or a percent. The value is the same: ~0.33 or ~33%.

**2.** Event B refers to the column labeled "B." The total for this column is: 10 + 20 = 30. Therefore, **the probability of Event B is:**
<br>$$P(A \mid B) = 	\frac{30}{90} = 	\frac{1}{3}$$<br />
Again, this can be written in either form as shown above in number 1.

It looks like the probabilities of Event A and Event B are represented in equal proportions in the total!

**3.** But what about **the probability of either Event A *or* Event B?** To calculate $$P(A \mid B)$$, we need to find the sum of the probability of A *and* B, but subtract the quantity where they overlap to avoid factoring it into our calculations twice.
<br> *(Remember, we want to find the probability of A **or** B, not A **and** B, because we're not calculating if they will happen at the same time in this case. We're interested in the probability of either occuring separately.)* <br />
<br> Therefore, we can use the formula:<br />
$$P(A \text{ or } B) = P(A)+P(B)- P(A \text{ and } B)$$

From the table, we can fill in:
$$P(A \text{ and } B) = \frac{10}{90}$$

And remember to omit this from our final results:

$$P(A \text{ or } B) = \frac{30}{90} + \frac{30}{90} - \frac{10}{90} = 0.555$$

Therefore, the probability of either Event A or Event B is ~0.55 or about ~55%.

**4.** As we just demonstrated in number 3, $P(A \text{ or } B) = $P(A) + P(B)$ is **False** because it does not subtract the overlap of $$P(A \text{ and } B)$$.


# Now onto next: Bayes' Theorem
What is it and why is it useful? **Bayes' Theorem** is essentially a way to update our beliefs about something based on new evidence we find. It combines our prior knowledge (how likely we think something is before seeing new data) with new information to get a revised probability.

**Simply put, Bayes' Theorem says:**

$$
Posterior = \frac{Likelihood \times Prior}{Evidence}
$$

With *Prior Probability* being our original belief, *Likelihood* being how likely the new evidence is if our belief was true, and *Posterior (Probability)* being our updated belief after considering the new evidence.

### To try applying Bayes' Theorem, we're given a scenario:
> "Jane is getting married tomorrow at an outdoor ceremony in the desert. In recent years, it has rained only 5 days each year. Unfortunately, the weatherman has predicted rain for tomorrow. When it actually rains, the weatherman correctly forecasts rain 90% of the time. When it doesn't rain, he incorrectly forecasts rain 10% of the time."

### What is the probability that it will rain on the day of Jane's wedding? 
The following information accompanies our scenario:
> Solution: The sample space is defined by two mutually-exclusive events: it rains or it does not rain. Additionally, a third event occurs when the weatherman predicts rain. Notation for these events appears below:
> 
> - Event A1. It rains on Jane's wedding.
> - Event A2. It does not rain on Marie's wedding.
> - Event B. The weatherman predicts rain.

Laying out these variables in English looks something like this:
- **P(A1)** = $\frac{5}{365}$ = 0.0136985 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(It rains 5 days out of the year.)*
- **P(A2)** = $\frac{360}{365}$ = 0.9863014 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(It does not rain 360 days out of the year.)*
- **P(B|A1)** = 0.9 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(When it rains, the weatherman predicts rain 90% of the time.)*
- **P(B|A2)** = 0.1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(When it does not rain, the weatherman predicts rain 10% of the time.)*

Of these outcomes, we want to know $P(A1|B)$, the probability that it will rain on the day of Jane's wedding, given that there is a forecast for rain by the weatherman.

One approach we could use is to write this out as a fraction in the form of Bayes' Theorem, as you can see below:
$P(A_1 | B) = \frac{P(A_1) \cdot P(B | A_1)}{P(A_1) \cdot P(B | A_1) + P(A_2) \cdot P(B | A_2)}$

But this formula is a little cumbersome and hard for a human to read. Instead, I humbly ask you to put away your abacus and mechanical calculator and follow my advice: **never spend an hour doing what a computer can do in a second.**

Instead, let's head over to RStudio and do the exact same thing more efficiently by **letting R handle everything for us.**

We can take the same abbreviations we used to represent each variable from above and plug those into R:

```R
# It rains 5 days out of the year.
P_A1 <- 0.0137
# It does not rain 360 days out of the year.
P_A2 <- 0.9863
# When it rains, the weatherman predicts rain 90% of the time.
P_B_given_A1 <- 0.9
# When it does not rain, the weatherman predicts rain 10% of the time.
P_B_given_A2 <- 0.1
```

Beautiful. Now we can use these to perform the calculation using Bayes' Theorem in R. We'll create a new variable called `P_A1_given_B` to assign our result to:

```R
P_A1_given_B <- (P_A1 * P_B_given_A1) / ((P_A1 * P_B_given_A1) + (P_A2 * P_B_given_A2))
```
When we run this and call the variable to print its contents to the console, the output we get is:
```R
> P_A1_given_B
[1] 0.1111211
```
...which is about ~11%. Is that really true? Even when the weatherman predicts rain, it only rains about 11% of the time? It appears that prospects for Jane's wedding are sunnier than they may seem.

### Why, though?
The explanation for this is because despite the weatherman's prediction, the overall probability of rain remains low. The prior probability of rain on any given day is actually very low (about ~1%). The weatherman's prediction itself does not significantly increase the chances of rain on the day of Jane's wedding. In other words, **prior probabilities influence the outcome** even when considering the weatherman's predictions. Therefore, Jane's 11% chance for rain and accompanying 89% chance for clear skies is **True.**

Think of it this way: your odds of being struck by lightning are something like 1 in 15,300. If you see a 100% increase in your odds for getting zapped, then you now have just a 0.01309% chance (meaning roughly zero point zero one, or less than a fraction of 1%).

## Let's see another example
From the textbook, we're asked to evaluate the following scenario:
> For a disease known to have a postoperative complication frequency of 20%, a surgeon suggests a new procedure. She/he tests it on 10 patients and found there are not complications.

**What is the probability of operating on 10 patients successfully with the traditional method?**

Okay, this problem is essentially asking us to figure out based on the given information which procedure is riskier: the old way or the new way our surgeon just tried.

Once again, I defer us to R to evaluate the numbers for this problem.

In R, we can use the `dbinom()` function *(short for "density of the binomial distribution")* to calculate a given number of successes from a series of trial runs. You can use this function to figure out the probability of successes in events with two possible outcomes.

Here's how we can start to think about the numbers we're working with so we can plug them into R:
- Number of patients: 10
- Probability of success (no complications): 80% or 0.8

Now we can simply type these **parameters** into variables for R to use:
```R
# number of patients
size <- 10 
# probability of no complications (success)
prob <- 0.8          
```
Then, it's just a matter of telling R to perform our **calculation** and to print the result:
```R
# Calculate the probability of 10 successes
result <- dbinom(10, size = size, prob = prob)
# Print the result
print(result)
```
**Tip:** You'll notice that the function `dibinom()` takes **three arguments: "x"** (the number of successes), **size** (the number of trials), and **prob** (the probability of successes on each trial.)
```
dbinom(x, size = _, prob = _)
```
Fantastic. The result we get when we run our code is:
```R
[1] 0.1073742
```

### What does it mean?
It means the likelihood of success when operating on all 10 patients using the original method of surgery is about 10.74%. In other words, there is about an ~11% chance that all 10 patients would have no complications from the surgery. This indicates that about 89% of the time, we could expect surgical complications. That's not very comforting.
```R
> dbinom(10, size = 10, prob = 0.8)
[1] 0.1073742
```
###### ~~*So that's why health informatics is the most popular concentration in my degree's department... Recruiters, email me!*~~
