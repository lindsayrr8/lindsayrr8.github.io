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
ggplot(data, aes(x=month, y=charge, color=as.factor(year), group=year)) + 
  # Line connecting the points
  geom_line() +   
  # Points for each data point
  geom_point() +  
  labs(title="Student Credit Card Charges Over Time", 
       x="Month", 
       y="Charge Amount ($)", 
       # Setting the legend title on the right to "Year"
       color="Year") +   
  # Rotate month labels for clarity
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +  
  # Label bottom with month names
  scale_x_discrete(labels=months) 
```
In English, this tells `R`: <br />
With `ggplot()`, use the data frame `data` with the specified `aes` ("aesthetic mapping", aka, things like position and color.) It tells `R` to put the year and month information on the 'x' axis. `y=charge` means that the credit card charges will be plotted on the 'y' axis. `color=as.factor(year)` simply colors the lines by the year variable (being 2012 or 2013), making it easier for a human to read the graph. The `as.factor(year)` part keeps the years as categories (factors) instead of numbers for doing arithmetic on, since that's not what we want in this case.

`geom_line()` tells `ggplot()` to plot the data as a line graph, and `geom_point() +` tells `ggplot()` to add points to the line graph. `labs()` is just setting the labels for what we've plotted, as described above. We're also using `theme()` to customize how the plot appears. In this case, we're rotating the axis labels by 45 degrees so they don't overlap and adjusting their horizontal alignment to the right with `hjust = 1`. `scale_x_discrete(labels=...)` is also customizing the labels on the 'x' axis.

When we run our code, we get the finished graph as our output:
![studentcreditcardchargesovertime](https://github.com/user-attachments/assets/cdb995bf-5ab1-4907-937d-23cecc3a7071)

It looks like the data follows a bit of a trend or seasonality. In both 2012 and 2013, spending spikes in March, tanks dramatically in April, creeps up to June, then dips again in August, before finally reaching a peak again in October.

# Exponential smoothing model:
## b. 
We are instructed to employ an **exponential smoothing model** to the same data we've been working with from above. 
To do that, we will need the `forecast` package so we can use the `forecast()` function:
```R
# Install 'forecast' if not already installed
install.packages("forecast")
# Load the forecast package
library(forecast)
```
Once that's done, we can use the `ts()` (time series) function to create a time series object from our data.
## Wait, why?
Wasn't what we just made in step 'a.' a time series? Well, "yesn't."

In step 'a.', our data was "shaped" like a time series is, but as far as `R` was concerned, it was just any old data frame. In order to get `R` to recognize and apply certain attributes or behaviors to our data as a time series, we need to explicitly tell `R` that it is one. In other words, in `R`, a time series is a specific type of object that is explicitly classed as one.

Let's convert what we've got:
```R
# Convert data into a time series object for 2012 and 2013
charges_ts <- ts(c(charges_2012, charges_2013), start=c(2012, 1), frequency=12)

# Print the time series object to check
print(charges_ts)
```
And our output looks similar, if a little different:
```R
> # Print the time series object to check
> print(charges_ts)
      Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec
2012 31.9 27.0 31.3 31.0 39.4 40.7 42.3 49.5 45.0 50.0 50.9 58.5
2013 39.4 36.2 40.5 44.6 46.8 44.7 52.2 54.0 48.8 55.8 58.7 63.4
```
That wasn't too bad. It's important to note that we need to do this in order to use certain functions associated with time series correctly.

*Speaking of which...*

## Allow me to introduce you to the `HoltWinters()` function.

What's that, you ask? Why, the names "Holt" & "Winters" refer to the **"Holt-Winters smoothing model," which is used with time series data.** It's a model that **forecasts** future data points by exponentially "smoothing" past data observations. An HW model takes into account **patterns like trends and seasonality** in your data. These two Holt and Winters fellows came up with it in the 1960's. 

So, let's use it on our data:
```R
# Apply Holt-Winters model
hw_model <- HoltWinters(charges_ts)

# Print the model summary
summary(hw_model)
```
In this case, the HW model is a good fit for evaluating our data since it seems to follow a trend or seasonality. You can tweak `HoltWinters()`'s arguments further to adjust for varying specifications, but for this simple exercise we're working with just the default configurations.

Running the code gives the results we got:
```R
> # Print the model summary
> summary(hw_model)
             Length Class  Mode     
fitted       48     mts    numeric  
x            24     ts     numeric  
alpha         1     -none- numeric  
beta          1     -none- numeric  
gamma         1     -none- numeric  
coefficients 14     -none- numeric  
seasonal      1     -none- character
SSE           1     -none- numeric  
call          2     -none- call 
```
## Interpreting these results:
A few of the highlights from what we're looking at here:
- Alpha (α): Controls the level of the time series. A high alpha value means the model is more sensitive to recent data, and a low alpha means the model "smooths" out the data more.
- Beta (β): Controls the trend (how the data is increasing or decreasing over time.)
- Gamma (γ): Controls the seasonality (the repeating patterns in the data, such as the spikes in March or October.)
- SSE is the difference between the observed data and the model's predictions. Since our SSE is small (compared to the values in our data), that means the model we have is doing a good job of fitting the historical data.
- All of these values are given as 1, meaning the model is using optimal values for these parameters.

Wonderful. Now we can use `forecast()` and `plot()` to make a prediction about future student credit card charges based on past trends:
```R
# Plot the forecast based on Holt-Winters model
forecasted_values <- forecast(hw_model)
plot(forecasted_values)
```
And our plot output looks like:
![forecastsfromholtwinters](https://github.com/user-attachments/assets/79054891-5472-42ae-b7b0-4541851032d3)

## Interpreting these results:
It looks like the model expects the data to continue trending upward in the same seasonal pattern through 2016. An upward trend does seem to be a reasonable prediction based on the increasing spending metrics from 2012 to 2013.

However, as always, it's important to note that while statistics can capture a lot, it can't capture everything. There are always certain assumptions you have to make (such as in this case where the model assumes the trend will continue to follow a seasonal pattern based on 2 years of prior data.) You can't always account for hidden variables and you certainly can't flawlessly predict the future. That would be fortunte telling, not statistics!

