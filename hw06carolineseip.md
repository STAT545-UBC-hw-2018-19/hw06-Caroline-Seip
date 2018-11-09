hw06
================
Caroline Seip
2018-11-08

For this assignment I will be performing 2 tasks

Strings
=======

Load the required packages:

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(stringr))
```

Find the stringi function that:

1.  Counts the number of words in a sentence

``` r
#Make a string of words, aka a sentence
string <- "Caribou are classified as a threatened species in Canada"
#Split the sentence by spaces, then find the length
sapply(strsplit(string, " "), length)
```

    ## [1] 9

I used the function 'strsplit' to find the number of words in the sentence.
