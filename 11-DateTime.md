Date and Time
================

-   [Date and Time](#date-and-time)
    -   [Creating](#creating)
    -   [Converting from strings](#converting-from-strings)
    -   [Extracting fields from date and time](#extracting-fields-from-date-and-time)
-   [Operations with date and time](#operations-with-date-and-time)

Date and Time
-------------

### Creating

"Now":

``` r
today <- Sys.Date()
today
```

    ## [1] "2018-07-12"

``` r
class(today)
```

    ## [1] "Date"

``` r
now <- Sys.time()
now
```

    ## [1] "2018-07-12 15:23:23 -03"

``` r
class(now)
```

    ## [1] "POSIXct" "POSIXt"

### Converting from strings

Dates in format YMD are easy:

``` r
monday <- as.Date("2017-07-03")
monday
```

    ## [1] "2017-07-03"

``` r
class(monday)
```

    ## [1] "Date"

Other formats can be parsed.

``` r
aDate <- "04/07/2017"
tuesday <- as.Date(aDate, "%d/%m/%Y")
tuesday
```

    ## [1] "2017-07-04"

``` r
class(tuesday)
```

    ## [1] "Date"

<tt>as.Date</tt> ignores time (or does it?)

``` r
mondayMorning <- as.Date("2017-07-03 05:30:00")
mondayMorning
```

    ## [1] "2017-07-03"

``` r
class(mondayMorning)
```

    ## [1] "Date"

Converting date and time with <tt>strptime</tt>:

``` r
aDate <- "04/07/2017"
tuesday <- strptime(aDate, "%d/%m/%Y")
tuesday
```

    ## [1] "2017-07-04 -03"

``` r
class(tuesday)
```

    ## [1] "POSIXlt" "POSIXt"

``` r
tuesdayMorning <- strptime("04/07/2017 at 05:20:17", "%d/%m/%Y at %H:%M:%S")
tuesdayMorning
```

    ## [1] "2017-07-04 05:20:17 -03"

``` r
class(tuesdayMorning)
```

    ## [1] "POSIXlt" "POSIXt"

### Extracting fields from date and time

``` r
tuesdayMorning
```

    ## [1] "2017-07-04 05:20:17 -03"

``` r
tM <- as.POSIXlt(tuesdayMorning)
tM$sec
```

    ## [1] 17

``` r
tM$wday
```

    ## [1] 2

You can get fields for sec, min, hour, mday (day of the month), mon (months after the first of the year), year (since 1900), wday (0-6, 0=Sunday), yday (day of year), isdst (DST).

Operations with date and time
-----------------------------

``` r
birthEAP <- as.Date("1809/01/19")
today <- Sys.Date()
diff <- today-birthEAP
diff
```

    ## Time difference of 76510 days

``` r
class(diff)
```

    ## [1] "difftime"

``` r
today <- Sys.Date()
future <- today+100 # days
future
```

    ## [1] "2018-10-20"

``` r
class(future)
```

    ## [1] "Date"

There are more flexible ways: StockOverflow is your friend! <https://stackoverflow.com/questions/14454476/get-the-difference-between-dates-in-terms-of-weeks-months-quarters-and-years>
