Practice Exam
=============

This practice exam asks you to do several code wrangling tasks that we
have done in class so far.

Clone this repo into Rstudio and fill in the necessary code. Then,
commit and push to github. Finally, turn in a link to canvas.

    ## ── Attaching packages ────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.2.1     ✓ purrr   0.3.3
    ## ✓ tibble  2.1.3     ✓ dplyr   0.8.4
    ## ✓ tidyr   1.0.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.4.0

    ## ── Conflicts ───────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

Make a plot with three facets, one for each airport in the weather data.
The x-axis should be the day of the year (1:365) and the y-axis should
be the mean temperature recorded on that day, at that airport.

    library(lubridate)

    ## 
    ## Attaching package: 'lubridate'

    ## The following object is masked from 'package:base':
    ## 
    ##     date

    weather %>% mutate(day_of_year = yday(time_hour))

    ## # A tibble: 26,115 x 16
    ##    origin  year month   day  hour  temp  dewp humid wind_dir wind_speed
    ##    <chr>  <int> <int> <int> <int> <dbl> <dbl> <dbl>    <dbl>      <dbl>
    ##  1 EWR     2013     1     1     1  39.0  26.1  59.4      270      10.4 
    ##  2 EWR     2013     1     1     2  39.0  27.0  61.6      250       8.06
    ##  3 EWR     2013     1     1     3  39.0  28.0  64.4      240      11.5 
    ##  4 EWR     2013     1     1     4  39.9  28.0  62.2      250      12.7 
    ##  5 EWR     2013     1     1     5  39.0  28.0  64.4      260      12.7 
    ##  6 EWR     2013     1     1     6  37.9  28.0  67.2      240      11.5 
    ##  7 EWR     2013     1     1     7  39.0  28.0  64.4      240      15.0 
    ##  8 EWR     2013     1     1     8  39.9  28.0  62.2      250      10.4 
    ##  9 EWR     2013     1     1     9  39.9  28.0  62.2      260      15.0 
    ## 10 EWR     2013     1     1    10  41    28.0  59.6      260      13.8 
    ## # … with 26,105 more rows, and 6 more variables: wind_gust <dbl>, precip <dbl>,
    ## #   pressure <dbl>, visib <dbl>, time_hour <dttm>, day_of_year <dbl>

Make a non-tidy matrix of that data where each row is an airport and
each column is a day of the year.

    weather %>% mutate(day_of_year = yday(time_hour)) %>% 
      drop_na(day_of_year) %>% 
      group_by(origin, day_of_year) %>% 
      summarize(wind_speed = mean(wind_speed)) %>% 
      spread(day_of_year, wind_speed)

    ## # A tibble: 3 x 365
    ## # Groups:   origin [3]
    ##   origin   `1`   `2`   `3`   `4`   `5`   `6`   `7`   `8`   `9`  `10`  `11`  `12`
    ##   <chr>  <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 EWR     13.2  10.9  8.58  14.0  9.40  9.11  7.34  7.19  5.99  8.92  4.79  5.03
    ## 2 JFK     15.4  14.5 11.7   16.3 11.7  10.9   8.34 10.5   7.77 11.8   6.81  6.14
    ## 3 LGA     15.4  13.6 11.1   15.4  9.88  9.76  9.06  8.34  8.87 11.8   7.58  6.43
    ## # … with 352 more variables: `13` <dbl>, `14` <dbl>, `15` <dbl>, `16` <dbl>,
    ## #   `17` <dbl>, `18` <dbl>, `19` <dbl>, `20` <dbl>, `21` <dbl>, `22` <dbl>,
    ## #   `23` <dbl>, `24` <dbl>, `25` <dbl>, `26` <dbl>, `27` <dbl>, `28` <dbl>,
    ## #   `29` <dbl>, `30` <dbl>, `31` <dbl>, `32` <dbl>, `33` <dbl>, `34` <dbl>,
    ## #   `35` <dbl>, `36` <dbl>, `37` <dbl>, `38` <dbl>, `39` <dbl>, `40` <dbl>,
    ## #   `41` <dbl>, `42` <dbl>, `43` <dbl>, `44` <dbl>, `45` <dbl>, `46` <dbl>,
    ## #   `47` <dbl>, `48` <dbl>, `49` <dbl>, `50` <dbl>, `51` <dbl>, `52` <dbl>,
    ## #   `53` <dbl>, `54` <dbl>, `55` <dbl>, `56` <dbl>, `57` <dbl>, `58` <dbl>,
    ## #   `59` <dbl>, `60` <dbl>, `61` <dbl>, `62` <dbl>, `63` <dbl>, `64` <dbl>,
    ## #   `65` <dbl>, `66` <dbl>, `67` <dbl>, `68` <dbl>, `69` <dbl>, `70` <dbl>,
    ## #   `71` <dbl>, `72` <dbl>, `73` <dbl>, `74` <dbl>, `75` <dbl>, `76` <dbl>,
    ## #   `77` <dbl>, `78` <dbl>, `79` <dbl>, `80` <dbl>, `81` <dbl>, `82` <dbl>,
    ## #   `83` <dbl>, `84` <dbl>, `85` <dbl>, `86` <dbl>, `87` <dbl>, `88` <dbl>,
    ## #   `89` <dbl>, `90` <dbl>, `91` <dbl>, `92` <dbl>, `93` <dbl>, `94` <dbl>,
    ## #   `95` <dbl>, `96` <dbl>, `97` <dbl>, `98` <dbl>, `99` <dbl>, `100` <dbl>,
    ## #   `101` <dbl>, `102` <dbl>, `103` <dbl>, `104` <dbl>, `105` <dbl>,
    ## #   `106` <dbl>, `107` <dbl>, `108` <dbl>, `109` <dbl>, `110` <dbl>,
    ## #   `111` <dbl>, `112` <dbl>, …

For each (airport, day) contruct a tidy data set of the airport’s
“performance” as the proportion of flights that departed less than an
hour late.

    performance <- flights %>% mutate(day_of_year = yday(time_hour)) %>% 
      mutate(lessthanHour = dep_delay<60) %>% 
      group_by(origin, day_of_year) %>% 
      summarize(proportion = mean(lessthanHour))
    performance$proportion[is.na(performance$proportion)] <- 1
    performance

    ## # A tibble: 1,095 x 3
    ## # Groups:   origin [3]
    ##    origin day_of_year proportion
    ##    <chr>        <dbl>      <dbl>
    ##  1 EWR              1      1    
    ##  2 EWR              2      1    
    ##  3 EWR              3      1    
    ##  4 EWR              4      1    
    ##  5 EWR              5      1    
    ##  6 EWR              6      1    
    ##  7 EWR              7      0.921
    ##  8 EWR              8      1    
    ##  9 EWR              9      1    
    ## 10 EWR             10      1    
    ## # … with 1,085 more rows

Construct a tidy data set to that give weather summaries for each
(airport, day). Use the total precipitation, minimum visibility, maximum
wind\_gust, and average wind\_speed.

    weather %>% mutate(day_of_year = yday(time_hour)) %>% 
      group_by(origin, day_of_year) %>% 
      summarize(precipitation=sum(precip), minVis = min(visib), max(wind_gust), mean(wind_speed))

    ## # A tibble: 1,092 x 6
    ## # Groups:   origin [3]
    ##    origin day_of_year precipitation minVis `max(wind_gust)` `mean(wind_speed)`
    ##    <chr>        <dbl>         <dbl>  <dbl>            <dbl>              <dbl>
    ##  1 EWR              1             0     10               NA              13.2 
    ##  2 EWR              2             0     10               NA              10.9 
    ##  3 EWR              3             0     10               NA               8.58
    ##  4 EWR              4             0     10               NA              14.0 
    ##  5 EWR              5             0     10               NA               9.40
    ##  6 EWR              6             0      6               NA               9.11
    ##  7 EWR              7             0     10               NA               7.34
    ##  8 EWR              8             0      8               NA               7.19
    ##  9 EWR              9             0      6               NA               5.99
    ## 10 EWR             10             0     10               NA               8.92
    ## # … with 1,082 more rows

Construct a linear model to predict the performance of each
(airport,day) using the weather summaries and a “fixed effect” for each
airport. Display the summaries.

    weatherByDay <- weather %>% mutate(day_of_year = yday(time_hour)) %>% 
      group_by(origin, day_of_year) %>% 
      summarize(precipitation=sum(precip), minVis = min(visib), maxGust=max(wind_gust), wind_speed=mean(wind_speed))

    joined <- left_join(performance, weatherByDay, by=c('origin', 'day_of_year'))
    summary(lm(proportion~precipitation+minVis+wind_speed+origin, data=joined))

    ## 
    ## Call:
    ## lm(formula = proportion ~ precipitation + minVis + wind_speed + 
    ##     origin, data = joined)
    ## 
    ## Residuals:
    ##       Min        1Q    Median        3Q       Max 
    ## -0.145345  0.000459  0.005749  0.010144  0.015600 
    ## 
    ## Coefficients:
    ##                 Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)    0.9966319  0.0022102 450.928  < 2e-16 ***
    ## precipitation  0.0035722  0.0020940   1.706 0.088317 .  
    ## minVis        -0.0005721  0.0001880  -3.043 0.002399 ** 
    ## wind_speed    -0.0001222  0.0001391  -0.879 0.379715    
    ## originJFK     -0.0031929  0.0014270  -2.238 0.025455 *  
    ## originLGA      0.0047265  0.0014010   3.374 0.000768 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.01875 on 1082 degrees of freedom
    ##   (7 observations deleted due to missingness)
    ## Multiple R-squared:  0.04829,    Adjusted R-squared:  0.04389 
    ## F-statistic: 10.98 on 5 and 1082 DF,  p-value: 2.503e-10

Repeat the above, but only for EWR. Obviously, exclude the fixed effect
for each airport.

    ewr <- joined[joined$origin=="EWR",]
    summary(lm(proportion~precipitation+minVis+wind_speed, data=ewr))

    ## 
    ## Call:
    ## lm(formula = proportion ~ precipitation + minVis + wind_speed, 
    ##     data = ewr)
    ## 
    ## Residuals:
    ##       Min        1Q    Median        3Q       Max 
    ## -0.144564  0.000611  0.007371  0.011144  0.011469 
    ## 
    ## Coefficients:
    ##                 Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)    9.987e-01  3.675e-03 271.784  < 2e-16 ***
    ## precipitation  3.242e-03  3.656e-03   0.887  0.37583    
    ## minVis        -9.703e-04  3.637e-04  -2.667  0.00799 ** 
    ## wind_speed    -2.337e-05  2.440e-04  -0.096  0.92377    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.02022 on 359 degrees of freedom
    ##   (2 observations deleted due to missingness)
    ## Multiple R-squared:  0.03688,    Adjusted R-squared:  0.02884 
    ## F-statistic: 4.583 on 3 and 359 DF,  p-value: 0.003653
