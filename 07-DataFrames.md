Data Frames
================

-   [Data Frames are Tables](#data-frames-are-tables)
    -   [Information on Data Frames](#information-on-data-frames)
    -   [Accessing Data Frames Elements](#accessing-data-frames-elements)
    -   [Adding More Data, Removing Data](#adding-more-data-removing-data)
-   [Reading and Writing Data Frames](#reading-and-writing-data-frames)
    -   [.. as CSV](#as-csv)
    -   [.. as R Data](#as-r-data)
-   [Missing Values (again)](#missing-values-again)

Data Frames are Tables
----------------------

Data Frames are the most common way to represent data in R in Data Science and Data Mining applications.

We can create data frames from sets of observations. This below is a column-based example.

``` r
maxTempSJC <- c(29.7,30.1,29.5,27.3,25.1,24.3,24.1,26.2,27.2,27.3,28,28.7)
avgTempSJC <- c(22.2,22.4,21.6,19.6,17,16.1,15.6,17.1,18.8,19.4,20.3,21.4)
minTempSJC <- c(16.2,16.5,15.7,13.2,10.1,8.9,8.2,9.9,11.9,13.4,14.2,15.3)
months <- c("Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec")
sjcTemps <- data.frame(Max=maxTempSJC,Avg=avgTempSJC,Min=minTempSJC,row.names = months)
sjcTemps
```

    ##      Max  Avg  Min
    ## Jan 29.7 22.2 16.2
    ## Feb 30.1 22.4 16.5
    ## Mar 29.5 21.6 15.7
    ## Apr 27.3 19.6 13.2
    ## May 25.1 17.0 10.1
    ## Jun 24.3 16.1  8.9
    ## Jul 24.1 15.6  8.2
    ## Aug 26.2 17.1  9.9
    ## Sep 27.2 18.8 11.9
    ## Oct 27.3 19.4 13.4
    ## Nov 28.0 20.3 14.2
    ## Dec 28.7 21.4 15.3

``` r
class(sjcTemps)
```

    ## [1] "data.frame"

Now for a row-based example, starting with an empty Data Frame:

``` r
sjcTemps2 <- data.frame(Max=numeric(),Avg=numeric(),Min=numeric())
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=29.7,Avg=22.2,Min=16.2))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=30.1,Avg=22.4,Min=16.5))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=29.5,Avg=21.6,Min=15.7))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=27.3,Avg=19.6,Min=13.2))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=25.1,Avg=17,  Min=10.1))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=24.3,Avg=16.1,Min= 8.9))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=24.1,Avg=15.6,Min= 8.2))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=26.2,Avg=17.1,Min= 9.9))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=27.2,Avg=18.8,Min=11.9))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=27.3,Avg=19.4,Min=13.4))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=28,  Avg=20.3,Min=14.2))
sjcTemps2 <- rbind(sjcTemps2,data.frame(Max=28.7,Avg=21.4,Min=15.3))
row.names(sjcTemps2) <- months
sjcTemps2
```

    ##      Max  Avg  Min
    ## Jan 29.7 22.2 16.2
    ## Feb 30.1 22.4 16.5
    ## Mar 29.5 21.6 15.7
    ## Apr 27.3 19.6 13.2
    ## May 25.1 17.0 10.1
    ## Jun 24.3 16.1  8.9
    ## Jul 24.1 15.6  8.2
    ## Aug 26.2 17.1  9.9
    ## Sep 27.2 18.8 11.9
    ## Oct 27.3 19.4 13.4
    ## Nov 28.0 20.3 14.2
    ## Dec 28.7 21.4 15.3

``` r
class(sjcTemps2)
```

    ## [1] "data.frame"

### Information on Data Frames

Basic functions to get information on data frames:

``` r
nrow(sjcTemps)
```

    ## [1] 12

``` r
ncol(sjcTemps)
```

    ## [1] 3

``` r
head(sjcTemps)
```

    ##      Max  Avg  Min
    ## Jan 29.7 22.2 16.2
    ## Feb 30.1 22.4 16.5
    ## Mar 29.5 21.6 15.7
    ## Apr 27.3 19.6 13.2
    ## May 25.1 17.0 10.1
    ## Jun 24.3 16.1  8.9

More information with <tt>str</tt>:

``` r
str(sjcTemps)
```

    ## 'data.frame':    12 obs. of  3 variables:
    ##  $ Max: num  29.7 30.1 29.5 27.3 25.1 24.3 24.1 26.2 27.2 27.3 ...
    ##  $ Avg: num  22.2 22.4 21.6 19.6 17 16.1 15.6 17.1 18.8 19.4 ...
    ##  $ Min: num  16.2 16.5 15.7 13.2 10.1 8.9 8.2 9.9 11.9 13.4 ...

Even more information (statistics) with <tt>summary</tt>:

``` r
summary(sjcTemps)
```

    ##       Max             Avg             Min       
    ##  Min.   :24.10   Min.   :15.60   Min.   : 8.20  
    ##  1st Qu.:25.93   1st Qu.:17.07   1st Qu.:10.05  
    ##  Median :27.30   Median :19.50   Median :13.30  
    ##  Mean   :27.29   Mean   :19.29   Mean   :12.79  
    ##  3rd Qu.:28.90   3rd Qu.:21.45   3rd Qu.:15.40  
    ##  Max.   :30.10   Max.   :22.40   Max.   :16.50

### Accessing Data Frames Elements

Accessing by columns' names

``` r
sjcTemps$Min
```

    ##  [1] 16.2 16.5 15.7 13.2 10.1  8.9  8.2  9.9 11.9 13.4 14.2 15.3

``` r
sjcTemps$Max
```

    ##  [1] 29.7 30.1 29.5 27.3 25.1 24.3 24.1 26.2 27.2 27.3 28.0 28.7

Accessing individual values

``` r
sjcTemps$Min[2]
```

    ## [1] 16.5

``` r
sjcTemps$Max[2]
```

    ## [1] 30.1

Basic slicing:

``` r
sjcTemps[,2]
```

    ##  [1] 22.2 22.4 21.6 19.6 17.0 16.1 15.6 17.1 18.8 19.4 20.3 21.4

``` r
sjcTemps[2,]
```

    ##      Max  Avg  Min
    ## Feb 30.1 22.4 16.5

``` r
sjcTemps[2,2]
```

    ## [1] 22.4

Using names:

``` r
sjcTemps["Jul",]
```

    ##      Max  Avg Min
    ## Jul 24.1 15.6 8.2

``` r
sjcTemps["Jul",1]
```

    ## [1] 24.1

``` r
sjcTemps["Jul","Min"]
```

    ## [1] 8.2

Using ranges, etc.:

``` r
sjcTemps[1:6,c(1,3)]
```

    ##      Max  Min
    ## Jan 29.7 16.2
    ## Feb 30.1 16.5
    ## Mar 29.5 15.7
    ## Apr 27.3 13.2
    ## May 25.1 10.1
    ## Jun 24.3  8.9

``` r
sjcTemps["Jul",2:3]
```

    ##      Avg Min
    ## Jul 15.6 8.2

``` r
sjcTemps[c("Jan","Jul"),c("Max","Min")]
```

    ##      Max  Min
    ## Jan 29.7 16.2
    ## Jul 24.1  8.2

If we can read these values, we can change them.

``` r
sjcTemps3 <- sjcTemps
sjcTemps3["Jul",] <- 0
sjcTemps3[,"Avg"] <- 0
sjcTemps3["Aug",] <- c(1,2,3)
sjcTemps3["Jul",] <- sjcTemps3["Jul",]+c(3,4)
sjcTemps3["Dec","Max"] <- 50
sjcTemps3
```

    ##      Max Avg  Min
    ## Jan 29.7   0 16.2
    ## Feb 30.1   0 16.5
    ## Mar 29.5   0 15.7
    ## Apr 27.3   0 13.2
    ## May 25.1   0 10.1
    ## Jun 24.3   0  8.9
    ## Jul  3.0   4  3.0
    ## Aug  1.0   2  3.0
    ## Sep 27.2   0 11.9
    ## Oct 27.3   0 13.4
    ## Nov 28.0   0 14.2
    ## Dec 50.0   0 15.3

### Adding More Data, Removing Data

We can add new columns to a Data Frame: just choose a new column name and an operation to fill it.

``` r
sjcTemps$Range <- sjcTemps$Max-sjcTemps$Min
sjcTemps$Flag <- TRUE
sjcTemps$Vacations <- c(TRUE,TRUE,FALSE,FALSE,FALSE,FALSE,TRUE,FALSE,FALSE,FALSE,FALSE,TRUE)
sjcTemps$Season <- factor(c('Summer','Summer','Autumn','Autumn','Autumn','Winter',
                     'Winter','Winter','Spring','Spring','Spring','Summer'))
sjcTemps
```

    ##      Max  Avg  Min Range Flag Vacations Season
    ## Jan 29.7 22.2 16.2  13.5 TRUE      TRUE Summer
    ## Feb 30.1 22.4 16.5  13.6 TRUE      TRUE Summer
    ## Mar 29.5 21.6 15.7  13.8 TRUE     FALSE Autumn
    ## Apr 27.3 19.6 13.2  14.1 TRUE     FALSE Autumn
    ## May 25.1 17.0 10.1  15.0 TRUE     FALSE Autumn
    ## Jun 24.3 16.1  8.9  15.4 TRUE     FALSE Winter
    ## Jul 24.1 15.6  8.2  15.9 TRUE      TRUE Winter
    ## Aug 26.2 17.1  9.9  16.3 TRUE     FALSE Winter
    ## Sep 27.2 18.8 11.9  15.3 TRUE     FALSE Spring
    ## Oct 27.3 19.4 13.4  13.9 TRUE     FALSE Spring
    ## Nov 28.0 20.3 14.2  13.8 TRUE     FALSE Spring
    ## Dec 28.7 21.4 15.3  13.4 TRUE      TRUE Summer

``` r
str(sjcTemps)
```

    ## 'data.frame':    12 obs. of  7 variables:
    ##  $ Max      : num  29.7 30.1 29.5 27.3 25.1 24.3 24.1 26.2 27.2 27.3 ...
    ##  $ Avg      : num  22.2 22.4 21.6 19.6 17 16.1 15.6 17.1 18.8 19.4 ...
    ##  $ Min      : num  16.2 16.5 15.7 13.2 10.1 8.9 8.2 9.9 11.9 13.4 ...
    ##  $ Range    : num  13.5 13.6 13.8 14.1 15 15.4 15.9 16.3 15.3 13.9 ...
    ##  $ Flag     : logi  TRUE TRUE TRUE TRUE TRUE TRUE ...
    ##  $ Vacations: logi  TRUE TRUE FALSE FALSE FALSE FALSE ...
    ##  $ Season   : Factor w/ 4 levels "Autumn","Spring",..: 3 3 1 1 1 4 4 4 2 2 ...

We can also drop columns from a Data Frame:

``` r
sjcTempsModified <- sjcTemps # avoid changing this one...
sjcTempsModified$Avg <- NULL
sjcTempsModified$Flag <- NULL
head(sjcTempsModified)
```

    ##      Max  Min Range Vacations Season
    ## Jan 29.7 16.2  13.5      TRUE Summer
    ## Feb 30.1 16.5  13.6      TRUE Summer
    ## Mar 29.5 15.7  13.8     FALSE Autumn
    ## Apr 27.3 13.2  14.1     FALSE Autumn
    ## May 25.1 10.1  15.0     FALSE Autumn
    ## Jun 24.3  8.9  15.4     FALSE Winter

Other way do to this:

``` r
sjcTempsModified <- subset(sjcTemps, select = c(Min,Max,Season))
# Also: sjcTempsModified <- sjcTemps[keep]
head(sjcTempsModified)
```

    ##      Min  Max Season
    ## Jan 16.2 29.7 Summer
    ## Feb 16.5 30.1 Summer
    ## Mar 15.7 29.5 Autumn
    ## Apr 13.2 27.3 Autumn
    ## May 10.1 25.1 Autumn
    ## Jun  8.9 24.3 Winter

Another one:

``` r
sjcTempsModified <- subset(sjcTemps, select = -c(Range,Flag,Avg,Season))
head(sjcTempsModified)
```

    ##      Max  Min Vacations
    ## Jan 29.7 16.2      TRUE
    ## Feb 30.1 16.5      TRUE
    ## Mar 29.5 15.7     FALSE
    ## Apr 27.3 13.2     FALSE
    ## May 25.1 10.1     FALSE
    ## Jun 24.3  8.9     FALSE

Reading and Writing Data Frames
-------------------------------

Creating Data Frames in code is not practical. Let's read them from files.

### .. as CSV

Let's read a CSV file into R (check it here: <https://github.com/rafaeldcsantos/CAP386/blob/master/Data/Taubate.csv>)

``` r
taubateWeather <- read.csv(file="Data/Taubate.csv", header=TRUE, sep=",", stringsAsFactors=FALSE)
taubateWeather
```

    ##    TAUBATE Maximum.Absolute.Temperature Maximum.Average.Temperature
    ## 1      Jan                         36.7                        30.2
    ## 2      Feb                         40.1                        30.5
    ## 3      Mar                         36.2                        29.9
    ## 4      Apr                         34.2                        27.8
    ## 5      May                         32.6                        25.4
    ## 6      Jun                         31.0                        24.6
    ## 7      Jul                         32.1                        24.4
    ## 8      Aug                         35.6                        26.4
    ## 9      Sep                         37.8                        27.6
    ## 10     Oct                         38.0                        27.5
    ## 11     Nov                         37.4                        28.7
    ## 12     Dec                         37.5                        29.1
    ## 13    Year                         40.1                        27.7
    ##    Average.Temperature Minimum.Average.Temperature
    ## 1                 23.3                        17.7
    ## 2                 23.5                        17.8
    ## 3                 22.9                        17.8
    ## 4                 20.8                        16.1
    ## 5                 18.1                        14.2
    ## 6                 16.7                        12.9
    ## 7                 16.4                        12.6
    ## 8                 18.2                        14.0
    ## 9                 20.0                        15.7
    ## 10                20.7                        16.4
    ## 11                21.7                        16.9
    ## 12                22.7                        17.1
    ## 13                20.4                        15.8
    ##    Minimum.Absolute.Temperature Rainfall..mm. Days.with.Rainfall....1mm
    ## 1                          10.9         233.5                        17
    ## 2                          12.6         192.1                        14
    ## 3                          11.6         173.5                        12
    ## 4                           5.4          67.1                         7
    ## 5                           4.2          40.9                         4
    ## 6                           1.1          29.3                         4
    ## 7                           0.9          31.1                         4
    ## 8                           2.6          41.7                         4
    ## 9                           3.8          64.0                         6
    ## 10                          7.8         132.8                        11
    ## 11                          8.6         146.2                        12
    ## 12                         11.0         244.6                        16
    ## 13                          0.9        1396.8                       111
    ##    Relative.Humidity Sunshine.Hours
    ## 1               76.8          170.0
    ## 2               76.7          168.2
    ## 3               76.8          179.5
    ## 4               75.9          177.3
    ## 5               76.2          176.1
    ## 6               75.7          175.6
    ## 7               72.5          188.9
    ## 8               69.1          186.2
    ## 9               69.2          158.8
    ## 10              74.0          148.8
    ## 11              73.8          161.5
    ## 12              76.8          155.0
    ## 13              74.5         2045.9

Check the formatting of the CSV file: the first column should be named "Month" (see also its last row...)

``` r
colnames(taubateWeather)[1] <- "Month"
```

Everything seems to be there! Just for fun let's see some statistics (dropping the measure for Year first)

``` r
taubateWeather <- taubateWeather[taubateWeather$Month != "Year", ]
str(taubateWeather)
```

    ## 'data.frame':    12 obs. of  10 variables:
    ##  $ Month                       : chr  "Jan" "Feb" "Mar" "Apr" ...
    ##  $ Maximum.Absolute.Temperature: num  36.7 40.1 36.2 34.2 32.6 31 32.1 35.6 37.8 38 ...
    ##  $ Maximum.Average.Temperature : num  30.2 30.5 29.9 27.8 25.4 24.6 24.4 26.4 27.6 27.5 ...
    ##  $ Average.Temperature         : num  23.3 23.5 22.9 20.8 18.1 16.7 16.4 18.2 20 20.7 ...
    ##  $ Minimum.Average.Temperature : num  17.7 17.8 17.8 16.1 14.2 12.9 12.6 14 15.7 16.4 ...
    ##  $ Minimum.Absolute.Temperature: num  10.9 12.6 11.6 5.4 4.2 1.1 0.9 2.6 3.8 7.8 ...
    ##  $ Rainfall..mm.               : num  233.5 192.1 173.5 67.1 40.9 ...
    ##  $ Days.with.Rainfall....1mm   : int  17 14 12 7 4 4 4 4 6 11 ...
    ##  $ Relative.Humidity           : num  76.8 76.7 76.8 75.9 76.2 75.7 72.5 69.1 69.2 74 ...
    ##  $ Sunshine.Hours              : num  170 168 180 177 176 ...

Let's save it.

``` r
write.csv(taubateWeather, file = "Data/Taubate-Fixed.csv")
```

See it here: <https://github.com/rafaeldcsantos/CAP386/blob/master/Data/Taubate-Fixed.csv>

### .. as R Data

We can save R objects (including data frames) like this:

``` r
dump("taubateWeather", file = "Data/Taubate-Fixed.R")
```

See the file here: <https://github.com/rafaeldcsantos/CAP386/blob/master/Data/Taubate-Fixed.R>

We can read dumped objects with <tt>source</tt>:

``` r
rm(taubateWeather) # make sure it is gone!
source(file = "Data/Taubate-Fixed.R")
str(taubateWeather)
```

    ## 'data.frame':    12 obs. of  10 variables:
    ##  $ Month                       : chr  "Jan" "Feb" "Mar" "Apr" ...
    ##  $ Maximum.Absolute.Temperature: num  36.7 40.1 36.2 34.2 32.6 31 32.1 35.6 37.8 38 ...
    ##  $ Maximum.Average.Temperature : num  30.2 30.5 29.9 27.8 25.4 24.6 24.4 26.4 27.6 27.5 ...
    ##  $ Average.Temperature         : num  23.3 23.5 22.9 20.8 18.1 16.7 16.4 18.2 20 20.7 ...
    ##  $ Minimum.Average.Temperature : num  17.7 17.8 17.8 16.1 14.2 12.9 12.6 14 15.7 16.4 ...
    ##  $ Minimum.Absolute.Temperature: num  10.9 12.6 11.6 5.4 4.2 1.1 0.9 2.6 3.8 7.8 ...
    ##  $ Rainfall..mm.               : num  233.5 192.1 173.5 67.1 40.9 ...
    ##  $ Days.with.Rainfall....1mm   : int  17 14 12 7 4 4 4 4 6 11 ...
    ##  $ Relative.Humidity           : num  76.8 76.7 76.8 75.9 76.2 75.7 72.5 69.1 69.2 74 ...
    ##  $ Sunshine.Hours              : num  170 168 180 177 176 ...

Dump can be used to dump several objects in the same file.

``` r
l <- c(FALSE,FALSE,TRUE,FALSE)
n <- c(12.333,12.389,12.918,13,14.021)
cc <- c('programming','r','python')
v <- pi*2;
dump(c("taubateWeather","l","n","cc","v"), file = "Data/SomeMixedData.R")
```

See the file here: <https://github.com/rafaeldcsantos/CAP386/blob/master/Data/SomeMixedData.R>

Missing Values (again)
----------------------

File with missing data: <https://github.com/rafaeldcsantos/CAP386/blob/master/Data/TaubateMissing.R>

``` r
taubateMissing <- read.csv(file="Data/TaubateMissing.csv", header=TRUE, sep=",", stringsAsFactors=FALSE)
taubateMissing
```

    ##    TAUBATE Maximum.Absolute.Temperature Maximum.Average.Temperature
    ## 1      Jan                         36.7                        30.2
    ## 2      Feb                         40.1                        30.5
    ## 3      Mar                         36.2                        29.9
    ## 4      Apr                         34.2                          NA
    ## 5      May                         32.6                        25.4
    ## 6      Jun                         31.0                        24.6
    ## 7      Jul                         32.1                        24.4
    ## 8      Aug                         35.6                        26.4
    ## 9      Sep                         37.8                        27.6
    ## 10     Oct                         38.0                        27.5
    ## 11     Nov                         37.4                        28.7
    ## 12     Dec                         37.5                        29.1
    ## 13    Year                         40.1                        27.7
    ##    Average.Temperature Minimum.Average.Temperature
    ## 1                 23.3                        17.7
    ## 2                 23.5                        17.8
    ## 3                 22.9                        17.8
    ## 4                 20.8                        16.1
    ## 5                 18.1                        14.2
    ## 6                 16.7                        12.9
    ## 7                 16.4                        12.6
    ## 8                 18.2                        14.0
    ## 9                 20.0                        15.7
    ## 10                20.7                          NA
    ## 11                21.7                        16.9
    ## 12                22.7                        17.1
    ## 13                20.4                        15.8
    ##    Minimum.Absolute.Temperature Rainfall..mm. Days.with.Rainfall....1mm
    ## 1                          10.9         233.5                        17
    ## 2                          12.6         192.1                        14
    ## 3                          11.6         173.5                        12
    ## 4                           5.4          67.1                         7
    ## 5                           4.2          40.9                         4
    ## 6                           1.1            NA                         4
    ## 7                           0.9          31.1                         4
    ## 8                           2.6          41.7                         4
    ## 9                           3.8          64.0                         6
    ## 10                          7.8         132.8                        11
    ## 11                          8.6         146.2                        12
    ## 12                         11.0         244.6                        NA
    ## 13                          0.9        1396.8                       111
    ##    Relative.Humidity Sunshine.Hours
    ## 1               76.8          170.0
    ## 2               76.7          168.2
    ## 3               76.8          179.5
    ## 4               75.9          177.3
    ## 5               76.2          176.1
    ## 6               75.7          175.6
    ## 7               72.5          188.9
    ## 8               69.1          186.2
    ## 9               69.2          158.8
    ## 10              74.0          148.8
    ## 11              73.8          161.5
    ## 12              76.8          155.0
    ## 13              74.5         2045.9

``` r
str(taubateMissing)
```

    ## 'data.frame':    13 obs. of  10 variables:
    ##  $ TAUBATE                     : chr  "Jan" "Feb" "Mar" "Apr" ...
    ##  $ Maximum.Absolute.Temperature: num  36.7 40.1 36.2 34.2 32.6 31 32.1 35.6 37.8 38 ...
    ##  $ Maximum.Average.Temperature : num  30.2 30.5 29.9 NA 25.4 24.6 24.4 26.4 27.6 27.5 ...
    ##  $ Average.Temperature         : num  23.3 23.5 22.9 20.8 18.1 16.7 16.4 18.2 20 20.7 ...
    ##  $ Minimum.Average.Temperature : num  17.7 17.8 17.8 16.1 14.2 12.9 12.6 14 15.7 NA ...
    ##  $ Minimum.Absolute.Temperature: num  10.9 12.6 11.6 5.4 4.2 1.1 0.9 2.6 3.8 7.8 ...
    ##  $ Rainfall..mm.               : num  233.5 192.1 173.5 67.1 40.9 ...
    ##  $ Days.with.Rainfall....1mm   : int  17 14 12 7 4 4 4 4 6 11 ...
    ##  $ Relative.Humidity           : num  76.8 76.7 76.8 75.9 76.2 75.7 72.5 69.1 69.2 74 ...
    ##  $ Sunshine.Hours              : num  170 168 180 177 176 ...

Which are the rows with complete cases?

``` r
complete.cases(taubateMissing)
```

    ##  [1]  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE
    ## [12] FALSE  TRUE

``` r
okdata <- subset(taubateMissing,complete.cases(taubateMissing))
str(okdata)
```

    ## 'data.frame':    9 obs. of  10 variables:
    ##  $ TAUBATE                     : chr  "Jan" "Feb" "Mar" "May" ...
    ##  $ Maximum.Absolute.Temperature: num  36.7 40.1 36.2 32.6 32.1 35.6 37.8 37.4 40.1
    ##  $ Maximum.Average.Temperature : num  30.2 30.5 29.9 25.4 24.4 26.4 27.6 28.7 27.7
    ##  $ Average.Temperature         : num  23.3 23.5 22.9 18.1 16.4 18.2 20 21.7 20.4
    ##  $ Minimum.Average.Temperature : num  17.7 17.8 17.8 14.2 12.6 14 15.7 16.9 15.8
    ##  $ Minimum.Absolute.Temperature: num  10.9 12.6 11.6 4.2 0.9 2.6 3.8 8.6 0.9
    ##  $ Rainfall..mm.               : num  233.5 192.1 173.5 40.9 31.1 ...
    ##  $ Days.with.Rainfall....1mm   : int  17 14 12 4 4 4 6 12 111
    ##  $ Relative.Humidity           : num  76.8 76.7 76.8 76.2 72.5 69.1 69.2 73.8 74.5
    ##  $ Sunshine.Hours              : num  170 168 180 176 189 ...
