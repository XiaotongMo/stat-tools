This skill track includes 4 courses
## Introduction to R
finished!
no notes...


## intermediate R
### Conditionals and Control Flow

### Loops

### Functions

### The apply family
#### lapply
- 
- use lapply with a build-in R function
- use lapply with your own function
- lapply and anonymous functions
- use lapply with additional arguments
  ```r
  # Definition of split_low
  pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
  split <- strsplit(pioneers, split = ":")       # strsplit() is a build-in function, split is the result.
  split_low <- lapply(split, tolower)						 # lapply() can process a balk of inputs with the same function, tolower() is a build-in function to recall the lowercase of the string
  
  # Generic select function
  select_el <- function(x, index) {    # function() is to define user-own functions, select_el is a user own function.
    x[index]                           # ~[] is a build-in function that recall elements of the order of index in x 
  }
  
  # Use lapply() twice on split_low: names and years
  names<-lapply(split_low, select_el,index=1)
  years<-lapply(split_low, select_el,index=2)
  names
  years
  ```
  output
  ```r
  > names
  [[1]]
  [1] "gauss"

  [[2]]
  [1] "bayes"

  [[3]]
  [1] "pascal"

  [[4]]
  [1] "pearson"
  > years
  [[1]]
  [1] "1777"

  [[2]]
  [1] "1702"

  [[3]]
  [1] "1623"

  [[4]]
  [1] "1857"
  ```
- use lapply in
   ```r
   lapply(split_low, function(x) {
      if (nchar(x[1]) > 5) {
        return(NULL)
      } else {
        return(x[2])
      }
   })
   ```
#### sapply

- difference between `lapply` and `sapply`
  if input is a `n*m` list and output is a `n*1` list:  
  |function|lapply|sapply|
  | -- | -- | -- |
  |when the lengths of results are the same |a `n*m` list|a `n` vector|
  |when not|a list|a list|
    if input is a `n*m` list and output is a `n*p` list:  
  |function|lapply|sapply|
  | -- | -- | -- |
  |when the lengths of results are the same |a `n*m` list|a `n*p` matrix|
  |when not|a list|a list|
  For example,
  ```r
  # temp is already defined in the workspace
  
  # Finish function definition of extremes_avg
  extremes_avg <- function(x) {
    ( min(x) + max(x) ) / 2
  }
  
  # Apply extremes_avg() over temp using sapply()
  sapply(temp,extremes_avg)
  
  # Apply extremes_avg() over temp using lapply()
  lapply(temp,extremes_avg)
  ```
  output:
  ```r
  > sapply(temp,extremes_avg)
  [1] 4.0 9.0 2.5 2.5 5.5 3.0 5.0
  > lapply(temp,extremes_avg)
  [[1]]
  [1] 4
  
  [[2]]
  [1] 9
  
  [[3]]
  [1] 2.5
  
  [[4]]
  [1] 2.5
  
  [[5]]
  [1] 5.5
  
  [[6]]
  [1] 3
  
  [[7]]
  [1] 5
  ```

#### vapply

```r
vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = TRUE)
```

> Over the elements inside `X`, the function `FUN` is applied. The `FUN.VALUE` argument expects a template for the return argument of this function `FUN`. `USE.NAMES` is `TRUE` by default; in this case [`vapply()`](http://www.rdocumentation.org/packages/base/functions/lapply) tries to generate a named array, if possible.


|function|lapply|sapply|vapply|
| -- | -- | -- | -- |
|row names |no|Yes|Yes|
|what in the `apply` function|x, fun|x, fun|x, fun, fun.value, use.names=TRUE|
|difference|Format of results: list|Format of result: vector, matrix (sometimes, list)|Like `sapply`, but will according to fun.value  `numeric(p)` which means the length is p.|

>  `vapply()` can be considered a more robust version of `sapply()`, because you explicitly restrict the output of the function you want to apply.

- sapply <-->vapply

```r
# compare the mean of elements in x and the value of y
## sapply
sapply(temp, function(x,y){ mean(x) > y}, y = 5)
## vapply
vapply(temp, function(x,y){ mean(x) > y}, y = 5, logical(1))
# 
```

### Utilities

> Mastering R programming is not only about understanding its programming concepts. Having a solid understanding of a wide range of R functions is also important. This chapter introduces you to many useful functions for data structure manipulation, regular expressions, and working with times and dates.

#### Mathematical utilities

> Have another look at some useful math functions that R features:
>
> `abs()`: Calculate the absolute value.
> `sum()`: Calculate the sum of all the values in a data structure.
> `mean()`: Calculate the arithmetic mean.
> `round()`: Round the values to 0 decimal places by default. Try out ?round in the console for variations of round() and ways to change the number of digits to round to.
>
> As a data scientist in training, you've estimated a regression model on the sales data for the past six months. After evaluating your model, you see that the training error of your model is quite regular, showing both positive and negative values. The error values are already defined in the workspace on the right (errors).

#### Data Utilities

> R features a bunch of functions to juggle around with data structures::
>
> `seq()`: Generate sequences, by specifying the from, to, and by arguments.
> `rep()`: Replicate elements of vectors and lists.
> `sort()`: Sort a vector in ascending order. Works on numerics, but also on character strings and logicals.
> `rev()`: Reverse the elements in a data structures for which reversal is defined.
> `str()`: Display the structure of any R object.
> `append()`: Merge vectors or lists.
> `is.*()`: Check for the class of an R object.
> `as.*()`: Convert an R object from one class to another.
> `unlist()`: Flatten (possibly embedded) lists to produce a vector.
>
> Remember the social media profile views data? Your LinkedIn and Facebook view counts for the last seven days are already defined as lists on the right.

For example

```r
# The linkedin and facebook lists have already been created for you
linkedin <- list(16, 9, 13, 5, 2, 17, 14)
facebook <- list(17, 7, 5, 16, 8, 13, 14)

# Convert linkedin and facebook to a vector: li_vec and fb_vec
li_vec<- unlist(linkedin)         
fb_vec<- unlist(facebook)

# Append fb_vec to li_vec: social_vec
social_vec <- append(li_vec, fb_vec)

# Sort social_vec
#rev(sort(social_vec))
sort(social_vec, decreasing = TRUE)
```

- `unlist` can change  a list to a vector, with a flattening method.

  before

  ```r
  > linkedin
  [[1]]
  [1] 16

  [[2]]
  [1] 9

  [[3]]
  [1] 13

  [[4]]
  [1] 5

  [[5]]
  [1] 2

  [[6]]
  [1] 17

  [[7]]
  [1] 14
  ```

  After (flattened)

  ```r
  > li_vec
  [1] 16  9 13  5  2 17 14
  ```




