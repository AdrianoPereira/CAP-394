Strings
================

-   [Splitting](#splitting)
-   [Joining](#joining)
-   [Regular Expressions](#regular-expressions)
    -   [grep](#grep)
    -   [gsub](#gsub)
    -   [gregexpr/regmatches](#gregexprregmatches)

Splitting
---------

``` r
name <- "Edgar Allan Poe"
names <- strsplit(name," ")
names
```

    ## [[1]]
    ## [1] "Edgar" "Allan" "Poe"

``` r
names <- unlist(names)
names
```

    ## [1] "Edgar" "Allan" "Poe"

``` r
length(names)
```

    ## [1] 3

``` r
head(names,n=1)
```

    ## [1] "Edgar"

``` r
tail(names,n=1)
```

    ## [1] "Poe"

Remember that everything can be vectors!

``` r
strsplit(c("a b c","d e f g","h","i j")," ")
```

    ## [[1]]
    ## [1] "a" "b" "c"
    ## 
    ## [[2]]
    ## [1] "d" "e" "f" "g"
    ## 
    ## [[3]]
    ## [1] "h"
    ## 
    ## [[4]]
    ## [1] "i" "j"

Joining
-------

"Edgar Allan Poe" -&gt; "Poe, E. A."

``` r
name <- "Edgar Allan Poe"
names <- unlist(strsplit(name," "))
parts <- length(names)
last <- tail(names,n=1)
firsts <- head(names,n=parts-1)
firsts
```

    ## [1] "Edgar" "Allan"

``` r
paste(last,firsts)
```

    ## [1] "Poe Edgar" "Poe Allan"

Remember vectors!

<b>EVIL CODE ALERT</b>

``` r
paste(substring(firsts, 1, 1),".",sep = "")
```

    ## [1] "E." "A."

``` r
paste(paste(substring(firsts, 1, 1),".",sep = ""),collapse = "")
```

    ## [1] "E.A."

``` r
paste(last,", ",paste(paste(substring(firsts, 1, 1),".",sep = ""),collapse = ""),sep="")
```

    ## [1] "Poe, E.A."

Regular Expressions
-------------------

### grep

``` r
names <- c("Edgar Allan Poe","Edgar Rice Burroughs","Alanis Morissette","Allan Quatermain")
grep("Allan",names)
```

    ## [1] 1 4

``` r
grep("^Allan",names)
```

    ## [1] 4

``` r
grep("Allan|Edgar",names)
```

    ## [1] 1 2 4

``` r
grep("^[Allan|Alan]",names)
```

    ## [1] 3 4

``` r
grep("n$",names)
```

    ## [1] 4

<tt>grepl</tt> may be more useful:

``` r
grepl("Allan",names)
```

    ## [1]  TRUE FALSE FALSE  TRUE

``` r
grepl("^Allan",names)
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
grepl("Allan|Edgar",names)
```

    ## [1]  TRUE  TRUE FALSE  TRUE

``` r
grepl("^[Allan|Alan]",names)
```

    ## [1] FALSE FALSE  TRUE  TRUE

``` r
grepl("n$",names)
```

    ## [1] FALSE FALSE FALSE  TRUE

### gsub

``` r
text <- "I think.... I hesitate... too.. much."
gsub(".","",text)
```

    ## [1] ""

``` r
gsub("\\.","",text)
```

    ## [1] "I think I hesitate too much"

``` r
gsub("[\\.]{2,}","",text)
```

    ## [1] "I think I hesitate too much."

### gregexpr/regmatches

``` r
text <- "...used 9920 pounds of flour, 3960 pounds of cheese, 1763.5 pounds of mushrooms, 1984 pounds of tomato puree, and 1984 pounds of chopped tomatoes..."
gregexpr("[0-9.]+",text)
```

    ## [[1]]
    ## [1]   1   9  31  54  82 115 146
    ## attr(,"match.length")
    ## [1] 3 4 4 6 4 4 3
    ## attr(,"useBytes")
    ## [1] TRUE

``` r
regmatches(text,gregexpr("[0-9.]+",text))
```

    ## [[1]]
    ## [1] "..."    "9920"   "3960"   "1763.5" "1984"   "1984"   "..."

``` r
numbers <- unlist(regmatches(text,gregexpr("[0-9.]+",text)))
as.numeric(numbers)
```

    ## Warning: NAs introduced by coercion

    ## [1]     NA 9920.0 3960.0 1763.5 1984.0 1984.0     NA
