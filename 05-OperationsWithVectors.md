Operations with Vectors
================

-   [Basic Operations with Vectors](#basic-operations-with-vectors)
    -   [Accessing Elements in a Vector](#accessing-elements-in-a-vector)
    -   [Mathematical Operations in Vectors](#mathematical-operations-in-vectors)
-   [Recycling Rule](#recycling-rule)
-   [Missing Data in Vectors](#missing-data-in-vectors)
    -   [Filtering by NAs](#filtering-by-nas)

Basic Operations with Vectors
-----------------------------

This is the monthly average temperature in Baltimore (from <http://www.rssweather.com/climate/Maryland/Baltimore/>)

``` r
tempHi <- c(41.2,44.8,53.9,64.5,73.9,82.7,87.2,85.1,78.2,67.0,56.3,46.0)
tempHi
```

    ##  [1] 41.2 44.8 53.9 64.5 73.9 82.7 87.2 85.1 78.2 67.0 56.3 46.0

We can label the vectors' elements!

``` r
months <- c("Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec")
names(tempHi) <- months
tempHi
```

    ##  Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec 
    ## 41.2 44.8 53.9 64.5 73.9 82.7 87.2 85.1 78.2 67.0 56.3 46.0

Other way to do this:

``` r
otherTemp <- c(Jan=41.2,Feb=44.8,Mar=53.9,Apr=64.5,May=73.9,Jun=82.7,
               Jul=87.2,Aug=85.1,Sep=78.2,Oct=67.0,Nov=56.3,Dec=46.0)
otherTemp
```

    ##  Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec 
    ## 41.2 44.8 53.9 64.5 73.9 82.7 87.2 85.1 78.2 67.0 56.3 46.0

``` r
names(otherTemp)
```

    ##  [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov"
    ## [12] "Dec"

Let's also get the lower temperatures:

``` r
tempLo <- c(23.5,26.1,33.6,42.0,51.8,60.8,65.8,63.9,56.6,43.7,34.7,27.3)
```

Now we can do simple operations on the whole vectors.

``` r
range <- tempHi-tempLo
range
```

    ##  Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec 
    ## 17.7 18.7 20.3 22.5 22.1 21.9 21.4 21.2 21.6 23.3 21.6 18.7

Convert it to Celsius:

``` r
tempHiC <- (5/9) * (tempHi - 32)
tempHiC
```

    ##       Jan       Feb       Mar       Apr       May       Jun       Jul 
    ##  5.111111  7.111111 12.166667 18.055556 23.277778 28.166667 30.666667 
    ##       Aug       Sep       Oct       Nov       Dec 
    ## 29.500000 25.666667 19.444444 13.500000  7.777778

Is this month too cold?

``` r
tooCold <- (((5/9) * (tempLo - 32)) < 0)
tooCold
```

    ##  [1]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [12]  TRUE

### Accessing Elements in a Vector

By indexes:

``` r
tempHi[7] # July
```

    ##  Jul 
    ## 87.2

``` r
tempHi[12] # December
```

    ## Dec 
    ##  46

By ranges:

``` r
tempHi[7:9] # July-September
```

    ##  Jul  Aug  Sep 
    ## 87.2 85.1 78.2

By lists:

``` r
tempHi[c(11:12,1:2)] # Nov-Feb
```

    ##  Nov  Dec  Jan  Feb 
    ## 56.3 46.0 41.2 44.8

By sequences:

``` r
tempHi[seq(2,12,2)] # Even months
```

    ##  Feb  Apr  Jun  Aug  Oct  Dec 
    ## 44.8 64.5 82.7 85.1 67.0 46.0

Subsetting:

``` r
tempHiC[tempHiC > 20] 
```

    ##      May      Jun      Jul      Aug      Sep 
    ## 23.27778 28.16667 30.66667 29.50000 25.66667

### Mathematical Operations in Vectors

``` r
min(tempHiC)
```

    ## [1] 5.111111

``` r
max(tempHiC)
```

    ## [1] 30.66667

``` r
mean(tempHiC)
```

    ## [1] 18.37037

``` r
sd(tempHiC)
```

    ## [1] 9.178011

Subsetting (again):

``` r
tempHiC[tempHiC > mean(tempHiC)] 
```

    ##      May      Jun      Jul      Aug      Sep      Oct 
    ## 23.27778 28.16667 30.66667 29.50000 25.66667 19.44444

Recycling Rule
--------------

Suppose a simple model for global warming:

``` r
hotter <- tempHiC + 10
hotter
```

    ##      Jan      Feb      Mar      Apr      May      Jun      Jul      Aug 
    ## 15.11111 17.11111 22.16667 28.05556 33.27778 38.16667 40.66667 39.50000 
    ##      Sep      Oct      Nov      Dec 
    ## 35.66667 29.44444 23.50000 17.77778

``` r
hotter-tempHiC
```

    ## Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec 
    ##  10  10  10  10  10  10  10  10  10  10  10  10

It's not going to be linear... let's try a more sensible one:

``` r
hotter <- tempHiC + c(3,3,2,2,2,1,1,1,1,2,2,3)
hotter
```

    ##       Jan       Feb       Mar       Apr       May       Jun       Jul 
    ##  8.111111 10.111111 14.166667 20.055556 25.277778 29.166667 31.666667 
    ##       Aug       Sep       Oct       Nov       Dec 
    ## 30.500000 26.666667 21.444444 15.500000 10.777778

``` r
hotter-tempHiC
```

    ## Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec 
    ##   3   3   2   2   2   1   1   1   1   2   2   3

So we can add a scalar and a vector to another vector. What if they're not the same size?

``` r
hotter <- tempHiC + c(3,2,1)
hotter
```

    ##       Jan       Feb       Mar       Apr       May       Jun       Jul 
    ##  8.111111  9.111111 13.166667 21.055556 25.277778 29.166667 33.666667 
    ##       Aug       Sep       Oct       Nov       Dec 
    ## 31.500000 26.666667 22.444444 15.500000  8.777778

``` r
hotter-tempHiC
```

    ## Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec 
    ##   3   2   1   3   2   1   3   2   1   3   2   1

The *Recycling Rule* states that the shorter vector values' are recycled. We get warnings when the lenght of the longer is not a multiple of the lenght of the shorter.

``` r
hotter <- tempHiC + c(3,2,1,0,-1)
```

    ## Warning in tempHiC + c(3, 2, 1, 0, -1): longer object length is not a
    ## multiple of shorter object length

``` r
hotter
```

    ##       Jan       Feb       Mar       Apr       May       Jun       Jul 
    ##  8.111111  9.111111 13.166667 18.055556 22.277778 31.166667 32.666667 
    ##       Aug       Sep       Oct       Nov       Dec 
    ## 30.500000 25.666667 18.444444 16.500000  9.777778

``` r
hotter-tempHiC
```

    ## Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec 
    ##   3   2   1   0  -1   3   2   1   0  -1   3   2

Missing Data in Vectors
-----------------------

``` r
avgTempSJC <- c(22.2,22.4,21.6,19.6,17,16.1,NA,17.1,18.8,19.4,20.3,21.4)
names(avgTempSJC) <- c("Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec")
avgTempSJC
```

    ##  Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec 
    ## 22.2 22.4 21.6 19.6 17.0 16.1   NA 17.1 18.8 19.4 20.3 21.4

Problems with some operators when some values are NAs:

``` r
min(avgTempSJC)
```

    ## [1] NA

``` r
max(avgTempSJC)
```

    ## [1] NA

``` r
mean(avgTempSJC)
```

    ## [1] NA

``` r
sd(avgTempSJC)
```

    ## [1] NA

We need to be clear about the existence of NAs:

``` r
min(avgTempSJC,na.rm = TRUE)
```

    ## [1] 16.1

``` r
max(avgTempSJC,na.rm = TRUE)
```

    ## [1] 22.4

``` r
mean(avgTempSJC,na.rm = TRUE)
```

    ## [1] 19.62727

``` r
sd(avgTempSJC,na.rm = TRUE)
```

    ## [1] 2.196857

### Filtering by NAs

``` r
is.na(avgTempSJC)
```

    ##   Jan   Feb   Mar   Apr   May   Jun   Jul   Aug   Sep   Oct   Nov   Dec 
    ## FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE

``` r
!is.na(avgTempSJC)
```

    ##   Jan   Feb   Mar   Apr   May   Jun   Jul   Aug   Sep   Oct   Nov   Dec 
    ##  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE

``` r
avgTempSJC[is.na(avgTempSJC)]
```

    ## Jul 
    ##  NA

``` r
avgTempSJC[!is.na(avgTempSJC)]
```

    ##  Jan  Feb  Mar  Apr  May  Jun  Aug  Sep  Oct  Nov  Dec 
    ## 22.2 22.4 21.6 19.6 17.0 16.1 17.1 18.8 19.4 20.3 21.4
