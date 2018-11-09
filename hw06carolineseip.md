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
suppressPackageStartupMessages(library(stringi))
```

Find the stringi function that:
-------------------------------

1.  Counts the number of words in a sentence

Using a 'strsplit'

``` r
#Make a string of words, aka a sentence
string <- "Caribou are classified as a threatened species in Canada"
#Split the sentence by spaces, then find the length
sapply(strsplit(string, " "), length)
```

    ## [1] 9

There are 9 words in the sentence.

Using 'stri\_count\_fixed':

``` r
#Count the number of spaces in the sentence, plus one because there will always be one more word in a sentence than the number of spaces
stri_count_fixed(string, " ") + 1
```

    ## [1] 9

There are 9 words in the sentence

1.  Finds duplicated strings

``` r
stri_duplicated(c("n", "a", "t", "h", "a", "n"), fromLast = FALSE)
```

    ## [1] FALSE FALSE FALSE FALSE  TRUE  TRUE

There are two duplicate letters in the name Nathan, 'a' and 'n'.

1.
