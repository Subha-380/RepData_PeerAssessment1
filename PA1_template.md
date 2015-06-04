# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
##Assumption - activity.csv file is present in the working directory

myfile <-read.csv("activity.csv",header=T)

## keeping only data with no missing values by using complete.cases
good <-complete.cases(myfile)
myfile <- myfile[good,]
```

```r
## What is mean total number of steps taken per day?
```

```r
## grouping the data by date
myfile_dates <- group_by(myfile,date)
## adding a column that gives the total steps per dayh
myfile_dates <- summarise(myfile_dates,total_steps = sum(steps))

## making a histogram of the total steps
hist(myfile_dates$total_steps,col="red",xlab="Total Steps", main = "Histogram")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

```r
## mean and median of total steps
mean_steps <- mean(myfile_dates$total_steps)
median_steps <- median(myfile_dates$total_steps)
```

```r
## What is the average daily activity pattern?
```

```r
## time series plot
## aggregating the data for steps vs interval
steps_int <- aggregate(steps ~ interval, data = myfile , mean)

## drawing the plot
plot(steps ~ interval, data = steps_int, type = "l")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

```r
## finding the max interval
steps_int[which.max(steps_int$steps),]$interval
```

```
## [1] 835
```

```r
## Imputing missing values
```


```r
## Are there differences in activity patterns between weekdays and weekends?
```


