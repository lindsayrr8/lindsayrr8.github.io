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

### To try applying Bayes' Theorem, we're given the following scenario:
> Jane is getting married tomorrow at an outdoor ceremony in the desert. In recent years, it has rained only 5 days each year. Unfortunately, the weatherman has predicted rain for tomorrow. When it actually rains, the weatherman correctly forecasts rain 90% of the time. When it doesn't rain, he incorrectly forecasts rain 10% of the time.


