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
<br>$P(A \mid B)$ $=$ 	$\frac{30}{90}$ $=$ 	$\frac{1}{3}$<br />
We can write this result as a decimal or a percent. The value is the same: ~0.33 or ~33%.

**2.** Event B refers to the column labeled "B." The total for this colum is: 10 + 20 = 30. Therefore, **the probability of Event B is:**
<br>$P(A \mid B)$ $=$ 	$\frac{30}{90}$ $=$ 	$\frac{1}{3}$<br />
Again, this can be written in either form as shown above in number 1.

It looks like the probabilities of Event A and Event B are independently equal!

**3.** But what about **the probability of either Event A *or* Event B?** To calculate $P(A \mid B)$, we need to find the sum of the probability of A *and* B, but subtract the quantity where they overlap to avoid factoring it into our calculations twice.
<br> *(Remember, we want to find the probability of A **or** B, not A **and** B, because we're not calculating if they will happen at the same time in this case. We're interested in the probability of either occuring separately.)* <br />
<br> Therefore, we can use the formula:<br />
$P(A \text{ or } B)$ $=$ $P(A)+P(B)-$ $P(A \text{ and } B)$

From the table, we can fill in:
$P(A \text{ and } B)$ $=$ $\frac{10}{90}$

And remember to omit this from our final results:

$P(A \text{ or } B)$ $=$ $\frac{30}{90}$ $+$ $\frac{30}{90}$ $-$ $\frac{10}{90}$ $=$ $0.555$

Therefore, the probability of either Event A or Event B is ~0.55 or about ~55%.

**4.** As we just demonstrated in number 3, $P(A \text{ or } B)$ $=$ $P(A) + P(B)$ is **False** because it does not subtract the overlap of $P(A \text{ and } B)$.


# Now onto next: Bayes' Theorem
What is it and why is it useful? **Bayes' Theorem** is essentially a way to update our beliefs about something based on new evidence we find. It combines our prior knowledge (how likely we think something is before seeing new data) with new information to get a revised probability.

**Simply put, Bayes' Theorem says:**

$Posterior = \frac{Likelihood \times Prior}{Evidence}$

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

With these possible events in mind, we can transform this information into **variables that R can handle** so it can perform calculations on potential outcomes for us.

Laying out these variables in English looks something like this:
- **P(A1)** = $\frac{5}{365}$ = 0.0136985 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(It rains 5 days out of the year.)*
- **P(A2)** = $\frac{360}{365}$ = 0.9863014 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(It does not rain 360 days out of the year.)*
- **P(B|A1)** = 0.9 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(When it rains, the weatherman predicts rain 90% of the time.)*
- **P(B|A2)** = 0.1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *(When it does not rain, the weatherman predicts rain 10% of the time.)*

Of these outcomes, we want to know $P(A1|B)$, the probability that it will rain on the day of Jane's wedding, given that there is a forecast for rain by the weatherman.

One approach we could use is to write this out as a fraction in the form of Bayes' Theorem, as you can see below:
$$
P(A_1 | B) = \frac{P(A_1) \cdot P(B | A_1)}{P(A_1) \cdot P(B | A_1) + P(A_2) \cdot P(B | A_2)}
$$

But hold off with your abacus and mechanical calculator for a sec. That formula is a little impractical and hard for a human to read. As a programmer and an aspiring data scientist, I'd prefer to ✨ **let R handle everything.** ✨ So instead, we'll head over to RStudio and start declaring some variables:

