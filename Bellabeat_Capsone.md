
## Setting up my Environment

#### Loading data sets and libraries

``` r
library(tidyverse)
library(ggplot2)
activity <- read_csv("Fitabase Data 4.12.16-5.12.16/dailyActivity_merged.csv")
sleep <- read_csv("Fitabase Data 4.12.16-5.12.16/sleepDay_merged.csv")
weight <- read_csv("Fitabase Data 4.12.16-5.12.16/weightLogInfo_merged.csv")
```

## Data Exploration

First, let’s check column names and structure of data sets.

``` r
colnames(activity)
```

    ##  [1] "Id"                       "ActivityDate"            
    ##  [3] "TotalSteps"               "TotalDistance"           
    ##  [5] "TrackerDistance"          "LoggedActivitiesDistance"
    ##  [7] "VeryActiveDistance"       "ModeratelyActiveDistance"
    ##  [9] "LightActiveDistance"      "SedentaryActiveDistance" 
    ## [11] "VeryActiveMinutes"        "FairlyActiveMinutes"     
    ## [13] "LightlyActiveMinutes"     "SedentaryMinutes"        
    ## [15] "Calories"

``` r
colnames(sleep)
```

    ## [1] "Id"                 "SleepDay"           "TotalSleepRecords" 
    ## [4] "TotalMinutesAsleep" "TotalTimeInBed"

``` r
colnames(weight)
```

    ## [1] "Id"             "Date"           "WeightKg"       "WeightPounds"  
    ## [5] "Fat"            "BMI"            "IsManualReport" "LogId"

``` r
str(activity)
```

    ## spc_tbl_ [940 × 15] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ Id                      : num [1:940] 1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
    ##  $ ActivityDate            : chr [1:940] "4/12/2016" "4/13/2016" "4/14/2016" "4/15/2016" ...
    ##  $ TotalSteps              : num [1:940] 13162 10735 10460 9762 12669 ...
    ##  $ TotalDistance           : num [1:940] 8.5 6.97 6.74 6.28 8.16 ...
    ##  $ TrackerDistance         : num [1:940] 8.5 6.97 6.74 6.28 8.16 ...
    ##  $ LoggedActivitiesDistance: num [1:940] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ VeryActiveDistance      : num [1:940] 1.88 1.57 2.44 2.14 2.71 ...
    ##  $ ModeratelyActiveDistance: num [1:940] 0.55 0.69 0.4 1.26 0.41 ...
    ##  $ LightActiveDistance     : num [1:940] 6.06 4.71 3.91 2.83 5.04 ...
    ##  $ SedentaryActiveDistance : num [1:940] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ VeryActiveMinutes       : num [1:940] 25 21 30 29 36 38 42 50 28 19 ...
    ##  $ FairlyActiveMinutes     : num [1:940] 13 19 11 34 10 20 16 31 12 8 ...
    ##  $ LightlyActiveMinutes    : num [1:940] 328 217 181 209 221 164 233 264 205 211 ...
    ##  $ SedentaryMinutes        : num [1:940] 728 776 1218 726 773 ...
    ##  $ Calories                : num [1:940] 1985 1797 1776 1745 1863 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   Id = col_double(),
    ##   ..   ActivityDate = col_character(),
    ##   ..   TotalSteps = col_double(),
    ##   ..   TotalDistance = col_double(),
    ##   ..   TrackerDistance = col_double(),
    ##   ..   LoggedActivitiesDistance = col_double(),
    ##   ..   VeryActiveDistance = col_double(),
    ##   ..   ModeratelyActiveDistance = col_double(),
    ##   ..   LightActiveDistance = col_double(),
    ##   ..   SedentaryActiveDistance = col_double(),
    ##   ..   VeryActiveMinutes = col_double(),
    ##   ..   FairlyActiveMinutes = col_double(),
    ##   ..   LightlyActiveMinutes = col_double(),
    ##   ..   SedentaryMinutes = col_double(),
    ##   ..   Calories = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
str(sleep)
```

    ## spc_tbl_ [413 × 5] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ Id                : num [1:413] 1.5e+09 1.5e+09 1.5e+09 1.5e+09 1.5e+09 ...
    ##  $ SleepDay          : chr [1:413] "4/12/2016 12:00:00 AM" "4/13/2016 12:00:00 AM" "4/15/2016 12:00:00 AM" "4/16/2016 12:00:00 AM" ...
    ##  $ TotalSleepRecords : num [1:413] 1 2 1 2 1 1 1 1 1 1 ...
    ##  $ TotalMinutesAsleep: num [1:413] 327 384 412 340 700 304 360 325 361 430 ...
    ##  $ TotalTimeInBed    : num [1:413] 346 407 442 367 712 320 377 364 384 449 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   Id = col_double(),
    ##   ..   SleepDay = col_character(),
    ##   ..   TotalSleepRecords = col_double(),
    ##   ..   TotalMinutesAsleep = col_double(),
    ##   ..   TotalTimeInBed = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
str(weight)
```

    ## spc_tbl_ [67 × 8] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ Id            : num [1:67] 1.50e+09 1.50e+09 1.93e+09 2.87e+09 2.87e+09 ...
    ##  $ Date          : chr [1:67] "5/2/2016 11:59:59 PM" "5/3/2016 11:59:59 PM" "4/13/2016 1:08:52 AM" "4/21/2016 11:59:59 PM" ...
    ##  $ WeightKg      : num [1:67] 52.6 52.6 133.5 56.7 57.3 ...
    ##  $ WeightPounds  : num [1:67] 116 116 294 125 126 ...
    ##  $ Fat           : num [1:67] 22 NA NA NA NA 25 NA NA NA NA ...
    ##  $ BMI           : num [1:67] 22.6 22.6 47.5 21.5 21.7 ...
    ##  $ IsManualReport: logi [1:67] TRUE TRUE FALSE TRUE TRUE TRUE ...
    ##  $ LogId         : num [1:67] 1.46e+12 1.46e+12 1.46e+12 1.46e+12 1.46e+12 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   Id = col_double(),
    ##   ..   Date = col_character(),
    ##   ..   WeightKg = col_double(),
    ##   ..   WeightPounds = col_double(),
    ##   ..   Fat = col_double(),
    ##   ..   BMI = col_double(),
    ##   ..   IsManualReport = col_logical(),
    ##   ..   LogId = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

There are 15 columns and 940 rows in the `activity` data set. Data
contains different measurements of daily activity, as total steps,
calories burnt, total distance passed and active minutes.

`Sleep` data set has information on total minutes in bed and total
minutes asleep, as well as how many times a day a person slept. In
total, data set has 5 columns and 413 rows.

And the last one `weight` data set has 8 columns and 67 rows. There are
weights in kg and pounds and BMI index.

Let’s see how many unique Ids we have, in other words, how many people
are represented in the data sets.

``` r
cat("'Activity' data set has", length(unique(activity$Id)), "unique Ids.")
```

    ## 'Activity' data set has 33 unique Ids.

``` r
cat("'Sleep' data set has", length(unique(sleep$Id)), "unique Ids.")
```

    ## 'Sleep' data set has 24 unique Ids.

``` r
cat("'Weight' data set has", length(unique(weight$Id)), "unique Ids.")
```

    ## 'Weight' data set has 8 unique Ids.

Now, let’s see for what period data was collected.

``` r
min(activity$ActivityDate)
```

    ## [1] "4/12/2016"

``` r
max(activity$ActivityDate)
```

    ## [1] "5/9/2016"

``` r
min(sleep$SleepDay)
```

    ## [1] "4/12/2016 12:00:00 AM"

``` r
max(sleep$SleepDay)
```

    ## [1] "5/9/2016 12:00:00 AM"

``` r
min(weight$Date)
```

    ## [1] "4/12/2016 11:59:59 PM"

``` r
max(weight$Date)
```

    ## [1] "5/9/2016 6:39:44 AM"

We can see that there is data from April 12, 2016 until May 9, 2016 in
all three data sets.

And what about summary for each column.

``` r
summary(activity)
```

    ##        Id            ActivityDate         TotalSteps    TotalDistance   
    ##  Min.   :1.504e+09   Length:940         Min.   :    0   Min.   : 0.000  
    ##  1st Qu.:2.320e+09   Class :character   1st Qu.: 3790   1st Qu.: 2.620  
    ##  Median :4.445e+09   Mode  :character   Median : 7406   Median : 5.245  
    ##  Mean   :4.855e+09                      Mean   : 7638   Mean   : 5.490  
    ##  3rd Qu.:6.962e+09                      3rd Qu.:10727   3rd Qu.: 7.713  
    ##  Max.   :8.878e+09                      Max.   :36019   Max.   :28.030  
    ##  TrackerDistance  LoggedActivitiesDistance VeryActiveDistance
    ##  Min.   : 0.000   Min.   :0.0000           Min.   : 0.000    
    ##  1st Qu.: 2.620   1st Qu.:0.0000           1st Qu.: 0.000    
    ##  Median : 5.245   Median :0.0000           Median : 0.210    
    ##  Mean   : 5.475   Mean   :0.1082           Mean   : 1.503    
    ##  3rd Qu.: 7.710   3rd Qu.:0.0000           3rd Qu.: 2.053    
    ##  Max.   :28.030   Max.   :4.9421           Max.   :21.920    
    ##  ModeratelyActiveDistance LightActiveDistance SedentaryActiveDistance
    ##  Min.   :0.0000           Min.   : 0.000      Min.   :0.000000       
    ##  1st Qu.:0.0000           1st Qu.: 1.945      1st Qu.:0.000000       
    ##  Median :0.2400           Median : 3.365      Median :0.000000       
    ##  Mean   :0.5675           Mean   : 3.341      Mean   :0.001606       
    ##  3rd Qu.:0.8000           3rd Qu.: 4.782      3rd Qu.:0.000000       
    ##  Max.   :6.4800           Max.   :10.710      Max.   :0.110000       
    ##  VeryActiveMinutes FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes
    ##  Min.   :  0.00    Min.   :  0.00      Min.   :  0.0        Min.   :   0.0  
    ##  1st Qu.:  0.00    1st Qu.:  0.00      1st Qu.:127.0        1st Qu.: 729.8  
    ##  Median :  4.00    Median :  6.00      Median :199.0        Median :1057.5  
    ##  Mean   : 21.16    Mean   : 13.56      Mean   :192.8        Mean   : 991.2  
    ##  3rd Qu.: 32.00    3rd Qu.: 19.00      3rd Qu.:264.0        3rd Qu.:1229.5  
    ##  Max.   :210.00    Max.   :143.00      Max.   :518.0        Max.   :1440.0  
    ##     Calories   
    ##  Min.   :   0  
    ##  1st Qu.:1828  
    ##  Median :2134  
    ##  Mean   :2304  
    ##  3rd Qu.:2793  
    ##  Max.   :4900

``` r
summary(sleep)
```

    ##        Id              SleepDay         TotalSleepRecords TotalMinutesAsleep
    ##  Min.   :1.504e+09   Length:413         Min.   :1.000     Min.   : 58.0     
    ##  1st Qu.:3.977e+09   Class :character   1st Qu.:1.000     1st Qu.:361.0     
    ##  Median :4.703e+09   Mode  :character   Median :1.000     Median :433.0     
    ##  Mean   :5.001e+09                      Mean   :1.119     Mean   :419.5     
    ##  3rd Qu.:6.962e+09                      3rd Qu.:1.000     3rd Qu.:490.0     
    ##  Max.   :8.792e+09                      Max.   :3.000     Max.   :796.0     
    ##  TotalTimeInBed 
    ##  Min.   : 61.0  
    ##  1st Qu.:403.0  
    ##  Median :463.0  
    ##  Mean   :458.6  
    ##  3rd Qu.:526.0  
    ##  Max.   :961.0

``` r
summary(weight)
```

    ##        Id                Date              WeightKg       WeightPounds  
    ##  Min.   :1.504e+09   Length:67          Min.   : 52.60   Min.   :116.0  
    ##  1st Qu.:6.962e+09   Class :character   1st Qu.: 61.40   1st Qu.:135.4  
    ##  Median :6.962e+09   Mode  :character   Median : 62.50   Median :137.8  
    ##  Mean   :7.009e+09                      Mean   : 72.04   Mean   :158.8  
    ##  3rd Qu.:8.878e+09                      3rd Qu.: 85.05   3rd Qu.:187.5  
    ##  Max.   :8.878e+09                      Max.   :133.50   Max.   :294.3  
    ##                                                                         
    ##       Fat             BMI        IsManualReport      LogId          
    ##  Min.   :22.00   Min.   :21.45   Mode :logical   Min.   :1.460e+12  
    ##  1st Qu.:22.75   1st Qu.:23.96   FALSE:26        1st Qu.:1.461e+12  
    ##  Median :23.50   Median :24.39   TRUE :41        Median :1.462e+12  
    ##  Mean   :23.50   Mean   :25.19                   Mean   :1.462e+12  
    ##  3rd Qu.:24.25   3rd Qu.:25.56                   3rd Qu.:1.462e+12  
    ##  Max.   :25.00   Max.   :47.54                   Max.   :1.463e+12  
    ##  NA's   :65

Interesting observations:

- average steps taken: 7638
- average sedentary time: 16.5 hours
- lightly active minutes: 3.2 hours
- fairly active and very active time on average 13.5 min and 21.1 min
  accordingly
- average total time in bed: 7.6 hours
- average total time asleep: 7 hours
- maximum total time in bed: 16 hours (could be for an ill person)
- average BMI is 25.19 (healthy BMI is considered from 18.5 to 24.9)
- min and max BMI are 21 and 47 accordingly

## Limitations of Data

Reviewing this data set, I noticed two limitations. One is that it
doesn’t specify gender. We are doing this project for Bellabeat app,
which is specifically designed for women, and here we have data from
Fitbit with unknown gender. It could be all men or partially men, and
this would be a strongly biased data. For this project we should be
focused on the performance of women only. There is a
[discussion](https://www.kaggle.com/datasets/arashnic/fitbit/discussion/289024?search=women)
on Kaggle on this topic, if you want to read more.

And the second limitation is that we have records on very few people,
it’s not enough to make any conclusions about population (for example,
population of those who are using fitness trackers).

Nevertheless, I decided to keep going with this project and this data
set as it’s for educational purpose only. In statistics, there is a term
[convenience
sampling](https://www.questionpro.com/blog/convenience-sampling/). This
type of sampling is usually highly biased and shouldn’t be used, unless
only low risk circumstances are involved, like in our case. In real
world, I would search for more credible data.

## Data Cleaning

#### Fixing Formatting

The date columns are in string format. Let’s fix it. And as well, let’s
rename these columns the same.

``` r
activity$Date <- as.POSIXct(activity$ActivityDate, format = "%m/%d/%Y")
sleep$Date <- as.POSIXct(sleep$SleepDay, format = "%m/%d/%Y")
weight$Date <- as.POSIXct(weight$Date, format = "%m/%d/%Y")
```

And then drop old columns that were replaced by new ones.

``` r
sleep <- select(sleep, -SleepDay)
activity <- select(activity, -ActivityDate)
```

#### Removing Duplicates

First, let’s check if there is any duplicated row.

``` r
sum(duplicated(activity))
```

    ## [1] 0

``` r
sum(duplicated(sleep))
```

    ## [1] 3

``` r
sum(duplicated(weight))
```

    ## [1] 0

There are 3 duplicated rows in `sleep` data set. Let’s drop them.

``` r
sleep <- sleep %>%
  distinct() %>%
  drop_na()
```

#### Cleaning Null values

Let’s see if there is any null value. Function `complete.cases` counts
rows that don’t have any null values and function `nrow` counts total
amount of rows in a data set. If they return the same number, it means
there is no nulls in the data set. If the returned numbers differ,
further exploration is needed.

``` r
sum(complete.cases(activity))
```

    ## [1] 940

``` r
nrow(activity)
```

    ## [1] 940

``` r
sum(complete.cases(sleep))
```

    ## [1] 410

``` r
nrow(sleep)
```

    ## [1] 410

``` r
sum(complete.cases(weight))
```

    ## [1] 2

``` r
nrow(weight)
```

    ## [1] 67

The `weight` data set has only two complete rows out 67. Let’explore it.

``` r
head(weight)
```

    ## # A tibble: 6 × 8
    ##           Id Date                WeightKg WeightPo…¹   Fat   BMI IsMan…²   LogId
    ##        <dbl> <dttm>                 <dbl>      <dbl> <dbl> <dbl> <lgl>     <dbl>
    ## 1 1503960366 2016-05-02 00:00:00     52.6       116.    22  22.6 TRUE    1.46e12
    ## 2 1503960366 2016-05-03 00:00:00     52.6       116.    NA  22.6 TRUE    1.46e12
    ## 3 1927972279 2016-04-13 00:00:00    134.        294.    NA  47.5 FALSE   1.46e12
    ## 4 2873212765 2016-04-21 00:00:00     56.7       125.    NA  21.5 TRUE    1.46e12
    ## 5 2873212765 2016-05-12 00:00:00     57.3       126.    NA  21.7 TRUE    1.46e12
    ## 6 4319703577 2016-04-17 00:00:00     72.4       160.    25  27.5 TRUE    1.46e12
    ## # … with abbreviated variable names ¹​WeightPounds, ²​IsManualReport

It looks like the problem is with a column `Fat`. I will print all the
values from the column.

``` r
weight$Fat
```

    ##  [1] 22 NA NA NA NA 25 NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
    ## [26] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
    ## [51] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

Right, it has only two non-null values. Let’s drop this column.

``` r
weight <- select(weight, -Fat)
sum(complete.cases(weight))
```

    ## [1] 67

``` r
nrow(weight)
```

    ## [1] 67

Great, there is no more null values! We can move on to data
transformation.

## Data Transformation

#### Turning Minutes into Hours

First of all, I want to turn minutes into hours in `sleep` data set to
easier analyze it.

``` r
sleep2 <- sleep %>%
  mutate(
    TotalHoursAsleep = round(sleep$TotalMinutesAsleep / 60, 1),
    TotalHoursInBed = round(sleep$TotalTimeInBed / 60, 1)
  )

head(sleep2)
```

    ## # A tibble: 6 × 7
    ##           Id TotalSleepRec…¹ Total…² Total…³ Date                Total…⁴ Total…⁵
    ##        <dbl>           <dbl>   <dbl>   <dbl> <dttm>                <dbl>   <dbl>
    ## 1 1503960366               1     327     346 2016-04-12 00:00:00     5.4     5.8
    ## 2 1503960366               2     384     407 2016-04-13 00:00:00     6.4     6.8
    ## 3 1503960366               1     412     442 2016-04-15 00:00:00     6.9     7.4
    ## 4 1503960366               2     340     367 2016-04-16 00:00:00     5.7     6.1
    ## 5 1503960366               1     700     712 2016-04-17 00:00:00    11.7    11.9
    ## 6 1503960366               1     304     320 2016-04-19 00:00:00     5.1     5.3
    ## # … with abbreviated variable names ¹​TotalSleepRecords, ²​TotalMinutesAsleep,
    ## #   ³​TotalTimeInBed, ⁴​TotalHoursAsleep, ⁵​TotalHoursInBed

#### Merging Data

In order to visualize correlations between variable in different data
sets later, I will merge data now. As all of the data sets have
different amount of rows, merging them all together will mean loosing
huge amount of rows. So I will merge two at a time.

``` r
activity_sleep <- merge(activity, sleep, by = c("Id", "Date"))
activity_weight <- merge(activity, weight, by = c("Id", "Date"))
sleep_weight <- merge(sleep, weight, by = c('Id', 'Date'))

cat("'activity_sleep' dataset has", n_distinct(activity_sleep$Id), "unique Ids and", n_distinct(activity_sleep$Date), "unique dates.\n")
```

    ## 'activity_sleep' dataset has 24 unique Ids and 31 unique dates.

``` r
cat("'activity_weight' dataset has", n_distinct(activity_weight$Id), "unique Ids and", n_distinct(activity_weight$Date), "unique dates.\n")
```

    ## 'activity_weight' dataset has 8 unique Ids and 31 unique dates.

``` r
cat("'sleep_weight' dataset has", n_distinct(sleep_weight$Id), "unique Ids and", n_distinct(sleep_weight$Date), "unique dates")
```

    ## 'sleep_weight' dataset has 5 unique Ids and 30 unique dates

#### Creating new Table with Average Steps per Weekday

To have a table with average steps by all of the participants per each
day of a week, first, I will turn dates into days of week and then I
will calculate average number of steps.

``` r
weekday_activity <- activity %>%
  mutate(Weekday = weekdays(Date))

weekday_activity$Weekday <- ordered(weekday_activity$Weekday, levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
"Friday", "Saturday", "Sunday"))

weekday_avg_steps <- weekday_activity %>%
    group_by(Weekday) %>%
        summarize (DailySteps = mean(TotalSteps))

head(weekday_avg_steps)
```

    ## # A tibble: 6 × 2
    ##   Weekday   DailySteps
    ##   <ord>          <dbl>
    ## 1 Monday         7781.
    ## 2 Tuesday        8125.
    ## 3 Wednesday      7559.
    ## 4 Thursday       7406.
    ## 5 Friday         7448.
    ## 6 Saturday       8153.

#### Creating new Table with Average Sleep Time per Weekday

Now, I will do the same with hours asleep.

``` r
weekday_sleep <- sleep2 %>%
  mutate(Weekday = weekdays(Date))

weekday_sleep$Weekday <- ordered(weekday_sleep$Weekday, levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
"Friday", "Saturday", "Sunday"))

weekday_avg_sleep <- weekday_sleep %>%
    group_by(Weekday) %>%
        summarize(DailySleep = mean(TotalHoursAsleep))

head(weekday_avg_sleep)
```

    ## # A tibble: 6 × 2
    ##   Weekday   DailySleep
    ##   <ord>          <dbl>
    ## 1 Monday          6.99
    ## 2 Tuesday         6.75
    ## 3 Wednesday       7.24
    ## 4 Thursday        6.69
    ## 5 Friday          6.76
    ## 6 Saturday        6.99

## Data Visualization

#### Visualizing Total Steps

First of all, we will look at the distribution of number of steps taken
a day.

``` r
ggplot(data = activity) +
    geom_histogram(mapping = aes(x = TotalSteps, color = "red", fill = 'red'), 
                   binwidth = 4000, alpha = 0.8, show.legend = FALSE) +
    geom_vline(aes(xintercept=10000), linetype="dashed", color = "darkred") +
    labs(x = "daily steps", title = "Distribution of number of steps") +
    theme_classic()
```

![](case_study_files/figure-gfm/distribution%20steps-1.png)<!-- -->

Recommendation of 10,000 steps is widely known and most of the
participants in this study don’t reach it but the [latest
research](%22https://www.nbcnews.com/health/health-news/how-many-steps-day-should-you-take-study-finds-7-n1278853%22)
suggests that there is no need to walk 10,000 or more steps a day. Yes,
people gain more health benefits the more steps they took, but the
greatest statistically significant reduction in mortality risk appeared
to be between 7,000 and 10,000 steps.

Here we can see a positive correlation below 10,000, in other words,
there is more people who walk close to 10 thousand steps (e.g. 9000
steps) compared to the ones who walk 5 thousand and even more than those
who walk 2 thousand. It looks fine, but still let’s find out what
percentage of records is in the recommended range.

``` r
less_7000 <- sum(activity$TotalSteps < 7000) / length(activity$TotalSteps) * 100
between_7000_10000 <- sum(activity$TotalSteps >= 7000 & activity$TotalSteps < 10000) / length(activity$TotalSteps) * 100
more_10000 <- sum(activity$TotalSteps >= 10000) / length(activity$TotalSteps) * 100

data <- matrix(c(less_7000, between_7000_10000, more_10000), nrow=3, ncol=1)
rownames(data) <- c('Less than 7,000 steps','7,000-10,000 steps','More than 10,000 steps')
colnames(data) <- "Percentage" 
final=as.table(data)
print(final)
```

    ##                        Percentage
    ## Less than 7,000 steps    46.48936
    ## 7,000-10,000 steps       21.27660
    ## More than 10,000 steps   32.23404

``` r
activity2 <- activity %>%
    mutate(
        TotalSteps = case_when(
            activity$TotalSteps < 7000 ~ "0-7,000",
            activity$TotalSteps >= 7000 &
                activity$TotalSteps < 10000 ~ "7,000-10,000",
            activity$TotalSteps >= 10000 ~ "More than 10,000"
        ))

ggplot(data = activity2, aes(x = TotalSteps, color = TotalSteps, fill = TotalSteps)) +
    geom_bar(alpha = 0.8, show.legend = FALSE) +
    labs(x = "total steps", title = "All steps records divided into 3 groups") +
    theme_classic()
```

![](case_study_files/figure-gfm/bar%20plot-1.png)<!-- -->

Now, we can clearly see that almost half of the records are below 7,000
steps! And only 21.3% of records are between 7 and 10 thousand steps.
That definitely needs some improvement.

#### Analyzing BMI

Now, let’s move on to the body mass index. BMI is a value derived from
the mass and height of a person. According to [World Health
Organization](%22https://www.who.int/europe/news-room/fact-sheets/item/a-healthy-lifestyle---who-recommendations%22):

- If your BMI is less than 18.5, it falls within the underweight range.
- If your BMI is 18.5 to 24.9, it falls within the Healthy Weight range.
- If your BMI is 25.0 to 29.9, it falls within the overweight range.
- If your BMI is 30.0 or higher, it falls within the obese range.

``` r
ggplot(data = weight) +
    geom_histogram(mapping = aes(x = BMI, color = "red", fill = "red"), 
                   bins = 25, alpha = 0.8, show.legend = FALSE) +
    labs(title = "Distribution of Body Mass Index records") +
    theme_classic()
```

![](case_study_files/figure-gfm/histogram%20of%20bmi-1.png)<!-- -->

We have one outlier with BMI more than 40 and the rest falls into
category with index between 20 and 30. But there is one problem with
this histogram. As you might remember we have only 8 people in the
`weight` data set and the distribution shows all records by these 8
people during less than one month. It can be highly skewed by people who
record their weight often. It has very low probability that BMI of any
person can change significantly during 1 month, so we will count only
average body mass index per participant.

``` r
weight_grouped <- weight %>%
    group_by(Id) %>%
    summarise(BMI = mean(BMI))
```

Next, we will group people by category.

``` r
weight_grouped2 <- weight_grouped %>%
    mutate(
        BMI = case_when(
            weight_grouped$BMI < 18.5 ~ "Underweight",
            weight_grouped$BMI >= 18.5 &
                weight_grouped$BMI < 25 ~ "Healthy Weight",
            weight_grouped$BMI >= 25 &
                weight_grouped$BMI < 30 ~ "Overweight",
            weight_grouped$BMI >= 30 ~ "Obese"
        ))
```

And, finally, create a bar chart. I use `fct_relevel` to put categories
in the correct order and `scale_fill_manual` to change colors to more
intuitive ones (green for healthy, orange for overweight and red for
obese).

``` r
library(forcats)

ggplot(data = weight_grouped2, aes(x = fct_relevel(BMI, "Overweight", after = 1), fill = fct_relevel(BMI, "Overweight", after = 1))) +
    geom_bar(alpha = 0.7, show.legend = FALSE) +
    labs(title = "Participants categorized by Body Mass Index", x = "BMI category") +
    scale_fill_manual(values=c("darkgreen", "orange", "red")) +
    theme_classic()
```

![](case_study_files/figure-gfm/barchart%20bmi-1.png)<!-- -->

So, we can see that in our small sample we don’t have anyone in
underweight range (as you might have noticed from the distribution
above, as well), there are 3 people in healthy weight, 4 people in
overweight and 1 in obese range.

#### Visualizing Sleep Patterns

Let’s move on to analyze sleep patterns of our participants.

``` r
ggplot(data = sleep2) +
    geom_histogram(mapping = aes(x = TotalHoursAsleep, fill = 'red', color = 'red'), 
                   bins = 25, alpha = 0.8, show.legend = FALSE) +
    labs(title = "Distribution of sleep records", x = 'hours asleep') +
    theme_classic()
```

![](case_study_files/figure-gfm/histogram%20of%20sleeping-1.png)<!-- -->

Sleep records have standard normal distribution with highest frequency
in the range from 5.5 to 9 hours a day. But as well, we see disturbing
amount of records that are less than 5 hours.

According to [National Sleep Foundation
guidelines]('https://pubmed.ncbi.nlm.nih.gov/29073412/') healthy adults
need between 7 and 9 hours of sleep per night. Babies, young children,
and teens need even more sleep to enable their growth and development.
People over 65 should also get 7 to 8 hours per night.

I will calculate average amount of sleep per participant and divide them
into categories, according to National Sleep Foundation guidelines. And
let’s suppose that we have only adults younger than 65 in our study.

``` r
sleep_grouped <- sleep2 %>%
    group_by(Id) %>%
    summarise(AveHoursAsleep = mean(TotalHoursAsleep))
```

``` r
sleep_grouped2 <- sleep_grouped %>%
    mutate(
        AverageHoursAsleep = case_when(
            sleep_grouped$AveHoursAsleep < 7 ~ "Too Little",
            sleep_grouped$AveHoursAsleep  >= 7 &
                sleep_grouped$AveHoursAsleep  <= 9 ~ "Healthy Sleep",
            sleep_grouped$AveHoursAsleep  > 9 ~ "Too Much"
        ))
```

``` r
ggplot(data = sleep_grouped2, aes(x = fct_relevel(AverageHoursAsleep, "Healthy Sleep", after = 1), fill = fct_relevel(AverageHoursAsleep, "Healthy Sleep", after = 1))) +
    geom_bar(alpha = 0.8, show.legend = FALSE) +
    labs(title = "Amount of sleep each participant gets on average", x = "") +
    theme_classic()
```

![](case_study_files/figure-gfm/barchart%20sleep-1.png)<!-- -->

Most of the participants don’t sleep enough (less than 7 hours a day)
and some sleep too much (more than 9 hours a day).

#### Visualization of Steps depending on a Day of a Week

Next, I will visualize average steps taken per day of a week for
everyone in our sample together.

``` r
ggplot(weekday_avg_steps, aes(x = Weekday, y = DailySteps)) +
      geom_bar(stat = 'identity', color = '#007702', fill = "#007702", alpha = 0.7) +
      labs(title = "Average steps per weekday", x= "", y = "") +
    theme_classic()
```

![](case_study_files/figure-gfm/visualize%20steps%20per%20weekday-1.png)<!-- -->

It looks like there is slightly more activity (more steps taken) on
Tuesdays and Saturdays, while on Sundays people tend to walk less and
probably rest more.

#### Visualization of Hours Asleep depending on a Day of a Week

Now, I will do the same with hours asleep.

``` r
ggplot(weekday_avg_sleep, aes(Weekday, DailySleep)) +
      geom_bar(stat = 'identity', fill='#CD022D', color = '#CD022D', alpha = 0.7) +
      labs(title = "Average hours asleep per weekday", x= "", y = "") +
      theme_classic()
```

![](case_study_files/figure-gfm/visulize%20sleep%20per%20weekday-1.png)<!-- -->

Here we see that on Sundays and Wednesdays participants tend to sleep
more.

#### Visualizing Correlation between Calories and Total Steps

``` r
ggplot(data = activity, aes(x = TotalSteps, y = Calories)) +
  geom_point(color = '#003D30') +
  geom_smooth(method = 'loess', formula = 'y ~ x', color = '#009175') +
  labs(title = "Total steps vs calories", y = 'calories', x = 'total steps') +
  theme_classic()
```

![](case_study_files/figure-gfm/scatter%20calories%20vs%20steps-1.png)<!-- -->

There is a positive correlation, meaning that higher numbers of steps
are associated with higher amounts of calories burnt.

#### Visualizing Correlation between Sedentary Minutes and Total Minutes Asleep

``` r
ggplot(data = activity_sleep, aes(x = SedentaryMinutes, y = TotalMinutesAsleep)) +
  geom_point(color = '#00306F') +
  geom_smooth(method = 'loess', formula = 'y ~ x', color = '#005FCC') +
  labs(title = "Sedentary minutes vs total minutes asleep", x = 'sedentary minutes', y = 'minutes asleep') +
  theme_classic()
```

![](case_study_files/figure-gfm/scatter%20sedentary%20vs%20asleep-1.png)<!-- -->

Here we can see a negative correlation, meaning that more sedentary
minutes are associated with less total minutes asleep.

#### Visualizing Correlation between Time in the Bed and Time Asleep

``` r
ggplot(data = sleep, aes(x = TotalTimeInBed, y = TotalMinutesAsleep)) +
  geom_point(color = '#450270') +
  geom_smooth(method = 'loess', formula = 'y ~ x', color = '#8400CD') +
  labs(title = "Total time in bed vs total time asleep", x = 'minutes in bed', y = 'minutes asleep') +
  theme_classic()
```

![](case_study_files/figure-gfm/scatter%20in%20bed%20vs%20asleep-1.png)<!-- -->

Here, there is a pretty strong positive correlation. It makes sense.
Time you sleep is correlated with the time you spend in the bed. But
does it mean that more time spent in bed helps (in other words, causes)
you to sleep more? Unfortunately, this data is not enough to answer this
question.

## Conclusions

Recommendations for `Bellabeat` app made based on analysis of `Fitbit`
data:

- Many people walk less than 7000 steps (46.5% of our sample). So I
  recommend to put an emphasis on this number. 10 thousand might feel
  too intimidating for some people, while 7 thousand steps sounds more
  reachable and according to the latest studies, it’s enough for health
  benefits.
- Most of the users in our sample sleep too little. Providing reminders
  to go to sleep earlier could be helpful.
- For users who don’t reach their daily goals of sleep and steps, I
  recommend sending personalized emails about positive effect that
  activity makes on a sleep. But for this, more research should be done,
  as in our analysis we stated association between variables, not
  causation.
- As Sundays tend to be less active for most of the people in our
  sample, some soft motivation could be helpful. By soft motivation I
  mean let people sleep and rest on this day (as they anyway will do),
  decrease step goals but still send few reminders to go out, take
  relaxing pleasant walks and enjoy their Sunday.

### Thank you for your time!

#### Feel free to ask me anything, if you have any doubts.
