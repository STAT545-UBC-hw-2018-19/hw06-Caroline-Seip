hw06
================
Caroline Seip
2018-11-08

For this assignment I will be performing two tasks. First I will explore character data by reading and completing the exercises in the Strings chapter. Secondly I will write a function to convert Fahrenheit to Celsius.

Table of Contents
=================

-   Loading packages
-   Character Data
-   Writing Functions

Loading packages
================

Load the required packages:

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(stringr))
suppressPackageStartupMessages(library(stringi))
suppressPackageStartupMessages(library(testthat))
```

Task 1: Character Data
======================

Read and work the exercises in the Strings chapter
--------------------------------------------------

### Find the stringi function that:

#### Counts the number of words in a sentence

Using `strsplit`:

``` r
#Make a string of words, aka a sentence
string <- "Caribou are classified as a threatened species in Canada"
#Split the sentence by spaces, then find the length
sapply(strsplit(string, " "), length)
```

    ## [1] 9

There are 9 words in the sentence.

Using `stri_count_fixed`:

``` r
#Count the number of spaces in the sentence, plus one because there will always be 
#one more word in a sentence than the number of spaces
stri_count_fixed(string, " ") + 1
```

    ## [1] 9

There are 9 words in the sentence

#### Finds duplicated strings

Using `stri_duplicated`:

``` r
stri_duplicated(c("n", "a", "t", "h", "a", "n"), fromLast = FALSE)
```

    ## [1] FALSE FALSE FALSE FALSE  TRUE  TRUE

There are two duplicate letters in the name Nathan, "a" and "n".

#### Generate random text

Using `stri_rand_lipsum`:

``` r
#Generate one paragraph of random lorem ipsum text, don't start with lorem ipsum
stri_rand_lipsum(1, start_lipsum = FALSE)
```

    ## [1] "Efficitur non malesuada nec ac et, condimentum convallis ornare tempor. Egestas at ligula convallis senectus nibh a ac eros. Vestibulum ornare, non, ut dignissim at consequat duis in per. Tincidunt cursus eget sapien sed eu, sed vel aliquet, dapibus vel quis tincidunt. Cras dignissim non, ullamcorper torquent nulla lobortis. Porta leo leo, tincidunt justo lobortis, eu. Vel dolor suspendisse, amet interdum ad lorem tellus donec. Non eget ac sit diam sit parturient venenatis, consectetur, lectus, augue. Tempus at est semper ornare sed blandit velit. Ac in erat, tempor, quis tempus. Dapibus, quisque sed, et donec a imperdiet non. Felis pellentesque sed, tellus neque est eu nulla pellentesque quam. Tincidunt aenean, taciti leo eget urna. Viverra ut, in enim mi mauris eu pulvinar accumsan curae tempus. Vestibulum hac non dictum turpis sed sed."

### How do you control the language that 'stri\_sort' uses for sorting?

Specifying the `locale` in the `stri_sort` function allows us to change the language, for example:

``` r
#Sort letters, using American english
stri_sort(letters, locale="en_US")
```

    ##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q"
    ## [18] "r" "s" "t" "u" "v" "w" "x" "y" "z"

``` r
#Sort letters, using Lithuanian
stri_sort(letters, locale="lt_LT")
```

    ##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "y" "j" "k" "l" "m" "n" "o" "p"
    ## [18] "q" "r" "s" "t" "u" "v" "w" "x" "z"

If we specify Lithuanian, the letter "y" moves to between "i" and "j", instead of between "x" and "z".

Task 2: Writing Functions
=========================

Converting temperature data from remote wildlife cameras :camera: :bear: :deer:
-------------------------------------------------------------------------------

I have chosen to write a function to convert Fahrenheit to Celsius. This is useful for me because I use remote wildlife cameras that have internal thermometers to report temperature. The default setting on these cameras is Fahreneheit, so if the camera is not set up correctly the temperature will be reported in Fahrenheit, instead of Celsius.

The formula for converting Fahrenheit to Celsius is:

`C= (F-32)*(5/9)`

To test I will convert a commonly seen temperature on the cameras to Celsius (...it's northern Alberta :snowflake:)

``` r
#The input of 'FtoC' is temperature in Fahrenheit
FtoC <- function(f) {
#F to C formula
  c <- (f-32)*(5/9)
  #FtoC will return the temperature in Celsius
  return(c)
}
#Test the function by converting -30F to C
FtoC(-30)
```

    ## [1] -34.44444

-30F is equal to -34.4C. This was the expected result.

Now let's formally test the function `FtoC` using `testthat`:

32 degrees Fahrenheit should be equal to 0 degrees Celsius

``` r
test_that("Simple cases work", {
  expect_equal(FtoC(32), 0)
})
```

Seems happy! :smiley:

Now let's try to break the function:

``` r
FtoC("hello")
```

    ## Error in f - 32: non-numeric argument to binary operator

Great, it doesn't work on character data.

Let's update the `FtoC` function to throw a custom error if the input is not numeric:

``` r
FtoC <- function (f) {
  if (!is.numeric(f)) {
    stop(paste("Expecting f to be numeric, you gave me",
               typeof(f)))
  }
  (f-32)*(5/9)
}
FtoC("hello")
```

    ## Error in FtoC("hello"): Expecting f to be numeric, you gave me character

Nice! We have now made a custom error message for the `FtoC` function, so that it will only accept numeric data.
