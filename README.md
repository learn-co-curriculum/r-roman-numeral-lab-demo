# Roman Numerals with R

In this lab you will be writing an R Function `convert_to_roman` that will convert an Integer into a Roman Numeral. 

## Structure

- `tests/test_input_argument_validity.R`, the current tests used for validity of input argument.  
- `tests/test_roman_numeral_conversiona.R`, the current tests used for converstions.  
- `code/roman_numeral.R`, where to implement your function.

In order to be able to run the example the following packages need to be locally installed

- the `testthat` package used for unit testing.

```r
#Using the CRAN repo
install.packages("checkpoint")
install.packages("testthat")
```

## Running the Tests

You can run the tests with `auto_test()` or by running `learn.R` from the command line or RSTudio.

## Walkthrough

### Getting Started

__Think about the design of the code__, in this case the function that we want to develop  

* where to put the function, e.g folder, file
* name of the function
* function parameter(s)
    * what type of parameter(s)
    * any assumption(s) on the possible values

__Implement the shell of the function__ , with a very simplicistic implementation 

* it accept an argument (any type)
* it returns a "I" value (hardcoded simplification)


```r
convert_to_roman <- function(num){
  return("I")
}
```

__The TDD mindset__, before writing any code 

* write a failing test, and then 
* make the simplest change to the code in order to make it pass (cut & paste allowed)
* re-run all tests, and when all tests are passing
* refactor the existing code using the tests as a safety net
* repeat for a new test condition


### Step 1, the argument must be integer otherwise an exception is thrown

(1) Create a test passing as argument a non numeric/ integer (e.g. 1) - expecting an error

* Add expectation: pass 1 return an error
    * Will fail cause an error is not thrown

```r
#Add expectation
context("Input Argument Validity")

test_that("passing a non numeric/ integer an exception is thrown",{
  expect_error(object = convert_to_roman(1))
})
}
```

* Modify the code in order to make it pass
            
```r
#Modify the code
convert_to_roman <- function(num){
  if(!is.integer(num)) stop("must be integer")
  return("I")
}
```

* Add expectation: pass 3.14 return an error
    * Will pass (same condition as before just a different argument)
    
```r
#Add expectations
context("Input Argument Validity")

test_that("passing a non numeric/ integer an exception is thrown",{
  expect_error(object = convert_to_roman(1))
  expect_error(object = convert_to_roman(3.14))
})
```
    
* Add expectation: pass a string return an error
    * Will pass (same condition as before just a different type for argument)

```r
#Add expectations
context("Input Argument Validity")

test_that("passing a non numeric/ integer an exception is thrown",{
  expect_error(object = convert_to_roman(1))
  expect_error(object = convert_to_roman(3.14))
  expect_error(object = convert_to_roman("test"))
})
```

(2) Create a test passing as argument a numeric/ integer (e.g. 1L) - expecting roman numeral "I"

* Add expectation: pass 1L return "I"
    * Will pass ("I" is hradcoded)

```r
context("Input Argument Validity")

test_that("passing a non numeric/ integer an exception is thrown",{
  expect_error(object = convert_to_roman(1))
  expect_error(object = convert_to_roman(3.14))
  expect_error(object = convert_to_roman("test"))
})

test_that("passing a numeric/ integer no exception thrown",{
  expect_match(object = convert_to_roman(1L), regexp = "^I$")
})
```



### Step 2, passing an integer the correct roman numeral is returned

(3) Create a test passing as argument an integer between [1..3]

* Add expectation: pass 1L return "I" 
    * Should pass cause already coverend in (2)

```r
#Create a new context, a new test and add expectation
context("Roman Numeral Conversion")

test_that("passing an integer between [1..3] the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(1L), regexp = "^I$")
})
```

* Add expectation: pass 2L return "II"
    * Will fail cause wrong roman numeral is returned

```r
#Create a new context, a new test and add expectation
context("Roman Numeral Conversion")

test_that("passing an integer between [1..3] the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(1L), regexp = "^I$")
  expect_match(object = convert_to_roman(2L), regexp = "^II$")
})
```

* Modify the code in order to make it pass 

```r
#Modify the code
convert_to_roman <- function(num){
  if(!is.integer(num)) stop("must be integer")
  if (num == 1L) return("I")
  if (num == 2L) return("II")
}
```

Repeat for 3 return "III": add expectation (make the test fail) and modify the code (make the test pass)

```r
#Create a new context, a new test and add expectation
context("Roman Numeral Conversion")

test_that("passing an integer between [1..3] the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(1L), regexp = "^I$")
  expect_match(object = convert_to_roman(2L), regexp = "^II$")
  expect_match(object = convert_to_roman(3L), regexp = "^III$")
})
```

```r
#Modify the code
convert_to_roman <- function(num){
  if(!is.integer(num)) stop("must be integer")
  if (num == 1L) return("I")
  if (num == 2L) return("II")
  if (num == 3L) return("III")
}
```

(4) Create a test passing as argument a particular integer 4

* Add expectation: pass 4L return "IV" 
    * Will fail cause wrong roman numeral is returned

```r
#Add a new test and add expectation
context("Roman Numeral Conversion")

test_that("passing an integer between [1..3] the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(1L), regexp = "^I$")
  expect_match(object = convert_to_roman(2L), regexp = "^II$")
  expect_match(object = convert_to_roman(3L), regexp = "^III$")
})

test_that("passing an integer 4 the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(4L), regexp = "^IV$")
})
```

* Modify the code in order to make it pass

```r
#Modify the code
convert_to_roman <- function(num){
  if(!is.integer(num)) stop("must be integer")
  if (num == 1L) return("I")
  if (num == 2L) return("II")
  if (num == 3L) return("III")
  if (num == 4L) return("IV")
}
```

(5) Create a test passing as argument a particular integer 5

* Add expectation: pass 5L return "V" 
    * Will fail cause wrong roman numeral is returned
* Modify the code in order to make it pass

Continue one simple step at a time ..... 

Note that the code implementing that function is shaped incrementally, one smal step after the other. Using this simple approach the final tests and code will look like

```r
#Test for the conversion [1..10]
context("Roman Numeral Conversion")

test_that("passing an integer between [1..3] the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(1L), regexp = "^I$")
  expect_match(object = convert_to_roman(2L), regexp = "^II$")
  expect_match(object = convert_to_roman(3L), regexp = "^III$")
})

test_that("passing an integer 4 the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(4L), regexp = "^IV$")
})

test_that("passing an integer 5 the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(5L), regexp = "^V$")
})

test_that("passing an integer between [6..8] the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(6L), regexp = "^VI$")
  expect_match(object = convert_to_roman(7L), regexp = "^VII$")
  expect_match(object = convert_to_roman(8L), regexp = "^VIII$")
})

test_that("passing an integer 9 the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(9L), regexp = "^IX$")
})

test_that("passing an integer 10 the correct roman numeral is returned",{
  expect_match(object = convert_to_roman(10L), regexp = "^X$")
})
```

```r
#Simplest code possible to pass the tests
convert_to_roman <- function(num){
  if(!is.integer(num)) stop("must be integer")

  if(num == 1L) return("I")
  if(num == 2L) return("II")
  if(num == 3L) return("III")
  if(num == 4L) return("IV")
  if(num == 5L) return("V")
  if(num == 6L) return("VI")
  if(num == 7L) return("VII")
  if(num == 8L) return("VIII")
  if(num == 9L) return("IX")
  if(num == 10L) return("X")
}
```

Once we have a test harness around the code we can __start to refactor the code__ in order to get a more general and flexible solution

* change the code/ refactor
* run all tests and make them pass
* repeat till you are satisfied

```r
convert_to_roman <- function(num){
  if(!is.integer(num)) stop("must be integer")

  roman_numeral <- NULL
  decimal_values <- c(10L, 9L, 5L,4L, 1L)
  roman_numerals <- c("X", "IX", "V","IV", "I")

  for (i in 1: length(decimal_values)){
    while(decimal_values[i] <= num){
      roman_numeral <- paste(roman_numeral, roman_numerals[i], sep = "")
      num <- num - decimal_values[i]
    }
  }
  return(roman_numeral)
}
```
