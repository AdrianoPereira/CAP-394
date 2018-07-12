Downloading Files
================

-   [First: File System](#first-file-system)
    -   [Files and directories](#files-and-directories)
-   [Downloading Files](#downloading-files)
    -   [Reproducible Research](#reproducible-research)

First: File System
------------------

Where am I?

``` r
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive/INPE/CAP-394 Data Science/CAP-394"

Change working directory

``` r
orig <- getwd()
setwd("..")
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive/INPE/CAP-394 Data Science"

``` r
setwd("/Users/rafaelsantos/SYNC/OneDrive/")
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive"

``` r
setwd(orig)
getwd()
```

    ## [1] "/Users/rafaelsantos/SYNC/OneDrive/INPE/CAP-394 Data Science/CAP-394"

<b>This may reduce portability and compromise reproducibility!</b>

### Files and directories

``` r
file.exists("Data/Taubate.csv")
```

    ## [1] TRUE

``` r
file.exists("Data/TruthOrConsequences.csv")
```

    ## [1] FALSE

``` r
list.files("Data")
```

    ## [1] "SomeMixedData.R"    "Taubate-Fixed.R"    "Taubate-Fixed.csv" 
    ## [4] "Taubate.csv"        "TaubateMissing.csv"

``` r
file.info("Data/Taubate.csv")
```

    ##                  size isdir mode               mtime               ctime
    ## Data/Taubate.csv  829 FALSE  755 2018-07-12 11:56:59 2018-07-12 11:57:10
    ##                                atime uid gid        uname grname
    ## Data/Taubate.csv 2018-07-12 12:23:49 501  20 rafaelsantos  staff

``` r
tam <- file.info("Data/Taubate.csv")$size
tam
```

    ## [1] 829

``` r
age <- Sys.time()-(file.info("Data/Taubate.csv")$ctime)
age
```

    ## Time difference of 3.471215 hours

``` r
if (age > 7)
  {
  "Older than a week!"
  }
```

Conditional directory creation:

``` r
file.exists("TempData")
```

    ## [1] FALSE

``` r
if (!file.exists("TempData"))
  {
  dir.create("TempData")  
  }
file.exists("TempData")
```

    ## [1] TRUE

``` r
# Do something with directory...
aVector <- c(1,2,3)
dump("aVector", file = "TempData/aVector.R")
# CAREFUL HERE
unlink("TempData", recursive = TRUE, force = TRUE)
```

Downloading Files
-----------------

``` r
taubateURL <- "https://raw.githubusercontent.com/rafaeldcsantos/CAP-394/master/Data/Taubate.csv"
dir.create("TempData")  
download.file(taubateURL,destfile = "TempData/Taubate.csv",method="curl")
if (file.exists("TempData/Taubate.csv"))
  {
  tam <- file.info("TempData/Taubate.csv")$size
  paste("File downloaded, ",tam," bytes")
  } else
  {
  "Error downloading file!"
  }
```

    ## [1] "File downloaded,  829  bytes"

Nasty stuff about ways different OSs works, timeouts, etc. will not be covered.

### Reproducible Research

Remember to store the URL and the date you've downloaded the file.

Consider that results may be significantly different from what you'll provide!
