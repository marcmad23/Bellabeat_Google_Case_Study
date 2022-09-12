#About Bellabeat

Bellabeat is a high tech manufacturer of health based products for
women, and even though small they have been quite successful. Urška
Sršen, co-founder and Chief Creative Officer of Bellabeat, knows the
company has potential to be a major player in the global smart device
market and believes that by analyzing smart device data new growth
potential can be found.

##Main Questions

1.What are some trends in smart device usage?

2.How could these trends apply to Bellabeat customers?

3.How could these trends help influence Bellabeat marketing strategy?

##Business Task

Analyze data on smart device usage on non-Bellabeat smart devices, then
use those insights to provide recommendations for Bellabeat marketing
strategy improvement.

#Data Preparation

Installed and Loaded packages that would be necesary for the preparation
and analysis of the data.

Then imported the data into R Studio, which had already been cleaned and
validated in in Sheets prior. All data was taken from a zip file
provided by Mobius on Kaggle. They provided fitbit fitness tracker data
that was to be used in this analysis.

``` r
sleepDay <- read_csv(" sleepDay.csv")
```

    ## Rows: 413 Columns: 5
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): SleepDay
    ## dbl (4): Id, TotalSleepRecords, TotalMinutesAsleep, TotalTimeInBed
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
dailyActivity <- read_csv("daily_activity.csv")
```

    ## Rows: 940 Columns: 15
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (1): ActivityDate
    ## dbl (14): Id, TotalSteps, TotalDistance, TrackerDistance, LoggedActivitiesDi...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
dailyCalories <- read_csv("dailyCalories.csv")
```

    ## Rows: 940 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): ActivityDay
    ## dbl (2): Id, Calories
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
dailyIntensities <- read_csv("dailyIntensities.csv")
```

    ## Rows: 940 Columns: 10
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): ActivityDay
    ## dbl (9): Id, SedentaryMinutes, LightlyActiveMinutes, FairlyActiveMinutes, Ve...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
dailySteps <- read_csv("dailySteps.csv")
```

    ## Rows: 940 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): ActivityDay
    ## dbl (2): Id, StepTotal
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
heartrate_seconds_merged <- read_csv("heartrate_seconds_merged.csv")
```

    ## Rows: 2483658 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Time
    ## dbl (2): Id, Value
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
hourlyCalories <- read_csv("hourlyCalories.csv")
```

    ## Rows: 22099 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): ActivityHour
    ## dbl (2): Id, Calories
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
hourlyIntensities <- read_csv("hourlyIntensities.csv")
```

    ## Rows: 22099 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): ActivityHour
    ## dbl (3): Id, TotalIntensity, AverageIntensity
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
weightLogInfo <- read_csv("weightLogInfo.csv")
```

    ## Rows: 67 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Date
    ## dbl (6): Id, WeightKg, WeightPounds, Fat, BMI, LogId
    ## lgl (1): IsManualReport
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

To make sure they were imported correctly I used the head fucntion to
take a look at the csv files as dataframes

    ## # A tibble: 6 × 3
    ##           Id ActivityHour          Calories
    ##        <dbl> <chr>                    <dbl>
    ## 1 1503960366 4/12/2016 12:00:00 AM       81
    ## 2 1503960366 4/12/2016 1:00:00 AM        61
    ## 3 1503960366 4/12/2016 2:00:00 AM        59
    ## 4 1503960366 4/12/2016 3:00:00 AM        47
    ## 5 1503960366 4/12/2016 4:00:00 AM        48
    ## 6 1503960366 4/12/2016 5:00:00 AM        48

    ## # A tibble: 6 × 4
    ##           Id ActivityHour          TotalIntensity AverageIntensity
    ##        <dbl> <chr>                          <dbl>            <dbl>
    ## 1 1503960366 4/12/2016 12:00:00 AM             20            0.333
    ## 2 1503960366 4/12/2016 1:00:00 AM               8            0.133
    ## 3 1503960366 4/12/2016 2:00:00 AM               7            0.117
    ## 4 1503960366 4/12/2016 3:00:00 AM               0            0    
    ## 5 1503960366 4/12/2016 4:00:00 AM               0            0    
    ## 6 1503960366 4/12/2016 5:00:00 AM               0            0

    ## # A tibble: 6 × 15
    ##        Id ActivityDate TotalSteps TotalDistance TrackerDistance LoggedActivitie…
    ##     <dbl> <chr>             <dbl>         <dbl>           <dbl>            <dbl>
    ## 1  1.50e9 4/12/2016         13162          8.5             8.5                 0
    ## 2  1.50e9 4/13/2016         10735          6.97            6.97                0
    ## 3  1.50e9 4/14/2016         10460          6.74            6.74                0
    ## 4  1.50e9 4/15/2016          9762          6.28            6.28                0
    ## 5  1.50e9 4/16/2016         12669          8.16            8.16                0
    ## 6  1.50e9 4/17/2016          9705          6.48            6.48                0
    ## # … with 9 more variables: VeryActiveDistance <dbl>,
    ## #   ModeratelyActiveDistance <dbl>, LightActiveDistance <dbl>,
    ## #   SedentaryActiveDistance <dbl>, VeryActiveMinutes <dbl>,
    ## #   FairlyActiveMinutes <dbl>, LightlyActiveMinutes <dbl>,
    ## #   SedentaryMinutes <dbl>, Calories <dbl>

    ## # A tibble: 6 × 3
    ##           Id ActivityDay Calories
    ##        <dbl> <chr>          <dbl>
    ## 1 1503960366 4/12/2016       1985
    ## 2 1503960366 4/13/2016       1797
    ## 3 1503960366 4/14/2016       1776
    ## 4 1503960366 4/15/2016       1745
    ## 5 1503960366 4/16/2016       1863
    ## 6 1503960366 4/17/2016       1728

    ## # A tibble: 6 × 10
    ##           Id ActivityDay SedentaryMinutes LightlyActiveMinutes FairlyActiveMinu…
    ##        <dbl> <chr>                  <dbl>                <dbl>             <dbl>
    ## 1 1503960366 4/12/2016                728                  328                13
    ## 2 1503960366 4/13/2016                776                  217                19
    ## 3 1503960366 4/14/2016               1218                  181                11
    ## 4 1503960366 4/15/2016                726                  209                34
    ## 5 1503960366 4/16/2016                773                  221                10
    ## 6 1503960366 4/17/2016                539                  164                20
    ## # … with 5 more variables: VeryActiveMinutes <dbl>,
    ## #   SedentaryActiveDistance <dbl>, LightActiveDistance <dbl>,
    ## #   ModeratelyActiveDistance <dbl>, VeryActiveDistance <dbl>

    ## # A tibble: 6 × 3
    ##           Id ActivityDay StepTotal
    ##        <dbl> <chr>           <dbl>
    ## 1 1503960366 4/12/2016       13162
    ## 2 1503960366 4/13/2016       10735
    ## 3 1503960366 4/14/2016       10460
    ## 4 1503960366 4/15/2016        9762
    ## 5 1503960366 4/16/2016       12669
    ## 6 1503960366 4/17/2016        9705

    ## # A tibble: 6 × 5
    ##           Id SleepDay           TotalSleepRecor… TotalMinutesAsl… TotalTimeInBed
    ##        <dbl> <chr>                         <dbl>            <dbl>          <dbl>
    ## 1 1503960366 4/12/2016 12:00:0…                1              327            346
    ## 2 1503960366 4/13/2016 12:00:0…                2              384            407
    ## 3 1503960366 4/15/2016 12:00:0…                1              412            442
    ## 4 1503960366 4/16/2016 12:00:0…                2              340            367
    ## 5 1503960366 4/17/2016 12:00:0…                1              700            712
    ## 6 1503960366 4/19/2016 12:00:0…                1              304            320

    ## # A tibble: 6 × 3
    ##           Id Time                 Value
    ##        <dbl> <chr>                <dbl>
    ## 1 2022484408 4/12/2016 7:21:00 AM    97
    ## 2 2022484408 4/12/2016 7:21:05 AM   102
    ## 3 2022484408 4/12/2016 7:21:10 AM   105
    ## 4 2022484408 4/12/2016 7:21:20 AM   103
    ## 5 2022484408 4/12/2016 7:21:25 AM   101
    ## 6 2022484408 4/12/2016 7:22:05 AM    95

    ## # A tibble: 6 × 8
    ##           Id Date       WeightKg WeightPounds   Fat   BMI IsManualReport   LogId
    ##        <dbl> <chr>         <dbl>        <dbl> <dbl> <dbl> <lgl>            <dbl>
    ## 1 1503960366 5/2/2016 …     52.6         116.    22  22.6 TRUE           1.46e12
    ## 2 1503960366 5/3/2016 …     52.6         116.    NA  22.6 TRUE           1.46e12
    ## 3 1927972279 4/13/2016…    134.          294.    NA  47.5 FALSE          1.46e12
    ## 4 2873212765 4/21/2016…     56.7         125.    NA  21.5 TRUE           1.46e12
    ## 5 2873212765 5/12/2016…     57.3         126.    NA  21.7 TRUE           1.46e12
    ## 6 4319703577 4/17/2016…     72.4         160.    25  27.5 TRUE           1.46e12

After importing the data, I noticed that the data type for the date
needed to be updated for the dataframes, using lubridate I updated the
data frames.

Now that the dates are in the correct format, I had to separate the date
columns in certain data frames that contained both the date and time in
a single column. This was done using the separate function.

``` r
heartrate_seconds_merged<-separate(heartrate_seconds_merged,Time,c("Date","Time"),sep = " ")
weightLogInfo<-separate(weightLogInfo,Date,c("Date","Time"),sep = " ")
hourlyCalories<-separate(hourlyCalories,ActivityHour,c("Date","Time"),sep = " ")
hourlyIntensities<-separate(hourlyIntensities,ActivityHour,c("Date","Time"),sep = " ")
```

Next I check the sample size of the data sets I am choosing to analyze,
usually a sample size of over 25 is reliable enough to analyze due to
the variety of subjects.

``` r
n_distinct(dailyActivity$Id)
```

    ## [1] 33

``` r
n_distinct(heartrate_seconds_merged$Id)
```

    ## [1] 14

``` r
n_distinct(weightLogInfo$Id)
```

    ## [1] 8

``` r
n_distinct(hourlyIntensities$Id)
```

    ## [1] 33

``` r
n_distinct(hourlyCalories$Id)
```

    ## [1] 33

``` r
n_distinct(dailySteps$Id)
```

    ## [1] 33

``` r
n_distinct(dailyIntensities$Id)
```

    ## [1] 33

``` r
n_distinct(dailyCalories$Id)
```

    ## [1] 33

``` r
n_distinct(sleepDay$Id)
```

    ## [1] 24

\*heartrate_seconds_merged and weightLogInfo both contain substantially
low amounts of unique Id’s, however sleepDay has 24 which is close
enough to our limit so it can still be included in the analysis.

#Data Exploration and Analysis

To get a grasp on the information the datasets contain, I selected
specific columns in the data frames and summarized the data within them.
This was especially helpful in giving me an idea of what I should expect
in the data being dealt with.

``` r
dailyActivity %>% 
  select(TotalSteps,
         TotalDistance,
        SedentaryMinutes, Calories) %>% 
  summary()
```

    ##    TotalSteps    TotalDistance    SedentaryMinutes    Calories   
    ##  Min.   :    0   Min.   : 0.000   Min.   :   0.0   Min.   :   0  
    ##  1st Qu.: 3790   1st Qu.: 2.620   1st Qu.: 729.8   1st Qu.:1828  
    ##  Median : 7406   Median : 5.245   Median :1057.5   Median :2134  
    ##  Mean   : 7638   Mean   : 5.490   Mean   : 991.2   Mean   :2304  
    ##  3rd Qu.:10727   3rd Qu.: 7.713   3rd Qu.:1229.5   3rd Qu.:2793  
    ##  Max.   :36019   Max.   :28.030   Max.   :1440.0   Max.   :4900

``` r
dailyIntensities %>% 
  select(SedentaryMinutes,
         LightlyActiveMinutes,
         LightActiveDistance) %>% 
  summary()
```

    ##  SedentaryMinutes LightlyActiveMinutes LightActiveDistance
    ##  Min.   :   0.0   Min.   :  0.0        Min.   : 0.000     
    ##  1st Qu.: 729.8   1st Qu.:127.0        1st Qu.: 1.945     
    ##  Median :1057.5   Median :199.0        Median : 3.365     
    ##  Mean   : 991.2   Mean   :192.8        Mean   : 3.341     
    ##  3rd Qu.:1229.5   3rd Qu.:264.0        3rd Qu.: 4.782     
    ##  Max.   :1440.0   Max.   :518.0        Max.   :10.710

``` r
dailySteps %>% 
  select(StepTotal,
         ActivityDay) %>% 
  summary()
```

    ##    StepTotal      ActivityDay        
    ##  Min.   :    0   Min.   :2016-04-12  
    ##  1st Qu.: 3790   1st Qu.:2016-04-19  
    ##  Median : 7406   Median :2016-04-26  
    ##  Mean   : 7638   Mean   :2016-04-26  
    ##  3rd Qu.:10727   3rd Qu.:2016-05-04  
    ##  Max.   :36019   Max.   :2016-05-12

``` r
sleepDay %>% 
  select(TotalTimeInBed,
         TotalMinutesAsleep,
         TotalSleepRecords) %>% 
  summary()
```

    ##  TotalTimeInBed  TotalMinutesAsleep TotalSleepRecords
    ##  Min.   : 61.0   Min.   : 58.0      Min.   :1.000    
    ##  1st Qu.:403.0   1st Qu.:361.0      1st Qu.:1.000    
    ##  Median :463.0   Median :433.0      Median :1.000    
    ##  Mean   :458.6   Mean   :419.5      Mean   :1.119    
    ##  3rd Qu.:526.0   3rd Qu.:490.0      3rd Qu.:1.000    
    ##  Max.   :961.0   Max.   :796.0      Max.   :3.000

``` r
hourlyCalories %>% 
  select(Calories) %>% 
  summary()
```

    ##     Calories     
    ##  Min.   : 42.00  
    ##  1st Qu.: 63.00  
    ##  Median : 83.00  
    ##  Mean   : 97.39  
    ##  3rd Qu.:108.00  
    ##  Max.   :948.00

``` r
hourlyIntensities %>% 
  select(TotalIntensity,
         AverageIntensity) %>% 
  summary()
```

    ##  TotalIntensity   AverageIntensity
    ##  Min.   :  0.00   Min.   :0.0000  
    ##  1st Qu.:  0.00   1st Qu.:0.0000  
    ##  Median :  3.00   Median :0.0500  
    ##  Mean   : 12.04   Mean   :0.2006  
    ##  3rd Qu.: 16.00   3rd Qu.:0.2667  
    ##  Max.   :180.00   Max.   :3.0000

``` r
dailyActivity %>% 
  select(LightlyActiveMinutes,
         FairlyActiveMinutes,
         VeryActiveMinutes) %>% 
  summary()
```

    ##  LightlyActiveMinutes FairlyActiveMinutes VeryActiveMinutes
    ##  Min.   :  0.0        Min.   :  0.00      Min.   :  0.00   
    ##  1st Qu.:127.0        1st Qu.:  0.00      1st Qu.:  0.00   
    ##  Median :199.0        Median :  6.00      Median :  4.00   
    ##  Mean   :192.8        Mean   : 13.56      Mean   : 21.16   
    ##  3rd Qu.:264.0        3rd Qu.: 19.00      3rd Qu.: 32.00   
    ##  Max.   :518.0        Max.   :143.00      Max.   :210.00

Key Takeaways: *Avg sedentary min is 991, Avg total distance 5.245, Avg
cal 2304 *Avg min asleep was 419.5 about 6 hours *Avg cal per hour 97.39
*Avg total intensity per hour 12.04 \*LightlyActiveMinutes has the
highest values, signifying that most participants were lightly active
more often than being fairly or vary active

After summarizing data I realized some of the datasets had matching
information that could be used to merge certain datasets with others,
using the merge function I combined them, however I would need to make
sure the columns contained the same data.

``` r
dailyActivity<-dailyActivity %>% 
  rename(Date=ActivityDate)
sleepDay<-sleepDay %>% 
  rename(Date=SleepDay)

activity_sleep <-merge(dailyActivity,sleepDay,by=c("Id","Date"))
head(activity_sleep)
```

    ##           Id       Date TotalSteps TotalDistance TrackerDistance
    ## 1 1503960366 2016-04-12      13162          8.50            8.50
    ## 2 1503960366 2016-04-13      10735          6.97            6.97
    ## 3 1503960366 2016-04-15       9762          6.28            6.28
    ## 4 1503960366 2016-04-16      12669          8.16            8.16
    ## 5 1503960366 2016-04-17       9705          6.48            6.48
    ## 6 1503960366 2016-04-19      15506          9.88            9.88
    ##   LoggedActivitiesDistance VeryActiveDistance ModeratelyActiveDistance
    ## 1                        0               1.88                     0.55
    ## 2                        0               1.57                     0.69
    ## 3                        0               2.14                     1.26
    ## 4                        0               2.71                     0.41
    ## 5                        0               3.19                     0.78
    ## 6                        0               3.53                     1.32
    ##   LightActiveDistance SedentaryActiveDistance VeryActiveMinutes
    ## 1                6.06                       0                25
    ## 2                4.71                       0                21
    ## 3                2.83                       0                29
    ## 4                5.04                       0                36
    ## 5                2.51                       0                38
    ## 6                5.03                       0                50
    ##   FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes Calories
    ## 1                  13                  328              728     1985
    ## 2                  19                  217              776     1797
    ## 3                  34                  209              726     1745
    ## 4                  10                  221              773     1863
    ## 5                  20                  164              539     1728
    ## 6                  31                  264              775     2035
    ##   TotalSleepRecords TotalMinutesAsleep TotalTimeInBed
    ## 1                 1                327            346
    ## 2                 2                384            407
    ## 3                 1                412            442
    ## 4                 2                340            367
    ## 5                 1                700            712
    ## 6                 1                304            320

``` r
View(activity_sleep)

hourlyActivity <-merge(hourlyCalories,hourlyIntensities,by=c("Id","Date","Time"))
head(hourlyActivity)
```

    ##           Id       Date     Time Calories TotalIntensity AverageIntensity
    ## 1 1503960366 2016-04-12 00:00:00       81             20         0.333333
    ## 2 1503960366 2016-04-12 01:00:00       61              8         0.133333
    ## 3 1503960366 2016-04-12 02:00:00       59              7         0.116667
    ## 4 1503960366 2016-04-12 03:00:00       47              0         0.000000
    ## 5 1503960366 2016-04-12 04:00:00       48              0         0.000000
    ## 6 1503960366 2016-04-12 05:00:00       48              0         0.000000

``` r
View(hourlyActivity)
```

Now we are ready to create our visualizations!

#Data Visualizations

Alongside the summaries above, I used visualizations to find certain
connections and draw conclusions on relationships between variables.

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Bellabeat_CaseStudy_files/figure-markdown_github/TotalSteps%20v%20Calories-1.png)
Here we see a positive relationship between the number of total steps
and calories burned, more steps lead to more activity which in turn
causes the user to burn more calories.

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Bellabeat_CaseStudy_files/figure-markdown_github/SedentaryMinutes%20v%20TotalMinutesAsleep-1.png)
As SedentaryMinutes increased, we saw a decrease in TotalMinutesAsleep,
this shows that the less active throughout the day the users are the
less sleep they get.

``` r
ggplot(data = hourlyActivity,aes(x=Time,y=Calories))+
  geom_histogram(stat = 'identity',fill='pink') + theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1)) + labs(title = "Total Calories Burned Hourly")
```

    ## Warning: Ignoring unknown parameters: binwidth, bins, pad

![](Bellabeat_CaseStudy_files/figure-markdown_github/Calories%20burned%20over%20Hours-1.png)

``` r
ggplot(data = hourlyActivity,aes(x=Time,y=AverageIntensity))+
  geom_histogram(stat = 'identity',fill='red') + theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))+labs(title = "AverageIntensity By Hour")
```

    ## Warning: Ignoring unknown parameters: binwidth, bins, pad

![](Bellabeat_CaseStudy_files/figure-markdown_github/unnamed-chunk-2-1.png)

In both plots 17:00-19:00 hold the highest values, this signifies that
during these hours the users are the most physically active as they have
the highest average intensity and most calories lost.

#Summary and Recommendations

Through the data we are able to get a picture of what type of people use
fitness tracker devices, working women who find time later in the day to
engage in light physical activity. However, there are quite a few
limitations on this data, there is some missing data for an ID,
4057192912, which could affect the analysis. Based off what we have
there are many things that we can include in Bellabeat products to
increrase our presence in the global smart device market

1.  Tracking the light activity that so many users engage in would not
    only be motivation but it would serve to keep progress on things
    such as weight maintenance and overall physical fitness. These are
    busy women who spend a good portion of their time remaining
    sedentary, by marking their progress not only will they be able to
    gauge themselves it would also encourage them to engage in even more
    physical activity.

2.  It was discovered that many of these users seemed to be more active
    around the times 17:00-19:00,or 5pm-7pm, by sending notifications
    around this time Bellabeat can promote more physical activity at a
    time when the users are done with work.

3.  By promoting more activity, sedentary minutes will decrease, earlier
    in this analysis a relationship between sedentary minutes and total
    time asleep was found. The more time a user spend being sedentary
    the less sleep they would get, and the average was about 419.5 min
    or about 6 hours. This is below the recommended amount of 7-8 hours,
    so not only will Bellabeat promote a healthier lifestyle, they will
    help their users sleep alot better at night.

Through these changes and updates, Bellabeat can be more of a health
companion rather than just another fitness tracker. This can greatly
impact the lives of women who might not have enough time to spend hours
in the gym and track how much calories they burn when they go out for a
walk.
