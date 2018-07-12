Variables in R
================

-   [Assignments](#assignments)
-   [Reading Variables](#reading-variables)
-   [Listing and Removing Variables](#listing-and-removing-variables)

Assignments
-----------

These are three ways we can do assignments:

``` r
a <- 10
b = 20
30 -> c
```

Reading Variables
-----------------

These are some of the ways we can inspect the variables' values:

``` r
print(a)
```

    ## [1] 10

``` r
b
```

    ## [1] 20

``` r
cat(c)
```

    ## 30

Listing and Removing Variables
------------------------------

``` r
ls()
```

    ## [1] "a" "b" "c"

``` r
rm(b)
print(b)
```

    ## Error in print(b): object 'b' not found
