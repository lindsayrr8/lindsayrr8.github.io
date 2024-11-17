# Time Series in R

This week, we'll be covering an introduction to **time series** in `R`. Time series have to do with data obtained at regular time intervals of some sort.

To start analyzing time series, we're given the following prompt:
> **Question 1** <br />
> *The table below represents charges for a student credit card.* <br />
> **a.** Construct a time series plot using R. <br />
> **b.** Employ Exponential Smoothing Model as outline in Avril VoghlanLinks to an external site.'s notes and report the statistical  outcome <br />
> **c.** Provide a discussion on time series and Exponential Smoothing Model result you led to. <br />
> 
| Month	| 2012 | 2013 |
|-------|------|------|
| Jan	  | 31.9 | 39.4 |
| Feb	  | 27   | 36.2 |
| March	| 31.3 | 40.5 |
| Apr	  |	44.6 | 44.6 |
| May	  | 39.4 | 46.8 |
| Jun	  | 40.7 | 44.7 |
| Jul	  | 42.3 | 52.2 |
| Aug	  | 49.5 |	54  |
| Sep	  | 45   | 48.8 |
| Oct	  | 50	 | 55.8 |
| Nov	  | 50.9 | 58.7 |
| Dec	  | 58.5 | 63.4 |

## Constructing a time series plot with R:
## a.
To start, we'll take this data and convert it to a format that `R` can understand. And since we'll be plotting this data, we'll also load in `ggplot2`:
```R
# Load ggplot2 for plotting
library(ggplot2)

# Add data to vectors
months <- c('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec')
charges_2012 <- c(31.9, 27, 31.3, 31, 39.4, 40.7, 42.3, 49.5, 45, 50, 50.9, 58.5)
charges_2013 <- c(39.4, 36.2, 40.5, 44.6, 46.8, 44.7, 52.2, 54, 48.8, 55.8, 58.7, 63.4)
# Add vectors to the data frame with relevant labels
data <- data.frame(month=rep(months, 2),
                   year=rep(c(2012, 2013), each=12),
                   charge=c(charges_2012, charges_2013))

# Initial look at the data frame
head(data)
```
Running `head(data)` gives us a glimpse at the data frame we've just created, which gives the following output:
```R
> # Initial look at the data frame
> head(data)
  month year charge
1   Jan 2012   31.9
2   Feb 2012   27.0
3   Mar 2012   31.3
4   Apr 2012   31.0
5   May 2012   39.4
6   Jun 2012   40.7
```
Nice. Looks good so far. Specific data points are still associated with a certain month and year, as in our original data format. We're ready to start plotting.

## Plotting with ggplot()
Thankfully, using the function `ggplot()` will handle the bulk of the work for plotting our data. We simply need to set it up with a few specifications as our arguments:
```R
# Plotting the time series
ggplot(data, aes(x=interaction(year, month), y=charge, color=as.factor(year))) +
  geom_line() +
  geom_point() +
  labs(title="Student Credit Card Charges Over Time", x="Month-Year", y="Charge Amount ($)") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  scale_x_discrete(labels=interaction(rep(c(2012, 2013), each=12), months))
```
In English, this tells `R`: with `ggplot()`, use the data frame `data` with the specified `aes` ("aesthetic mapping", aka, things like position and color.) It tells `R` to put the year and month information on the 'x' axis. `y=charge` means that the credit card charges will be plotted on the 'y' axis. `color=as.factor(year)` simply colors the lines by the year variable (being 2012 or 2013), making it easier for a human to read the graph. The `as.factor(year)` part keeps the years as categories (factors) instead of numbers for doing arithmetic on, since that's not what we want in this case.

`geom_line()` tells `ggplot()` to plot the data as a line graph, and `geom_point() +` tells `ggplot()` to add points to the line graph. `labs()` is just setting the labels for what we've plotted, as described above. We're also using `theme()` to customize how the plot appears. In this case, we're rotating the axis labels by 45 degrees so they don't overlap and adjusting their horizontal alignment to the right with `hjust = 1`.

`scale_x_discrete(labels=...)` is also customizing the labels on the 'x' axis. The `rep(c(2012, 2013), each=12)` part repeats each year 12 times for both 2012 and 2013, ensuring there's a pair for every month. `interaction(...)` combines each year with the corresponding month to form the correct labels. *(Remember, you've really got to spell every single detail out in order for a computer to follow instructions!)*

