Control
================

-   [Conditionals](#conditionals)
-   [Loops](#loops)
    -   [Skipping steps: next](#skipping-steps-next)
-   [Major annoyance!](#major-annoyance)

Conditionals
------------

``` r
avgTempSJC <- c(22.2,22.4,21.6,19.6,17,16.1,15.6,17.1,18.8,19.4,20.3,21.4)
names(avgTempSJC) <- c("Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec")

if (avgTempSJC["Jan"] > 20) 
  {
  "Good!"
  } else {
  "Bad!"
  }
```

    ## [1] "Good!"

We can assign results of conditionals to variables.

``` r
weatherJan <- if (avgTempSJC["Jan"] > 20) {
  "Good!"
} else {
  "Bad!"
}
weatherJan
```

    ## [1] "Good!"

Remember: think in vectors! Simple IFs don't work with vectors...

``` r
if (avgTempSJC > 20) {
  "Good!"
} else {
  "Bad!"
}
```

    ## Warning in if (avgTempSJC > 20) {: the condition has length > 1 and only
    ## the first element will be used

    ## [1] "Good!"

... but this works:

``` r
weather <- ifelse((avgTempSJC > 20), "Good","Bad")
weather
```

    ##    Jan    Feb    Mar    Apr    May    Jun    Jul    Aug    Sep    Oct 
    ## "Good" "Good" "Good"  "Bad"  "Bad"  "Bad"  "Bad"  "Bad"  "Bad"  "Bad" 
    ##    Nov    Dec 
    ## "Good" "Good"

Loops
-----

Fors...

``` r
for(i in 1:12) {
  print(avgTempSJC[i])
}
```

    ##  Jan 
    ## 22.2 
    ##  Feb 
    ## 22.4 
    ##  Mar 
    ## 21.6 
    ##  Apr 
    ## 19.6 
    ## May 
    ##  17 
    ##  Jun 
    ## 16.1 
    ##  Jul 
    ## 15.6 
    ##  Aug 
    ## 17.1 
    ##  Sep 
    ## 18.8 
    ##  Oct 
    ## 19.4 
    ##  Nov 
    ## 20.3 
    ##  Dec 
    ## 21.4

``` r
for(month in avgTempSJC) {
  print(month)
}
```

    ## [1] 22.2
    ## [1] 22.4
    ## [1] 21.6
    ## [1] 19.6
    ## [1] 17
    ## [1] 16.1
    ## [1] 15.6
    ## [1] 17.1
    ## [1] 18.8
    ## [1] 19.4
    ## [1] 20.3
    ## [1] 21.4

... and whiles too!

``` r
count = 1
while(count <= 12) {
  print(avgTempSJC[count])
  count <- count+1
}
```

    ##  Jan 
    ## 22.2 
    ##  Feb 
    ## 22.4 
    ##  Mar 
    ## 21.6 
    ##  Apr 
    ## 19.6 
    ## May 
    ##  17 
    ##  Jun 
    ## 16.1 
    ##  Jul 
    ## 15.6 
    ##  Aug 
    ## 17.1 
    ##  Sep 
    ## 18.8 
    ##  Oct 
    ## 19.4 
    ##  Nov 
    ## 20.3 
    ##  Dec 
    ## 21.4

Other loop: repeat

``` r
count = 1
repeat {
  if (count > 12) {
    break
  } else {
    print(avgTempSJC[count])
    count <- count+1
  }
}
```

    ##  Jan 
    ## 22.2 
    ##  Feb 
    ## 22.4 
    ##  Mar 
    ## 21.6 
    ##  Apr 
    ## 19.6 
    ## May 
    ##  17 
    ##  Jun 
    ## 16.1 
    ##  Jul 
    ## 15.6 
    ##  Aug 
    ## 17.1 
    ##  Sep 
    ## 18.8 
    ##  Oct 
    ## 19.4 
    ##  Nov 
    ## 20.3 
    ##  Dec 
    ## 21.4

### Skipping steps: next

``` r
for(i in 1:12) 
  {
  if (avgTempSJC[i] > 20) { next }
  print(avgTempSJC[i])
  }
```

    ##  Apr 
    ## 19.6 
    ## May 
    ##  17 
    ##  Jun 
    ## 16.1 
    ##  Jul 
    ## 15.6 
    ##  Aug 
    ## 17.1 
    ##  Sep 
    ## 18.8 
    ##  Oct 
    ## 19.4

Major annoyance!
----------------

This works:

``` r
if (avgTempSJC["Jan"] > 20) 
  {
  "Good!"
  } else {
  "Bad!"
  }
```

    ## [1] "Good!"

This too:

``` r
if (avgTempSJC["Jan"] > 20) { "Good!" } else { "Bad!" }
```

    ## [1] "Good!"

This doesn't:

``` r
if (avgTempSJC["Jan"] > 20) 
  { "Good!" } 
  else { "Bad!" }
```

    ## Error: <text>:3:3: unexpected 'else'
    ## 2:   { "Good!" } 
    ## 3:   else
    ##      ^
