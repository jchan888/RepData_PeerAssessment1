#Reproducible Research: Peer Assessment 1

##Introduction

It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit, Nike Fuelband, or Jawbone Up. These type of devices are part of the "quantified self" movement - a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

##Data

The data for this assignment can be downloaded from the course web site:

* Dataset: [Activity monitoring data](https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip) [52K]

The variables included in this dataset are:

* steps: Number of steps taking in a 5-minute interval (missing values are coded as NA)

* date: The date on which the measurement was taken in YYYY-MM-DD format

* interval: Identifier for the 5-minute interval in which measurement was taken

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.

##Assignment

This assignment will be described in multiple parts. You will need to write a report that answers the questions detailed below. Ultimately, you will need to complete the entire assignment in a single R markdown document that can be processed by knitr and be transformed into an HTML file.

Throughout your report make sure you always include the code that you used to generate the output you present. When writing code chunks in the R markdown document, always use echo = TRUE so that someone else will be able to read the code. This assignment will be evaluated via peer assessment so it is essential that your peer evaluators be able to review the code for your analysis.



For the plotting aspects of this assignment, feel free to use any plotting system in R (i.e., base, lattice, ggplot2)

Fork/clone the [GitHub repository created for this assignment](http://github.com/rdpeng/RepData_PeerAssessment1). You will submit this assignment by pushing your completed files into your forked repository on GitHub. The assignment submission will consist of the URL to your GitHub repository and the SHA-1 commit ID for your repository state.

NOTE: The GitHub repository also contains the dataset for the assignment so you do not have to download the data separately.

###Loading and preprocessing the data

Show any code that is needed to

1. Load the data (i.e. read.csv())

2. Process/transform the data (if necessary) into a format suitable for your analysis


```r
activity <- read.csv("activity.csv", header=TRUE, sep=",", na.strings="NA")
```

```
## Warning in file(file, "rt"): cannot open file 'activity.csv': No such file
## or directory
```

```
## Error in file(file, "rt"): cannot open the connection
```

```r
activity$interval <- factor(activity$interval)
```

```
## Error in factor(activity$interval): object 'activity' not found
```

###What is mean total number of steps taken per day?

For this part of the assignment, you can ignore the missing values in the dataset.

1. Calculate the total number of steps taken per day


```r
total_steps_byday <- aggregate(steps ~ date, data=activity, sum, na.rm=TRUE)
```

```
## Error in eval(expr, envir, enclos): object 'activity' not found
```

```r
total_steps_byday$steps <- as.numeric(total_steps_byday$steps)
```

```
## Error in eval(expr, envir, enclos): object 'total_steps_byday' not found
```

2. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day


```r
hist(total_steps_byday$steps, xlab="Total steps/day", main="Total no. of steps per day")
```

```
## Error in hist(total_steps_byday$steps, xlab = "Total steps/day", main = "Total no. of steps per day"): object 'total_steps_byday' not found
```

3. Calculate and report the mean and median of the total number of steps taken per day


```r
mean_steps <- mean(total_steps_byday$steps, na.rm=TRUE)
```

```
## Error in mean(total_steps_byday$steps, na.rm = TRUE): object 'total_steps_byday' not found
```

```r
median_steps <- median(total_steps_byday$steps, na.rm=TRUE)
```

```
## Error in median(total_steps_byday$steps, na.rm = TRUE): object 'total_steps_byday' not found
```

* *The mean number of steps taken per day is as follows:*

```r
print(mean_steps)
```

```
## Error in print(mean_steps): object 'mean_steps' not found
```
* *The median number of steps taken per day is as follows:.*

```r
print(median_steps)
```

```
## Error in print(median_steps): object 'median_steps' not found
```

###What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
mean_steps_byinterval <- aggregate(steps ~ interval, data=activity, mean, na.rm=TRUE)
```

```
## Error in eval(expr, envir, enclos): object 'activity' not found
```

```r
plot(mean_steps_byinterval$interval, mean_steps_byinterval$steps, type="l", xlab="5-minute Interval", ylab="Average Number of Steps", main="Time series plot of average number of steps taken")
```

```
## Error in plot(mean_steps_byinterval$interval, mean_steps_byinterval$steps, : object 'mean_steps_byinterval' not found
```

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
max_steps_byinterval <- max(mean_steps_byinterval$steps)
```

```
## Error in eval(expr, envir, enclos): object 'mean_steps_byinterval' not found
```

```r
interval_max_steps <- mean_steps_byinterval[which.max(mean_steps_byinterval$steps),]$interval
```

```
## Error in eval(expr, envir, enclos): object 'mean_steps_byinterval' not found
```

* *The maximum number of steps is as follows:.*

```r
print(max_steps_byinterval)
```

```
## Error in print(max_steps_byinterval): object 'max_steps_byinterval' not found
```

* *The 5-minute interval with the maximum number of steps is as follows:.*

```r
print(interval_max_steps)
```

```
## Error in print(interval_max_steps): object 'interval_max_steps' not found
```

###Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)


```r
na_steps <- sum(is.na(as.character(activity$steps)))
```

```
## Error in eval(expr, envir, enclos): object 'activity' not found
```

```r
na_date <- sum(is.na(as.character(activity$date)))
```

```
## Error in eval(expr, envir, enclos): object 'activity' not found
```

```r
na_interval <- sum(is.na(as.character(activity$interval)))
```

```
## Error in eval(expr, envir, enclos): object 'activity' not found
```

```r
total_na <- na_steps+na_date+na_interval
```

```
## Error in eval(expr, envir, enclos): object 'na_steps' not found
```

* *The total number of missing values is as follows:.*

```r
print(total_na)
```

```
## Error in print(total_na): object 'total_na' not found
```

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

* *Missing values are replaced by the mean of every corresponding 5-minute interval.*

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.


```r
activity_no_na <- activity
```

```
## Error in eval(expr, envir, enclos): object 'activity' not found
```

```r
mean_steps_byinterval_ <- mean_steps_byinterval
```

```
## Error in eval(expr, envir, enclos): object 'mean_steps_byinterval' not found
```

```r
mean_steps_byinterval_$ave_steps <- mean_steps_byinterval_$steps
```

```
## Error in eval(expr, envir, enclos): object 'mean_steps_byinterval_' not found
```

```r
dropvars <- names(mean_steps_byinterval_) %in% c("steps") 
```

```
## Error in match(x, table, nomatch = 0L): object 'mean_steps_byinterval_' not found
```

```r
mean_steps_byinterval_ <- mean_steps_byinterval_[!dropvars]
```

```
## Error in eval(expr, envir, enclos): object 'mean_steps_byinterval_' not found
```

```r
activity_no_na <- merge(activity_no_na,mean_steps_byinterval_,by="interval")
```

```
## Error in merge(activity_no_na, mean_steps_byinterval_, by = "interval"): object 'activity_no_na' not found
```

```r
activity_no_na$steps <- ifelse(is.na(activity_no_na$steps), activity_no_na$ave_steps, activity_no_na$steps)
```

```
## Error in ifelse(is.na(activity_no_na$steps), activity_no_na$ave_steps, : object 'activity_no_na' not found
```

```r
activity_no_na <- activity_no_na[order(activity_no_na$date, activity_no_na$interval),]
```

```
## Error in eval(expr, envir, enclos): object 'activity_no_na' not found
```

```r
dropvars <- names(activity_no_na) %in% c("ave_steps") 
```

```
## Error in match(x, table, nomatch = 0L): object 'activity_no_na' not found
```

```r
activity_no_na <- activity_no_na[!dropvars]
```

```
## Error in eval(expr, envir, enclos): object 'activity_no_na' not found
```

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


```r
total_steps_byday_no_na <- aggregate(steps ~ date, data = activity_no_na, sum)
```

```
## Error in eval(expr, envir, enclos): object 'activity_no_na' not found
```

```r
hist(total_steps_byday_no_na$steps, xlab="Total steps/day", main="Total no. of steps per day")
```

```
## Error in hist(total_steps_byday_no_na$steps, xlab = "Total steps/day", : object 'total_steps_byday_no_na' not found
```

```r
mean_steps_no_na <- mean(total_steps_byday_no_na$steps)
```

```
## Error in mean(total_steps_byday_no_na$steps): object 'total_steps_byday_no_na' not found
```

```r
median_steps_no_na <- median(total_steps_byday_no_na$steps)
```

```
## Error in median(total_steps_byday_no_na$steps): object 'total_steps_byday_no_na' not found
```

* *The mean total number of steps taken per day is as follows:.*

```r
print(mean_steps_no_na)
```

```
## Error in print(mean_steps_no_na): object 'mean_steps_no_na' not found
```

* *The median total number of steps taken per day is as follows:.*

```r
print(median_steps_no_na)
```

```
## Error in print(median_steps_no_na): object 'median_steps_no_na' not found
```
* *It is observed that the mean and median for the complete dataset are identical, while the mean is identical with the mean of the dataset from the first assignment.*


###Are there differences in activity patterns between weekdays and weekends?

For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.


```r
activity_no_na$weekday <- weekdays(as.Date(activity_no_na$date))
```

```
## Error in as.Date(activity_no_na$date): object 'activity_no_na' not found
```

```r
activity_no_na$weekday <- ifelse(activity_no_na$weekday %in% c("Saturday", "Sunday"), c("weekend"), c("weekday"))
```

```
## Error in match(x, table, nomatch = 0L): object 'activity_no_na' not found
```

```r
activity_no_na$weekday <- factor(activity_no_na$weekday)
```

```
## Error in factor(activity_no_na$weekday): object 'activity_no_na' not found
```

```r
mean_steps_byweekday <- aggregate(activity_no_na$steps, by=list(weekday=activity_no_na$weekday,interval=activity_no_na$interval), mean, na.rm=TRUE)
```

```
## Error in aggregate(activity_no_na$steps, by = list(weekday = activity_no_na$weekday, : object 'activity_no_na' not found
```

```r
colnames(mean_steps_byweekday)[which(names(mean_steps_byweekday) == "x")] <- "steps"
```

```
## Error in colnames(mean_steps_byweekday)[which(names(mean_steps_byweekday) == : object 'mean_steps_byweekday' not found
```

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.


```r
library(lattice)
```

```
## Warning: package 'lattice' was built under R version 3.2.2
```

```r
xyplot(steps ~  interval | weekday, data = mean_steps_byweekday, layout = c(1,2), type ="l", xlab="5-minute Interval", ylab="Number of steps", main="Time series plot")
```

```
## Error in eval(substitute(groups), data, environment(x)): object 'mean_steps_byweekday' not found
```


