---
title: "Programming"
author: 
date: 
urlcolor: blue
output: 
  html_document:
    toc: true
    toc_depth: 3
    toc_float: true # toc_float option to float the table of contents to the left of the main document content. floating table of contents will always be visible even when the document is scrolled
      #collapsed: false # collapsed (defaults to TRUE) controls whether the TOC appears with only the top-level (e.g., H2) headers. If collapsed initially, the TOC is automatically expanded inline when necessary
      #smooth_scroll: true # smooth_scroll (defaults to TRUE) controls whether page scrolls are animated when TOC items are navigated to via mouse clicks
    number_sections: true
    fig_caption: true # ? this option doesn't seem to be working for figure inserted below outside of r code chunk    
    highlight: tango # Supported styles include "default", "tango", "pygments", "kate", "monochrome", "espresso", "zenburn", and "haddock" (specify null to prevent syntax    
    theme: default # theme specifies the Bootstrap theme to use for the page. Valid themes include default, cerulean, journal, flatly, readable, spacelab, united, cosmo, lumen, paper, sandstone, simplex, and yeti.
    df_print: tibble #options: default, tibble, paged
    keep_md: true # may be helpful for storing on github
    
---


# Introduction

Load packages:


```r
library(tidyverse)
```

# Foundational concepts

## Data structures and types

What is an **object**?

- Everything in R is an object
- We can classify objects based on their _class_ and _type_
- The _class_ of the object determines what kind of functions we can apply to it
  - E.g., "Date" functions usually only work on objects with a `Date` class
  - E.g., "String" functions usually only work with on objects with a `character` class
  - E.g., Functions that do mathematical computation usually work on objects with a `numeric` class
- Objects may be combined to form data structures

<br>
<details><summary>Class and object-oriented programming</summary>

> "Object-oriented programming (OOP) refers to a type of computer programming in which programmers define not only the data type of a data structure, but also the types of operations (functions) that can be applied to the data structure."

*Source: [Webopedia](https://www.webopedia.com/TERM/O/object_oriented_programming_OOP.html)*

<br>
R is an **object-oriented programming language**:

- The _class_ of an object is fundamental to object-oriented programming because:
  - It determines which functions can be applied to the object
  - It also determines what those functions do to the object
    - E.g., A specific function might do one thing to objects of __class__ A and another thing to objects of __class__ B
    - What a function does to objects of different class is determined by whoever wrote the function
- Many different object classes exist in R
- You can also create our own classes
    - E.g., The `labelled` class is an object class created by Hadley Wickham when he created the `haven` package
- In this course we will work with classes that have been created by others

</details>
<br>

[![](https://d33wubrfki0l68.cloudfront.net/1d1b4e1cf0dc5f6e80f621b0225354b0addb9578/6ee1c/diagrams/data-structures-overview.png){width=400px}](https://r4ds.had.co.nz/vectors.html)

*Credit: [R for Data Science](https://r4ds.had.co.nz/vectors.html)*

<br>
Basic **data structures**:

- [Atomic vectors](#atomtic-vectors)
- [Lists](#lists)
  - [Dataframes](#dataframes)
  
Basic **data types**:

- Logical (`TRUE`, `FALSE`)
- Numeric (e.g., `5`, `2.5`)
- Integer (e.g., `1L`, `4L`, where `L` tells R to store as `integer` type)
- Character (e.g., `"R is fun"`)

Functions for investigating R objects (From [Data Types and Structures](https://swcarpentry.github.io/r-novice-inflammation/13-supp-data-structures/))

- `str()`: Compactly display the internal structure of an R object
- `class()`: What kind of object is it (high-level)?
- `typeof()`: What is the object's data type (low-level)?

### Atomtic vectors

What are **atomic vectors**?

- **Atomic vectors** are objects that contains elements
- Elements must be of the same data type (i.e., _homogeneous_)
- Elements can be named to form a _named atomic vector_
- The `class()` and `typeof()` a vector describes the elements it contains

<br>
<details><summary>**Example**: Investigating logical vectors</summary>


```r
v <- c(TRUE, FALSE, FALSE, TRUE)
str(v)
```

```
##  logi [1:4] TRUE FALSE FALSE TRUE
```

```r
class(v)
```

```
## [1] "logical"
```

```r
typeof(v)
```

```
## [1] "logical"
```

</details>

<br>
<details><summary>**Example**: Investigating numeric vectors</summary>


```r
v <- c(1, 3, 5, 7)
str(v)
```

```
##  num [1:4] 1 3 5 7
```

```r
class(v)
```

```
## [1] "numeric"
```

```r
typeof(v)
```

```
## [1] "double"
```
</details>

<br>
<details><summary>**Example**: Investigating integer vectors</summary>


```r
v <- c(1L, 3L, 5L, 7L)
str(v)
```

```
##  int [1:4] 1 3 5 7
```

```r
class(v)
```

```
## [1] "integer"
```

```r
typeof(v)
```

```
## [1] "integer"
```

</details>

<br>
<details><summary>**Example**: Investigating character vectors</summary>

Each element in a `character` vector is a **string** (covered in next section):


```r
v <- c("a", "b", "c", "d")
str(v)
```

```
##  chr [1:4] "a" "b" "c" "d"
```

```r
class(v)
```

```
## [1] "character"
```

```r
typeof(v)
```

```
## [1] "character"
```

</details>

<br>
<details><summary>**Example**: Investigating named vectors</summary>


```r
v <- c(v1 = 1, v2 = 2, v3 = 3)
v
```

```
## v1 v2 v3 
##  1  2  3
```

```r
str(v)
```

```
##  Named num [1:3] 1 2 3
##  - attr(*, "names")= chr [1:3] "v1" "v2" "v3"
```

```r
class(v)
```

```
## [1] "numeric"
```

```r
typeof(v)
```

```
## [1] "double"
```

</details>


### Lists

What are **lists**?

- **Lists** are objects that contains elements
- Elements do not need to be of the same type (i.e., _heterogeneous_)
  - Elements can be atomic vectors or even other lists
- Elements can be named to form a _named list_
- The `class()` and `typeof()` a list is `list`

<br>
<details><summary>**Example**: Investigating heterogeneous lists</summary>


```r
l <- list(2.5, "abc", TRUE, c(1L, 2L, 3L))
str(l)
```

```
## List of 4
##  $ : num 2.5
##  $ : chr "abc"
##  $ : logi TRUE
##  $ : int [1:3] 1 2 3
```

```r
class(l)
```

```
## [1] "list"
```

```r
typeof(l)
```

```
## [1] "list"
```

</details>

<br>
<details><summary>**Example**: Investigating nested lists</summary>


```r
l <- list(list(TRUE, c(1, 2, 3), list(c("a", "b", "c"))), FALSE, 10L)
str(l)
```

```
## List of 3
##  $ :List of 3
##   ..$ : logi TRUE
##   ..$ : num [1:3] 1 2 3
##   ..$ :List of 1
##   .. ..$ : chr [1:3] "a" "b" "c"
##  $ : logi FALSE
##  $ : int 10
```

```r
class(l)
```

```
## [1] "list"
```

```r
typeof(l)
```

```
## [1] "list"
```

</details>

<br>
<details><summary>**Example**: Investigating named lists</summary>


```r
l <- list(l1 = 1, l2 = c("apple", "orange"), l3 = list(1, 2, 3))
str(l)
```

```
## List of 3
##  $ l1: num 1
##  $ l2: chr [1:2] "apple" "orange"
##  $ l3:List of 3
##   ..$ : num 1
##   ..$ : num 2
##   ..$ : num 3
```

```r
class(l)
```

```
## [1] "list"
```

```r
typeof(l)
```

```
## [1] "list"
```

</details>


#### Dataframes

What are **dataframes**?

- **Dataframes** are a special kind of **list** with the following characteristics:
  - Each element is a **vector** (i.e., _a column in the dataframe_)
  - The element should be named (i.e., _column name in the dataframe_)
  - Each of the vectors must be the same length (i.e., _same number of rows in the dataframe_)
  - The data type of each vector may be different
- Dataframes can be created using the function `data.frame()`
- The `class()` of  a dataframe is `data.frame`
- The `typeof()` a dataframe is `list`


<br>
<details><summary>**Example**: Investigating dataframe</summary>


```r
df <- data.frame(
  colA = c(1, 2, 3),
  colB = c("a", "b", "c"),
  colC = c(TRUE, FALSE, TRUE),
  stringsAsFactors = FALSE
)
df
```

```
## # A tibble: 3 x 3
##    colA colB  colC 
##   <dbl> <chr> <lgl>
## 1     1 a     TRUE 
## 2     2 b     FALSE
## 3     3 c     TRUE
```

```r
str(df)
```

```
## 'data.frame':	3 obs. of  3 variables:
##  $ colA: num  1 2 3
##  $ colB: chr  "a" "b" "c"
##  $ colC: logi  TRUE FALSE TRUE
```

```r
class(df)
```

```
## [1] "data.frame"
```

```r
typeof(df)
```

```
## [1] "list"
```

</details>

### Identifying object types

Functions for identifying object types (_returns `TRUE` or `FALSE`_):

- `is.logical()`: Is object of type `logical`?
- `is.integer()`: Is object of type `integer`?
- `is.double()`: Is object of type `double`?
- `is.numeric()`: Is object of type `numeric`?
- `is.character()`: Is object of type `character`?
- `is.atomic()`: Is object of type `atomic`?
- `is.list()`: Is object of type `list`?
- `is.vector()`: Is object of type `vector`?


Function | logical | int | dbl | chr | list
---------|---------|-----|-----|-----|-----
`is.logical()` | X | | | |
`is.integer()` |  |X | | |
`is.double()` |  | |X | |
`is.numeric()` |  |X |X | |
`is.character()` |  | | |X |
`is.atomic()` |X  |X |X |X |
`is.list()` |  | | | | X
`is.vector()` |X  |X |X |X |X

<br>
<details><summary>**Example**: Identifying object types</summary>


```r
v <- c(5, 6, 7)
is.logical(v)
```

```
## [1] FALSE
```

```r
is.integer(v)
```

```
## [1] FALSE
```

```r
is.double(v)
```

```
## [1] TRUE
```

```r
is.numeric(v)
```

```
## [1] TRUE
```

```r
is.character(v)
```

```
## [1] FALSE
```

```r
is.atomic(v)
```

```
## [1] TRUE
```

```r
is.list(v)
```

```
## [1] FALSE
```

```r
is.vector(v)
```

```
## [1] TRUE
```

</details>


### Converting between classes

Functions for converting between classes:

- `as.logical()`: Convert to `logical`
- `as.numeric()`: Convert to `numeric`
- `as.integer()`: Convert to `integer`
- `as.character()`: Convert to `character`
- `as.list()`: Convert to `list`
- `as.data.frame()`: Convert to `data.frame`


<br>
<details><summary>**Example**: Using `as.logical()` to convert to `logical`</summary>

Character vector coerced to logical vector:


```r
# Only "TRUE"/"FALSE", "True"/"False", "T"/"F", "true"/"false" are able to be coerced to logical type
as.logical(c("TRUE", "FALSE", "True", "False", "true", "false", "T", "F", "t", "f", ""))
```

```
##  [1]  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE    NA    NA    NA
```

Numeric vector coerced to logical vector:


```r
# 0 is treated as FALSE, while all other numeric values are treated as TRUE
as.logical(c(0, 0.0, 1, -1, 20, 5.5))
```

```
## [1] FALSE FALSE  TRUE  TRUE  TRUE  TRUE
```

</details>

<br>
<details><summary>**Example**: Using `as.numeric()` to convert to `numeric`</summary>

Logical vector coerced to numeric vector:


```r
# FALSE is mapped to 0 and TRUE is mapped to 1
as.numeric(c(FALSE, TRUE))
```

```
## [1] 0 1
```

Character vector coerced to numeric vector:


```r
# Strings containing numeric values can be coerced to numeric (leading 0's are dropped) 
# All other characters become NA
as.numeric(c("0", "007", "2.5", "abc", "."))
```

```
## [1] 0.0 7.0 2.5  NA  NA
```

</details>

<br>
<details><summary>**Example**: Using `as.integer()` to convert to `integer`</summary>

Logical vector coerced to integer vector:


```r
# FALSE is mapped to 0 and TRUE is mapped to 1
as.integer(c(FALSE, TRUE))
```

```
## [1] 0 1
```

Character vector coerced to integer vector:


```r
# Strings containing numeric values can be coerced to integer (leading 0's are dropped, decimals are truncated) 
# All other characters become NA
as.integer(c("0", "007", "2.5", "abc", "."))
```

```
## [1]  0  7  2 NA NA
```

Numeric vector coerced to integer vector:


```r
# All decimal places are truncated
as.integer(c(0, 2.1, 10.5, 8.8, -1.8))
```

```
## [1]  0  2 10  8 -1
```

</details>

<br>
<details><summary>**Example**: Using `as.character()` to convert to `character`</summary>

Logical vector coerced to character vector:


```r
as.character(c(FALSE, TRUE))
```

```
## [1] "FALSE" "TRUE"
```

Numeric vector coerced to character vector:


```r
as.character(c(-5, 0, 2.5))
```

```
## [1] "-5"  "0"   "2.5"
```

Integer vector coerced to character vector:


```r
as.character(c(-2L, 0L, 10L))
```

```
## [1] "-2" "0"  "10"
```

</details>

<br>
<details><summary>**Example**: Using `as.list()` to convert to `list`</summary>

Atomic vectors coerced to list:


```r
# Logical vector
as.list(c(TRUE, FALSE))
```

```
## [[1]]
## [1] TRUE
## 
## [[2]]
## [1] FALSE
```

```r
# Character vector
as.list(c("a", "b", "c"))
```

```
## [[1]]
## [1] "a"
## 
## [[2]]
## [1] "b"
## 
## [[3]]
## [1] "c"
```

```r
# Numeric vector
as.list(1:3)
```

```
## [[1]]
## [1] 1
## 
## [[2]]
## [1] 2
## 
## [[3]]
## [1] 3
```

</details>

<br>
<details><summary>**Example**: Using `as.data.frame()` to convert to `data.frame`</summary>

Lists coerced to dataframe:


```r
# Create a list
l <- list(A = c("x", "y", "z"), B = c(1, 2, 3))
str(l)
```

```
## List of 2
##  $ A: chr [1:3] "x" "y" "z"
##  $ B: num [1:3] 1 2 3
```

```r
# Convert to class `data.frame`
df <- as.data.frame(l, stringsAsFactors = F)
str(df)
```

```
## 'data.frame':	3 obs. of  2 variables:
##  $ A: chr  "x" "y" "z"
##  $ B: num  1 2 3
```

</details>


## Subsetting elements

What is **subsetting**?

- Subsetting refers to isolating particular elements of an object 
- Subsetting operators can be used to select/exclude elements (e.g., variables, observations)
- There are three subsetting operators: `[]`, `[[]]`, `$` 
- These operators function differently based on vector types (e.g., atomic vectors, lists, dataframes)

<br>
For the examples in the next few subsections, we will be working with the following named atomic vector, named list, and dataframe:

- Create named atomic vector called `v` with 4 elements

    
    ```r
    v <- c(a = 10, b = 20, c = 30, d = 40)
    v
    ```
    
    ```
    ##  a  b  c  d 
    ## 10 20 30 40
    ```

- Create named list called `l` with 4 elements

    
    ```r
    l <- list(a = TRUE, b = c("a", "b", "c"), c = list(1, 2), d = 10L)
    l
    ```
    
    ```
    ## $a
    ## [1] TRUE
    ## 
    ## $b
    ## [1] "a" "b" "c"
    ## 
    ## $c
    ## $c[[1]]
    ## [1] 1
    ## 
    ## $c[[2]]
    ## [1] 2
    ## 
    ## 
    ## $d
    ## [1] 10
    ```

- Create dataframe called `df` with 4 columns and 3 rows

    
    ```r
    df <- data.frame(
      a = c(11, 21, 31),
      b = c(12, 22, 32),
      c = c(13, 23, 33),
      d = c(14, 24, 34)
    )
    df
    ```
    
    ```
    ## # A tibble: 3 x 4
    ##       a     b     c     d
    ##   <dbl> <dbl> <dbl> <dbl>
    ## 1    11    12    13    14
    ## 2    21    22    23    24
    ## 3    31    32    33    34
    ```
    
### Subsetting using `[]`

The `[]` operator:

- Subsetting an object using `[]` returns an object of the same type
  - E.g., Using `[]` on an atomic vector returns an atomic vector, using `[]` on a list returns a list, etc.
- The returned object will contain the element(s) you selected
- Object attributes are retained when using `[]` (e.g., _name_)

Six ways to subset using `[]`:

1. Use positive integers to return elements at specified index positions
2. Use negative integers to exclude elements at specified index positions
3. Use logical vectors to return elements where corresponding logical is `TRUE`
4. Empty vector `[]` returns original object (useful for dataframes)
5. Zero vector `[0]` returns empty object (useful for testing data)
6. If object is named, use character vectors to return elements with matching names

<br>
<details><summary>**Example**: Using positive integers with `[]`</summary>

**Selecting a single element**: Specify the index of the element to subset


```r
# Select 1st element from numeric vector (note that names attribute is retained)
v[1]
```

```
##  a 
## 10
```

```r
# Subsetted object will be of type `numeric`
class(v[1])
```

```
## [1] "numeric"
```

```r
# Select 1st element from list (note that names attribute is retained)
l[1]
```

```
## $a
## [1] TRUE
```

```r
# Subsetted object will be a `list` containing the element
class(l[1])
```

```
## [1] "list"
```

<br>
**Selecting multiple elements**: Specify the indices of the elements to subset using `c()`


```r
# Select 3rd and 1st elements from numeric vector
v[c(3,1)]
```

```
##  c  a 
## 30 10
```

```r
# Subsetted object will be of type `numeric`
class(v[c(3,1)])
```

```
## [1] "numeric"
```

```r
# Select 1st element three times from list
l[c(1,1,1)]
```

```
## $a
## [1] TRUE
## 
## $a
## [1] TRUE
## 
## $a
## [1] TRUE
```

```r
# Subsetted object will be a `list` containing the elements
class(l[c(1,1,1)])
```

```
## [1] "list"
```

</details>

<br>
<details><summary>**Example**: Using negative integers with `[]`</summary>

**Excluding a single element**: Specify the index of the element to exclude


```r
# Exclude 1st element from numeric vector (note that names are retained)
v[-1]
```

```
##  b  c  d 
## 20 30 40
```

```r
# Subsetted object will be of type `numeric`
class(v[-1])
```

```
## [1] "numeric"
```

<br>
**Excluding multiple elements**: Specify the indices of the elements to exclude using `-c()`


```r
# Exclude 1st and 3rd elements from list
l[-c(1,3)]
```

```
## $b
## [1] "a" "b" "c"
## 
## $d
## [1] 10
```

```r
# Subsetted object will be a `list` containing the remaining elements
class(l[-c(1,3)])
```

```
## [1] "list"
```

</details>

<br>
<details><summary>**Example**: Using logical vectors with `[]`</summary>

If the logical vector is the same length as the object, then each element in the object whose corresponding position in the logical vector is `TRUE` will be selected:


```r
# Select 2nd and 3rd elements from numeric vector
v[c(FALSE, TRUE, TRUE, FALSE)]
```

```
##  b  c 
## 20 30
```

```r
# Subsetted object will be of type `numeric`
class(v[c(FALSE, TRUE, TRUE, FALSE)])
```

```
## [1] "numeric"
```

<br>
If the logical vector is shorter than the object, then the elements in the logical vector will be recycled:


```r
# This is equivalent to `l[c(FALSE, TRUE, FALSE, TRUE)]`, thus retaining 2nd and 4th elements
l[c(FALSE, TRUE)]
```

```
## $b
## [1] "a" "b" "c"
## 
## $d
## [1] 10
```

```r
# Subsetted object will be a `list` containing the elements
class(l[c(FALSE, TRUE)])
```

```
## [1] "list"
```

<br>
We can also write expressions that evaluates to either `TRUE` or `FALSE`:

```r
# This expression is recycled and evaluates to be equivalent to `l[c(FALSE, FALSE, TRUE, TRUE)]`
v[v > 20]
```

```
##  c  d 
## 30 40
```

</details>

<br>
<details><summary>**Example**: Using empty vector `[]`</summary>

An empty vector `[]` just returns the original object:


```r
# Original atomic vector
v[]
```

```
##  a  b  c  d 
## 10 20 30 40
```

```r
# Original list
l[]
```

```
## $a
## [1] TRUE
## 
## $b
## [1] "a" "b" "c"
## 
## $c
## $c[[1]]
## [1] 1
## 
## $c[[2]]
## [1] 2
## 
## 
## $d
## [1] 10
```

```r
# Original dataframe
df[]
```

```
## # A tibble: 3 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    11    12    13    14
## 2    21    22    23    24
## 3    31    32    33    34
```

</details>

<br>
<details><summary>**Example**: Using zero vector `[0]`</summary>

A zero vector `[0]` just returns an empty object of the same type as the original object:


```r
# Empty named atomic vector
v[0]
```

```
## named numeric(0)
```

```r
# Empty named list
l[0]
```

```
## named list()
```

```r
# Empty dataframe
df[0]
```

```
## # A tibble: 3 x 0
```

</details>

<br>
<details><summary>**Example**: Using element names with `[]`</summary>

We can select a single element or multiple elements by their name(s):


```r
# Equivalent to v[2]
v["b"]
```

```
##  b 
## 20
```

```r
# Equivalent to l[c(1, 3)]
l[c("a", "c")]
```

```
## $a
## [1] TRUE
## 
## $c
## $c[[1]]
## [1] 1
## 
## $c[[2]]
## [1] 2
```

</details>

### Subsetting using `[[]]`

The `[[]]` operator:

- We can only use `[[]]` to extract a single element rather than multiple elements
- Subsetting an object using `[[]]` returns the selected element itself, which might not be of the same type as the original object
  - E.g., Using `[[]]` to select an element from a list that is a numeric vector will return that numeric vector and not a list containing that numeric vector, like what `[]` would return
    - Let `x` be a list with 3 elements (_Think of it as a train with 3 cars_)
    [![](https://d33wubrfki0l68.cloudfront.net/1f648d451974f0ed313347b78ba653891cf59b21/8185b/diagrams/subsetting/train.png)](https://adv-r.hadley.nz/subsetting.html#subset-single)
    - `x[1]` will be a list containing the 1st element, which is a numeric vector (i.e., _train with the 1st car_)
    - `x[[1]]` will be the numeric vector itself (i.e., _the objects within the 1st car_)
    [![](https://d33wubrfki0l68.cloudfront.net/aea9600956ff6fbbc29d8bd49124cca46c5cb95c/28eaa/diagrams/subsetting/train-single.png)](https://adv-r.hadley.nz/subsetting.html#subset-single)
    - *Source: Subsetting from [R for Data Science](https://adv-r.hadley.nz/subsetting.html)*
- Object attributes are removed when using `[[]]`
  - E.g., Using `[[]]` on a named object returns just the selected element itself without the name attribute

<br>
Two ways to subset using `[[]]`:

1. Use a positive integer to return an element at the specified index position
2. If object is named, using a character to return an element with the specified name

<br>
<details><summary>**Example**: Using positive integer with `[[]]`</summary>


```r
# Select 1st element from numeric vector (note that names attribute is gone)
v[[1]]
```

```
## [1] 10
```

```r
# Subsetted element is `numeric`
class(v[[1]])
```

```
## [1] "numeric"
```

```r
# Select 1st element from list (note that names attribute is gone)
l[[1]]
```

```
## [1] TRUE
```

```r
# Subsetted element is `logical`
class(l[[1]])
```

```
## [1] "logical"
```

</details>

<br>
<details><summary>**Example**: Using element name with `[[]]`</summary>


```r
# Equivalent to v[[2]]
v[["b"]]
```

```
## [1] 20
```

```r
# Subsetted element is `numeric`
class(v[["b"]])
```

```
## [1] "numeric"
```

```r
# Equivalent to l[[2]]
l[["b"]]
```

```
## [1] "a" "b" "c"
```

```r
# Subsetted element is `character` vector
class(l[["b"]])
```

```
## [1] "character"
```

</details>


### Subsetting using `$`

The `$` operator:

- `obj_name$element_name` is shorthand for `obj_name[["element_name"]]`
- This operator only works on lists (including dataframes) and not on atomic vectors

<br>
<details><summary>**Example**: Subsetting with `$`</summary>

Subsetting a list with `$`:


```r
# Equivalent to l[["b"]]
l$b
```

```
## [1] "a" "b" "c"
```

```r
# Subsetted element is `character` vector
class(l$b)
```

```
## [1] "character"
```

<br>
Since dataframes is just a special kind of named list, it would work the same way:


```r
# Equivalent to df[["d"]]
df$d
```

```
## [1] 14 24 34
```

</details>

### Subsetting dataframes

Subsetting dataframes with `[]`, `[[]]`, and `$`:

- Subsetting dataframes works the same way as lists because dataframes are just a special kind of named list, where we can think of each element as a column
  - `df_name[<column(s)>]` returns a dataframe containing the selected column(s), with its attributes retained
  - `df_name[[<column>]]` or `df_name$<column>` returns the column itself, without any attributes
- In addition to the normal way of subsetting, we are also allowed to subset dataframes by cell(s)
  - `df_name[<row(s)>, <column(s)>]` returns the selected cell(s)
    - If a single cell is selected, or cells from the same column, then these would be returned as an object of the same type as that column (similar to how `[[]]` normally works)
    - Otherwise, the subsetted object would be a dataframe, as we'd normally expect when using `[]`
  - `df_name[[<row>, <column>]]` returns the selected cell

<br>
<details><summary>**Example**: Subsetting dataframe column(s) with `[]`</summary>

We can subset dataframe column(s) the same way we have subsetted atomic vector or list element(s):


```r
# Select 1st column from dataframe (note that names attribute is retained)
df[1]
```

```
## # A tibble: 3 x 1
##       a
##   <dbl>
## 1    11
## 2    21
## 3    31
```

```r
# Subsetted object will be a `data.frame` containing the column
class(df[1])
```

```
## [1] "data.frame"
```

```r
# Exclude 1st and 3rd columns from dataframe (note that names attribute is retained)
df[-c(1,3)]
```

```
## # A tibble: 3 x 2
##       b     d
##   <dbl> <dbl>
## 1    12    14
## 2    22    24
## 3    32    34
```

```r
# Subsetted object will be a `data.frame` containing the remaining columns
class(df[-c(1,3)])
```

```
## [1] "data.frame"
```

</details>

<br>
<details><summary>**Example**: Subsetting dataframe column with `[[]]` and `$`</summary>

We can select a single dataframe column the same way we have subsetted a single atomic vector or list element:


```r
# Select 1st column from dataframe by its index (note that names attribute is gone)
df[[1]]
```

```
## [1] 11 21 31
```

```r
# Subsetted column is `numeric` vector
class(df[[1]])
```

```
## [1] "numeric"
```

```r
# Equivalently, we could've selected 1st column by its name
df[["a"]]
```

```
## [1] 11 21 31
```

```r
# Equivalently, we could've selected 1st column using `$`
df$a
```

```
## [1] 11 21 31
```

</details>

<br>
<details><summary>**Example**: Subsetting dataframe cell(s) with `[]`</summary>

If we select a single cell by specifying its row and column, we will get back the element itself, not in a dataframe:


```r
# Selects cell in 1st row and 2nd col
df[1, 2]
```

```
## [1] 12
```

```r
# Subsetted cell is of type `numeric`
class(df[1, 2])
```

```
## [1] "numeric"
```

```r
# Equivalently, we could select using column name instead of index
df[1, "b"]
```

```
## [1] 12
```

<br>
Similarly, if we select cells from the same column, we will get back the elements themselves, not in a dataframe:


```r
# Selects cells from the 2nd col
df[c(1,3), 2]
```

```
## [1] 12 32
```

```r
# Subsetted cells is of type `numeric`
class(df[c(1,3), 2])
```

```
## [1] "numeric"
```

```r
# Selects all cells from the 2nd col
df[, 2]
```

```
## [1] 12 22 32
```

```r
# Subsetted column is of type `numeric`
class(df[, 2])
```

```
## [1] "numeric"
```

<br>
However, if we select cells from the same row, or cells across multiple rows and columns, we will get back a dataframe that contains the selected cells:


```r
# Selects cells from the 2nd row
df[2, c("a", "c")]
```

```
## # A tibble: 1 x 2
##       a     c
##   <dbl> <dbl>
## 1    21    23
```

```r
# Subsetted cells are returned as a dataframe
class(df[2, c("a", "c")])
```

```
## [1] "data.frame"
```

```r
# Selects all cells from the 2nd row
df[2, ]
```

```
## # A tibble: 1 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    21    22    23    24
```

```r
# Subsetted row is returned as a dataframe
class(df[2, ])
```

```
## [1] "data.frame"
```

```r
# Selects cells from multiple rows and columns
df[1:2, c("a", "c")]
```

```
## # A tibble: 2 x 2
##       a     c
##   <dbl> <dbl>
## 1    11    13
## 2    21    23
```

```r
# Subsetted cells are returned as a dataframe
class(df[1:2, c("a", "c")])
```

```
## [1] "data.frame"
```

</details>

<br>
<details><summary>**Example**: Subsetting dataframe cell with `[[]]`</summary>

With `[[]]`, we are only allowed to select a single cell:


```r
# Selects cell in 1st row and 2nd col
df[[1, 2]]
```

```
## [1] 12
```

```r
# Subsetted cell is of type `numeric`
class(df[[1, 2]])
```

```
## [1] "numeric"
```

```r
# This is equivalent to using `[]`
df[1, 2]
```

```
## [1] 12
```

</details>

## Attributes [SKIP]

### Augmented vectors

What are **augmented vectors** and **attributes**?

- Atomic vectors can be thought of as "just the data", while **augmented vectors** are atomic vectors with additional attributes attached
- **Attributes** are additional "metadata" that can be attached to any object (e.g., vector or list)
  - E.g., __Value labels__: Character labels (e.g., "Charter School") attached to numeric values
  - E.g., __Object class__: Specifies how object is treated by object oriented programming language
- Recall that when we subset by `[]`, all the attributes are retained. When we subset by `[[]]`, we get back "just the data" without any of the attributes.

**Example**: Variables of a dataset

- A data frame is a list
- Each element in the list is a variable (i.e., column), which consists of:
    - Atomic vector ("just the data")
    - Variable _name_, which is an attribute we attach to the element/variable
    - Any other attributes we want to attach to element/variable

__Main takaway__:

- Augmented vectors are atomic vectors (just the data) with additional attributes attached
- Description of attributes from [Wickham and Grolemund](https://r4ds.had.co.nz/vectors.html#attributes):
  - "Any vector can contain arbitrary additional __metadata__ through its __attributes__"
  - "You can think of __attributes__ as named list of vectors that can be attached to any object"
- Functions to identify and modify attributes
  - `attributes()`: View all attributes of an object or set/change all attributes of an object
  - `attr()`: View individual attribute of an object or set/change an individual attribute of an object

### `attributes()` function

__The `attributes()` function__:


```r
?attributes

# SYNTAX
attributes(x)  # Get attributes
attributes(x) <- value  # Set attributes
```

- Function: Get or set all attributes of an object
- Arguments
  - `x`: The object whose attributes we want to view or modify
  - `value`: In the assignment form, the value we want to set all attributes to be

<br>
<details><summary>**Example**: Using `attributes()` to get attributes of object</summary>

Recall our dataframe `df` from the previous examples, which has multiple attributes:


```r
df
```

```
## # A tibble: 3 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    11    12    13    14
## 2    21    22    23    24
## 3    31    32    33    34
```

```r
# View attributes of dataframe
attributes(df)
```

```
## $names
## [1] "a" "b" "c" "d"
## 
## $class
## [1] "data.frame"
## 
## $row.names
## [1] 1 2 3
```

<br>
When we subset by `[]`, attributes are retained:


```r
# Subset 1st column using `[]`
df[1]
```

```
## # A tibble: 3 x 1
##       a
##   <dbl>
## 1    11
## 2    21
## 3    31
```

```r
# Attributes are retained when we subset by `[]`
attributes(df[1])
```

```
## $names
## [1] "a"
## 
## $row.names
## [1] 1 2 3
## 
## $class
## [1] "data.frame"
```

<br>
When we subset by `[[]]`, attributes are removed and we are left with "just the data":


```r
# Subset 1st column using `[[]]`
df[[1]]
```

```
## [1] 11 21 31
```

```r
# Attributes are gone when we subset by `[[]]`
attributes(df[[1]])
```

```
## NULL
```

</details>

<br>
<details><summary>**Example**: Using `attributes()` to set attributes of object</summary>

Recall our named atomic vector `v` from the previous examples, which has the _name_ attribute:


```r
v
```

```
##  a  b  c  d 
## 10 20 30 40
```

```r
# View attributes of atomic vector
attributes(v)
```

```
## $names
## [1] "a" "b" "c" "d"
```

<br>
Remove all attributes from the vector:


```r
# Set all attributes to NULL
attributes(v) <- NULL

# The atomic vector is no longer named
v
```

```
## [1] 10 20 30 40
```

```r
# Confirm that the names attribute is no longer there
attributes(v)
```

```
## NULL
```

</details>

### `attr()` function

__The `attr()` function__:


```r
?attr

# SYNTAX AND DEFAULT VALUES
attr(x, which, exact = FALSE)  # Get attribute
attr(x, which) <- value  # Set attribute
```

- Function: Get or set a specific attribute of an object
- Arguments
  - `x`: The object whose attribute we want to view or modify
  - `which`: A non-empty string specifying which attribute is to be accessed
  - `exact`: If set to `TRUE`, the attribute specified by `which` needs to be matched exactly
  - `value`: In the assignment form, the value we want to set the attribute to be

<br>
<details><summary>**Example**: Using `attr()` to get attribute of object</summary>

Recall our dataframe `df` from the previous examples, which has multiple attributes:


```r
df
```

```
## # A tibble: 3 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    11    12    13    14
## 2    21    22    23    24
## 3    31    32    33    34
```

```r
# View attributes of dataframe
attributes(df)
```

```
## $names
## [1] "a" "b" "c" "d"
## 
## $class
## [1] "data.frame"
## 
## $row.names
## [1] 1 2 3
```

<br>
We can use `attr()` to fetch individual attributes:


```r
# Get the names attribute
attr(df, "names")
```

```
## [1] "a" "b" "c" "d"
```

```r
# Note that we don't have to provide the full name of attribute for it to be recognized
attr(df, "nam")
```

```
## [1] "a" "b" "c" "d"
```

```r
# If we specify `exact = TRUE`, then we do have to provide exact attribute name
attr(df, "names", exact = TRUE)
```

```
## [1] "a" "b" "c" "d"
```

```r
# This no longer works
attr(df, "nam", exact = TRUE)
```

```
## NULL
```

</details>

<br>
<details><summary>**Example**: Using `attr()` to set attribute of object</summary>

Recall the atomic vector `v` that we've removed all attributes from in the previous example:


```r
v
```

```
## [1] 10 20 30 40
```

```r
# View attributes of atomic vector
attributes(v)
```

```
## NULL
```

<br>
We can add back the `names` attributes using `attr()`:


```r
# Add back names attribute
attr(v, "names") <- c("a", "b", "c", "d")

# View attributes
attributes(v)
```

```
## $names
## [1] "a" "b" "c" "d"
```

<br>
We can also create any other attributes we want:


```r
# Create new attribute called `greeting`
attr(x = v, which = "greeting") <- "Hi!"

# View `greeting` attribute
attr(x = v, which = "greeting")
```

```
## [1] "Hi!"
```

```r
# View all attributes
attributes(v)
```

```
## $names
## [1] "a" "b" "c" "d"
## 
## $greeting
## [1] "Hi!"
```

<br>
We can use `NULL` to remove attributes:


```r
# Remove `greeting` attribute
attr(x = v, which = "greeting") <- NULL

# Try viewing `greeting` attribute
attr(x = v, which = "greeting")
```

```
## NULL
```

```r
# View all attributes
attributes(v)
```

```
## $names
## [1] "a" "b" "c" "d"
```

</details>

<br>
<details><summary>**Example**: Using `attr()` to set attribute of dataframe variable</summary>

Unlike atomic vectors, we can also set attributes of individual elements of lists (which include dataframes). Recall our dataframe `df`:


```r
df
```

```
## # A tibble: 3 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    11    12    13    14
## 2    21    22    23    24
## 3    31    32    33    34
```

```r
# View attributes of dataframe
attributes(df)
```

```
## $names
## [1] "a" "b" "c" "d"
## 
## $class
## [1] "data.frame"
## 
## $row.names
## [1] 1 2 3
```

<br>
We can also add attributes to an individual column (i.e., variable) of the dataframe using `[[]]` or `$`:


```r
# Equivalent to df[["a"]] - Remember this usually starts off as "just the data" with no attributes
attributes(df$a)
```

```
## NULL
```

```r
# Add an attribute
attr(df$a, "description") <- "A is for Apple"

# View attributes
attributes(df$a)
```

```
## $description
## [1] "A is for Apple"
```

<br>
We can use `NULL` to remove attribute:


```r
# Remove `description` attribute
attr(df$a, "description") <- NULL

# Try viewing `description` attribute
attr(df$a, "description")
```

```
## NULL
```

```r
# View attributes
attributes(df$a)
```

```
## NULL
```

</details>

## Names and values [EMPTY]

## Prerequisite concepts

Several functions and concepts are used frequently when creating loops and/or functions.

### Sequences

What are **sequences**?

- (Loose) definition: A **sequence** is a list of numbers in ascending or descending order
- Sequences can be created using the `:` operator or `seq()` function

**Example**: Creating sequences using `:`


```r
# Sequence from -5 to 5
-5:5
```

```
##  [1] -5 -4 -3 -2 -1  0  1  2  3  4  5
```

```r
# Sequence from 5 to -5
5:-5
```

```
##  [1]  5  4  3  2  1  0 -1 -2 -3 -4 -5
```

<br>
__The `seq()` function__:


```r
?seq

# SYNTAX AND DEFAULT VALUES
seq(from = 1, to = 1, by = ((to - from)/(length.out - 1)),
    length.out = NULL, along.with = NULL, ...)
```

- Function: Generate a sequence
- Arguments
  - `from`: The starting value of sequence
  - `to`: The end (or maximal) value of sequence
  - `by`: Increment of the sequence

**Example**: Creating sequences using `seq()`


```r
# Sequence from 10 to 15, by increment of 1 (default)
seq(10,15)
```

```
## [1] 10 11 12 13 14 15
```

```r
# Explicitly specify increment of 1 (equivalent to above)
seq(from=10, to=15, by=1)
```

```
## [1] 10 11 12 13 14 15
```

```r
# Sequence from 100 to 150, by increment of 10
seq(from=100, to=150, by=10)
```

```
## [1] 100 110 120 130 140 150
```

### Length

__The `length()` function__:


```r
?length

# SYNTAX
length(x)
```

- Function: Returns the number of elements in the object
- Arguments:
  - `x`: The object to find the length of

<br>
**Example**: Using `length()` to find number of elements in `v`


```r
# View the atomic vector
v
```

```
##  a  b  c  d 
## 10 20 30 40
```

```r
# Use `length()` to find number of elements
length(v)
```

```
## [1] 4
```

<br>
**Example**: Using `length()` to find number of elements in `df`

Remember that dataframes are just lists where each element is a column, so the number of elements in a dataframe is just the number of columns it has:


```r
# View the dataframe
df
```

```
## # A tibble: 3 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    11    12    13    14
## 2    21    22    23    24
## 3    31    32    33    34
```

```r
# Use `length()` to find number of elements (i.e., columns)
length(df)
```

```
## [1] 4
```

<br>
When we subset a dataframe using `[]` (i.e., _select column(s) from the dataframe_), the length of the subsetted object is the number of columns we selected:


```r
# Subset one column
df[1]
```

```
## # A tibble: 3 x 1
##       a
##   <dbl>
## 1    11
## 2    21
## 3    31
```

```r
# Length is one
length(df[1])
```

```
## [1] 1
```

```r
# Subset three columns
df[1:3]
```

```
## # A tibble: 3 x 3
##       a     b     c
##   <dbl> <dbl> <dbl>
## 1    11    12    13
## 2    21    22    23
## 3    31    32    33
```

```r
# Length is three
length(df[1:3])
```

```
## [1] 3
```

<br>
When we subset a dataframe using `[[]]` (i.e., _isolate a specific column in the dataframe_), the length of the subsetted object is the number of rows in the dataframe:


```r
# Isolate a specific column
df[[2]]
```

```
## [1] 12 22 32
```

```r
# Length is number of elements in that column (i.e., number of rows in dataframe)
length(df[[2]])
```

```
## [1] 3
```


### Sequences and length

When writing loops, it is very common to create a sequence from 1 to the length (i.e., number of elements) of an object.

<br>
**Example**: Generating a sequence from 1 to length of `v`


```r
# There are 4 elements in the atomic vector
v
```

```
##  a  b  c  d 
## 10 20 30 40
```

```r
# Use `:` to generate a sequence from 1 to 4
1:length(v)
```

```
## [1] 1 2 3 4
```

```r
# Use `seq()` to generate a sequence from 1 to 4
seq(1, length(v))
```

```
## [1] 1 2 3 4
```

<br>
There is also a function `seq_along()` that makes it easier to generate a sequence from 1 to the length of an object.

<br>
__The `seq_along()` function__:


```r
?seq_along

# SYNTAX
seq_along(x)
```

- Function: Generates a sequence from 1 to the length of the input object
- Arguments
  - `x`: The object to generate the sequence for

<br>
**Example**: Generating a sequence from 1 to length of `df`


```r
# There are 4 elements (i.e., columns) in the dataframe
df
```

```
## # A tibble: 3 x 4
##       a     b     c     d
##   <dbl> <dbl> <dbl> <dbl>
## 1    11    12    13    14
## 2    21    22    23    24
## 3    31    32    33    34
```

```r
# Use `seq_along()` to generate a sequence from 1 to 4
seq_along(df)
```

```
## [1] 1 2 3 4
```

### Directories and paths [SKIP]

<br>

#### Current working directory

When you run R code in an `.Rmd` file, the working directory is the directory that your `.Rmd` file is in:


```r
getwd()
```

```
## [1] "/Users/cyouh95/Projects/RStudio/rclass2/lectures/programming"
```

<br>
When you run an `.R` script, the working directory is the directory indicated at the top of your console in RStudio:

![](../../assets/images/r_console.png)

- This is typically your home directory if you are not working from an RStudio project
- If you are working from an RStudio project, your working directory would be the project directory

<br>

#### Creating and deleting directories

<br>
__The `dir.create()` function__:


```r
?dir.create

# SYNTAX AND DEFAULT VALUES
dir.create(path, showWarnings = TRUE, recursive = FALSE, mode = "0777")
```

- Function: Creates new directories
- Arguments  
  - `path`: A character vector containing a single path name
  - `showWarnings`: Should the warnings on failure be shown?
    - If directory you want to create already exists, you will get a warning, but this won't cause the code to stop running
  - `recursive`: Should elements of the path other than the last be created?
    - That is, will `dir.create()` create the file path `new_directory/new_sub_directory` if neither `new_directory` nor `new_sub_directory` exist?

<br>
**Example**: Creating a new directory within current working directory


```r
# Check current working directory
getwd()
```

```
## [1] "/Users/cyouh95/Projects/RStudio/rclass2/lectures/programming"
```

```r
# Create new directory called `my_folder`
dir.create(path = "my_folder")

# Check that `my_folder` has been created
list.files()
```

```
## [1] "data"                     "ipeds_file_list.txt"     
## [3] "loop_example_ipeds.R"     "my_folder"               
## [5] "programming_lecture.html" "programming_lecture.md"  
## [7] "programming_lecture.Rmd"  "programming.Rproj"
```

<br>
__The `unlink()` function__:


```r
?unlink

# SYNTAX AND DEFAULT VALUES
unlink(x, recursive = FALSE, force = FALSE)
```

- Function: Deletes files or directories
- Arguments  
  - `x`: A character vector with the names of the files or directories to be deleted
  - `recursive`: Should directories be deleted recursively?
    - If recursive = `FALSE`, directories are not deleted, not even empty ones.
  - `force`: Should permissions be changed (if possible) to allow the file or directory to be removed?

<br>
**Example**: Deleting a directory within current working directory


```r
# Delete `my_folder` we just created
unlink(x = "my_folder", recursive = TRUE) 

# Check that `my_folder` has been deleted
list.files()
```

```
## [1] "data"                     "ipeds_file_list.txt"     
## [3] "loop_example_ipeds.R"     "programming_lecture.html"
## [5] "programming_lecture.md"   "programming_lecture.Rmd" 
## [7] "programming.Rproj"
```

<br>

#### File paths

> We use the `file.path()` command because it is smart. Some computer operating systems use forward slashes, `/`, for their file paths; others use backslashes, `\`. Rather than try to guess or assume what operating system future users will use, we can use R's function, `file.path()`, to check the current operating system and build the paths correctly for us.

*Credit: [Organizing Lecture](https://edquant.github.io/edh7916/lessons/organizing.html) by Ben Skinner*

<br>
__The `file.path()` function__:


```r
?file.path

# SYNTAX AND DEFAULT VALUES
file.path(..., fsep = .Platform$file.sep)
```

- Pass in each section of the file path as a separate argument
  - Example: `file.path('.', 'lectures', 'week_1')` returns `'./lectures/week_1'`
- You can also save this file path object in a variable
  - Example: `lec_dir <- file.path('.', 'lectures', 'week_1')`


# Iteration

What is **iteration**?

- Iteration is the repetition of some process or operation
  - Example: Iteration can help with "repeating the same operation on different columns, or on different datasets" (From [R for Data Science](https://r4ds.had.co.nz/iteration.html))
- Looping is the most common way to iterate

## Loop basics

What are **loops**?

- __Loops__ execute some set of commands multiple times
- Each time the loop executes the set of commands is an __iteration__
- The below loop iterates 4 times

<br>
__Example__: Printing each element of the vector `c(1,2,3,4)` using a loop


```r
c(1,2,3,4)  # There are 4 elements in the vector
```

```
## [1] 1 2 3 4
```

```r
for(i in c(1,2,3,4)) {  # Iterate over each element of the vector
  print(i)  # Print out each element
}
```

```
## [1] 1
## [1] 2
## [1] 3
## [1] 4
```

<br>
When to write **loops**?

- Broadly, rationale for writing loop:
  - Do not duplicate code
  - Can make changes to code in one place rather than many
- When to write a loop:
  - Grolemund and Wickham say __don't copy and paste more than twice__
  - If you find yourself doing this, consider writing a loop or function
- Don't worry about knowing all the situations you should write a loop
  - Rather, you'll be creating analysis dataset or analyzing data and you will notice there is some task that you are repeating over and over
  - Then you'll think, "Oh, I should write a loop or function for this"


## Components of a loop

How to write a **loop**?

- We can build loops using the `for()` function
- The **loop sequence** goes inside the parentheses of `for()`
- The **loop body** goes inside the pair of curly brackets (`{}`) that follows `for()`


```r
for(i in c(1,2,3,4)) {  # Loop sequence
  print(i)  # Loop body
}
```

<br>
Components of a **loop**:

1. __Sequence__: Determines what to "loop over"
    - In the above example, the sequence is `i in c(1,2,3,4)`
    - This creates a temporary/local object named `i` (could name it anything)
    - Each iteration of the loop will assign a different value to `i`
    - `c(1,2,3,4)` is the set of values that will be assigned to `i` 
        - In the first iteration, the value of `i` is `1`
        - In the second iteration, the value of `i` is `2`, etc.
2. __Body__: What commands to execute for each iteration of the loop
    - In the above example, the body is `print(i)`
    - Each time through the loop (i.e., iteration), body prints the value of object `i`
    

### Ways to write loop sequence

You may see the loop sequence being written in slightly different ways. For example, these three loops all do the same thing:

- Looping over the vector `c(1,2,3)`

    
    ```r
    for(z in c(1,2,3)) {  # Loop sequence
      print(z)  # Loop body
    }
    ```
    
    ```
    ## [1] 1
    ## [1] 2
    ## [1] 3
    ```

- Looping over the sequence `1:3` 

    
    ```r
    for(z in 1:3) {  # Loop sequence
      print(z)  # Loop body
    }
    ```
    
    ```
    ## [1] 1
    ## [1] 2
    ## [1] 3
    ```

- Looping over the object `num_sequence`
    
    
    ```r
    num_sequence <- 1:3
    for(z in num_sequence) {  # Loop sequence
      print(z)  # Loop body
    }
    ```
    
    ```
    ## [1] 1
    ## [1] 2
    ## [1] 3
    ```

### Printing values in loop body

When building a loop, it is useful to print out information to understand what the loop is doing. The `cat()` function allows us to concatenate and print multiple objects.

__The `cat()` function__:


```r
?cat

# SYNTAX AND DEFAULT VALUES
cat(... , file = "", sep = " ", fill = FALSE, labels = NULL, append = FALSE)
```

- Function: Concatenate and print multiple objects
- Arguments:
  - The input is all the objects you want to print, separated by commas
  - `sep`: By default, the objects are separated by a space when they are printed out
  - `fill`: If set to `TRUE`, a newline will be added after the printed output

<br>
For example, the two loops below are essentially the same, but the second approach is preferable because it more clearly prints out what object we are working with inside the loop:

- Using `print()` to print a single object `z`:

    
    ```r
    for(z in c(1,2,3)) {
      print(z)
    }
    ```
    
    ```
    ## [1] 1
    ## [1] 2
    ## [1] 3
    ```

- Using `cat()` to concatenate and print multiple items:

    
    ```r
    for(z in c(1,2,3)) {
      cat("object z =", z, fill=TRUE)  # `fill=TRUE` forces line break after each iteration
    }
    ```
    
    ```
    ## object z = 1
    ## object z = 2
    ## object z = 3
    ```

### Student exercise


1. Create a numeric vector that contains the year of birth of your family members
    - Example: `birth_years <- c(1944,1950,1981,2016)`
2. Write a loop that calculates the current year minus birth year and prints this number for each member of your family
    - Within this loop, you will create a new variable that calculates current year minus birth year

<br>
<details><summary>**Solution**</summary>


```r
birth_years <- c(1944,1950,1981,2016)
birth_years
```

```
## [1] 1944 1950 1981 2016
```

```r
for(y in birth_years) {  # Loop sequence
  cat("object y =", y, fill=TRUE)  # Loop body
  z <- 2020 - y
  cat("value of", y, "minus", 2018, "is", z, fill=TRUE)
}
```

```
## object y = 1944
## value of 1944 minus 2018 is 76
## object y = 1950
## value of 1950 minus 2018 is 70
## object y = 1981
## value of 1981 minus 2018 is 39
## object y = 2016
## value of 2016 minus 2018 is 4
```
</details>


## Ways to loop over a vector

There are 3 ways to loop over elements of an object:

1. [Looping over the elements](#looping-over-elements) (approach we have used so far)
2. [Looping over names of the elements](#looping-over-names)
3. [Looping over numeric indices associated with element position](#looping-over-indices) (approach recommended by Grolemnund and Wickham)

<br>
For the examples in the next few subsections, we will be working with the following named atomic vector and dataframe:

- Create named atomic vector called `vec`

    
    ```r
    vec <- c(a = 5, b = -10, c = 30)
    vec
    ```
    
    ```
    ##   a   b   c 
    ##   5 -10  30
    ```

- Create dataframe called `df` with randomly generated data, 3 columns (vars) and 4 rows (obs)

    
    ```r
    set.seed(12345) # so we all get the same variable values
    df <- tibble(a = rnorm(4), b = rnorm(4), c = rnorm(4))
    str(df)
    ```
    
    ```
    ## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  3 variables:
    ##  $ a: num  0.586 0.709 -0.109 -0.453
    ##  $ b: num  0.606 -1.818 0.63 -0.276
    ##  $ c: num  -0.284 -0.919 -0.116 1.817
    ```

### Looping over elements

**Syntax**: `for (i in object_name)`

- This approach iterates over each element in the object
- The value of `i` is equal to the element's _content_ (rather than its _name_ or _index position_)

<br>
**Example**: Looping over elements in `vec`
    

```r
vec  # View named atomic vector object
```

```
##   a   b   c 
##   5 -10  30
```

```r
for (i in vec) {
  cat("value of object i =",i, fill=TRUE)
  cat("object i has: type =", typeof(i), "; length =", length(i), "; class =", class(i),
      "\n", fill=TRUE)  # "\n" adds line break
}
```

```
## value of object i = 5
## object i has: type = double ; length = 1 ; class = numeric 
## 
## value of object i = -10
## object i has: type = double ; length = 1 ; class = numeric 
## 
## value of object i = 30
## object i has: type = double ; length = 1 ; class = numeric
```

<br>
**Example**: Looping over elements in `df`


```r
df  # View dataframe object
```

```
## # A tibble: 4 x 3
##        a      b      c
##    <dbl>  <dbl>  <dbl>
## 1  0.586  0.606 -0.284
## 2  0.709 -1.82  -0.919
## 3 -0.109  0.630 -0.116
## 4 -0.453 -0.276  1.82
```

```r
for (i in df) {
  cat("value of object i =",i, fill=TRUE)
  cat("object i has: type =", typeof(i), "; length =", length(i), "; class =", class(i),
      "\n", fill=TRUE)  # "\n" adds line break
}
```

```
## value of object i = 0.5855288 0.709466 -0.1093033 -0.4534972
## object i has: type = double ; length = 4 ; class = numeric 
## 
## value of object i = 0.6058875 -1.817956 0.6300986 -0.2761841
## object i has: type = double ; length = 4 ; class = numeric 
## 
## value of object i = -0.2841597 -0.919322 -0.1162478 1.817312
## object i has: type = double ; length = 4 ; class = numeric
```

<br>
<details><summary>**Example**: Calculating column averages for `df` by looping over columns</summary>

The dataframe `df` is a list object, where each element is a vector (i.e., column):


```r
df  # View dataframe object
```

```
## # A tibble: 4 x 3
##        a      b      c
##    <dbl>  <dbl>  <dbl>
## 1  0.586  0.606 -0.284
## 2  0.709 -1.82  -0.919
## 3 -0.109  0.630 -0.116
## 4 -0.453 -0.276  1.82
```

```r
for (i in df) {
  cat("value of object i =", i, fill=TRUE)
  cat("mean value of object i =", mean(i, na.rm = TRUE), "\n", fill=TRUE)
}
```

```
## value of object i = 0.5855288 0.709466 -0.1093033 -0.4534972
## mean value of object i = 0.1830486 
## 
## value of object i = 0.6058875 -1.817956 0.6300986 -0.2761841
## mean value of object i = -0.2145385 
## 
## value of object i = -0.2841597 -0.919322 -0.1162478 1.817312
## mean value of object i = 0.1243956
```
</details>

### Looping over names

**Syntax**: `for (i in names(object_name))`

- To use this approach, elements in the object must have name attributes
- This approach iterates over the names of each element in the object
- `names()` returns a vector of the object's element names
- The value of `i` is equal to the element's _name_ (rather than its _content_ or _index position_)
- But note that it is still possible to access the element's content inside the loop:
    - Access element contents using `object_name[i]`
        - Same object type as `object_name`; retains attributes (e.g., _name_)
    - Access element contents using `object_name[[i]]`
        - Removes level of hierarchy, thereby removing attributes
        - Approach recommended by Wickham because it isolates value of element

<br>
**Example**: Looping over elements in `vec`


```r
vec  # View named atomic vector object
```

```
##   a   b   c 
##   5 -10  30
```

```r
names(vec)  # View names of atomic vector object
```

```
## [1] "a" "b" "c"
```

```r
for (i in names(vec)) {
  cat("\nvalue of object i =", i, "; type =", typeof(i), fill=TRUE)
  str(vec[i])  # Access element contents using []
  str(vec[[i]])  # Access element contents using [[]]
}
```

```
## 
## value of object i = a ; type = character
##  Named num 5
##  - attr(*, "names")= chr "a"
##  num 5
## 
## value of object i = b ; type = character
##  Named num -10
##  - attr(*, "names")= chr "b"
##  num -10
## 
## value of object i = c ; type = character
##  Named num 30
##  - attr(*, "names")= chr "c"
##  num 30
```

<br>
**Example**: Looping over elements in `df`


```r
df  # View dataframe object
```

```
## # A tibble: 4 x 3
##        a      b      c
##    <dbl>  <dbl>  <dbl>
## 1  0.586  0.606 -0.284
## 2  0.709 -1.82  -0.919
## 3 -0.109  0.630 -0.116
## 4 -0.453 -0.276  1.82
```

```r
names(df)  # View names of dataframe object (i.e., column names)
```

```
## [1] "a" "b" "c"
```

```r
for (i in names(df)) {
  cat("\nvalue of object i =", i, "; type =", typeof(i), fill=TRUE)
  str(df[i])  # Access element contents using []
  str(df[[i]])  # Access element contents using [[]]
}
```

```
## 
## value of object i = a ; type = character
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  1 variable:
##  $ a: num  0.586 0.709 -0.109 -0.453
##  num [1:4] 0.586 0.709 -0.109 -0.453
## 
## value of object i = b ; type = character
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  1 variable:
##  $ b: num  0.606 -1.818 0.63 -0.276
##  num [1:4] 0.606 -1.818 0.63 -0.276
## 
## value of object i = c ; type = character
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  1 variable:
##  $ c: num  -0.284 -0.919 -0.116 1.817
##  num [1:4] -0.284 -0.919 -0.116 1.817
```


<br>
<details><summary>**Example**: Calculating column averages for `df` by looping over column names</summary>


```r
str(df)  # View structure of dataframe object
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  3 variables:
##  $ a: num  0.586 0.709 -0.109 -0.453
##  $ b: num  0.606 -1.818 0.63 -0.276
##  $ c: num  -0.284 -0.919 -0.116 1.817
```

<br>
Remember that we can use `[[]]` to access element contents by their name:


```r
for (i in names(df)) {
  cat("mean of element named", i, "=", mean(df[[i]], na.rm = TRUE), fill=TRUE)
}
```

```
## mean of element named a = 0.1830486
## mean of element named b = -0.2145385
## mean of element named c = 0.1243956
```

<br>
If we tried completing the task using `[]` to access the element contents, we would get an error because `mean()` only takes numeric or logical vectors as input, and `df[i]` returns a dataframe object:


```r
for (i in names(df)) {
  cat("mean of element named", i, "=", mean(df[i], na.rm = TRUE), fill=TRUE)
  
  # print(class(df[i]))
}
```

</details>

### Looping over indices


**Syntax**: `for (i in 1:length(object_name))` OR `for (i in seq_along(object_name))`

- This approach iterates over the index positions of each element in the object
- There are two ways to create the loop sequence:
    - `length()` returns the number of elements in the input object, which we can use to create a sequence of index positions (i.e., `1:length(object_name)`)
    - `seq_along()` returns a sequence of numbers that represent the index positions for all elements in the input object (i.e., equivalent to `1:length(object_name)`)
- The value of `i` is equal to the element's _index position_ (rather than its _content_ or _name_)
- But note that it is still possible to access the element's content inside the loop:
    - Access element contents using `object_name[i]`
        - Same object type as `object_name`; retains attributes (e.g., _name_)
    - Access element contents using `object_name[[i]]`
        - Removes level of hierarchy, thereby removing attributes
        - Approach recommended by Wickham because it isolates value of element
- Similarly, we can access the element's name by its index using `names(object_name)[i]` or `names(object_name)[[i]]`
    - In this case, using `[[]]` and `[]` are equivalent because `names()` returns an unnamed vector, which does not have any attributes

<br>
**Example**: Looping over elements in `vec`


```r
vec  # View named atomic vector object
```

```
##   a   b   c 
##   5 -10  30
```

```r
length(vec)  # View length of atomic vector object
```

```
## [1] 3
```

```r
1:length(vec)  # Create sequence from `1` to `length(vec)`
```

```
## [1] 1 2 3
```

```r
for (i in 1:length(vec)) {
  cat("\nvalue of object i =", i, "; type =", typeof(i), fill=TRUE)
  str(vec[i])  # Access element contents using []
  str(vec[[i]])  # Access element contents using [[]]
}
```

```
## 
## value of object i = 1 ; type = integer
##  Named num 5
##  - attr(*, "names")= chr "a"
##  num 5
## 
## value of object i = 2 ; type = integer
##  Named num -10
##  - attr(*, "names")= chr "b"
##  num -10
## 
## value of object i = 3 ; type = integer
##  Named num 30
##  - attr(*, "names")= chr "c"
##  num 30
```



<br>
**Example**: Looping over elements in `df`


```r
df  # View dataframe object
```

```
## # A tibble: 4 x 3
##        a      b      c
##    <dbl>  <dbl>  <dbl>
## 1  0.586  0.606 -0.284
## 2  0.709 -1.82  -0.919
## 3 -0.109  0.630 -0.116
## 4 -0.453 -0.276  1.82
```

```r
seq_along(df)  # Equivalent to `1:length(df)`
```

```
## [1] 1 2 3
```

```r
for (i in seq_along(df)) {
  cat("\nvalue of object i =", i, "; type =", typeof(i), fill=TRUE)
  str(df[i])  # Access element contents using []
  str(df[[i]])  # Access element contents using [[]]
}
```

```
## 
## value of object i = 1 ; type = integer
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  1 variable:
##  $ a: num  0.586 0.709 -0.109 -0.453
##  num [1:4] 0.586 0.709 -0.109 -0.453
## 
## value of object i = 2 ; type = integer
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  1 variable:
##  $ b: num  0.606 -1.818 0.63 -0.276
##  num [1:4] 0.606 -1.818 0.63 -0.276
## 
## value of object i = 3 ; type = integer
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  1 variable:
##  $ c: num  -0.284 -0.919 -0.116 1.817
##  num [1:4] -0.284 -0.919 -0.116 1.817
```

<br>
We could also access the element's name by its index:


```r
names(df)  # View names of dataframe object (i.e., column names)
```

```
## [1] "a" "b" "c"
```

```r
names(df)[[2]]  # We can access any element in the names vector by its index
```

```
## [1] "b"
```

```r
# Incorporate the above line into the loop
for (i in 1:length(df)) {
  cat("i =", i, "; name =", names(df)[[i]], fill=TRUE)
}
```

```
## i = 1 ; name = a
## i = 2 ; name = b
## i = 3 ; name = c
```

<br>
<details><summary>**Example**: Calculating column averages for `df` by looping over column indices</summary>

Use `i in seq_along(df)` to loop over the column indices and `[[]]` to access column contents:


```r
str(df)  # View structure of dataframe object
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  3 variables:
##  $ a: num  0.586 0.709 -0.109 -0.453
##  $ b: num  0.606 -1.818 0.63 -0.276
##  $ c: num  -0.284 -0.919 -0.116 1.817
```

```r
for (i in seq_along(df)) {
  cat("mean of element at index position", i, "=", mean(df[[i]], na.rm = TRUE), fill=TRUE)
}
```

```
## mean of element at index position 1 = 0.1830486
## mean of element at index position 2 = -0.2145385
## mean of element at index position 3 = 0.1243956
```

</details>

### Summary

There are 3 ways to loop over elements of an object:

1. [Looping over the elements](#looping-over-elements)
2. [Looping over names of the elements](#looping-over-names)
3. [Looping over numeric indices associated with element position](#looping-over-indices) (approach recommended by Grolemnund and Wickham)
    - Grolemnund and Wickham recommends this approach (**#3**) because given an element's index position, we can also extract the element name (**#2**) and value (**#1**)



```r
for (i in seq_along(df)) {
  cat("i =", i, fill=TRUE)  # element's index position
  
  name <- names(df)[[i]]  # element's name (what we looped over in approach #2)
  cat("name =", name, fill=TRUE)
  
  value <- df[[i]]  # element's value (what we looped over in approach #1)
  cat("value =", value, "\n", fill=TRUE)
}
```

```
## i = 1
## name = a
## value = 0.5855288 0.709466 -0.1093033 -0.4534972 
## 
## i = 2
## name = b
## value = 0.6058875 -1.817956 0.6300986 -0.2761841 
## 
## i = 3
## name = c
## value = -0.2841597 -0.919322 -0.1162478 1.817312
```


## Modifying vs. creating object

Grolemund and Wickham differentiate between two types of tasks loops accomplish:

1. __Modifying an existing object__
    - Example: Looping through a set of variables in a dataframe to:
        - Modify these variables OR
        - Create new variables (within the existing dataframe object)
    - When writing loops in Stata/SAS/SPSS, we are usually modifying an existing object because these programs typically only have one object (a dataset) open at a time
2. __Creating a new object__
    - Example: Creating an object that has summary statistics for each variable, which can be the basis for a table or graph, etc.
    - The new object will often be a vector of results based on looping through elements of a dataframe
    - In R (as opposed to Stata/SAS/SPSS), creating a new object is very common because R can hold many objects at the same time


### Modifying an existing object

How to modify an existing object?

- Recall that we can directly access elements in an object (e.g., atomic vector, lists) using `[[]]`. We can use this same notation to _modify_ the object.
- Even though atomic vectors can also be modified with `[]`, Wickhams recommends using `[[]]` in all cases to make it clear we are working with a single element (from [R for Data Science](https://r4ds.had.co.nz/iteration.html#modifying-an-existing-object))

<br>
<details><summary>**Example**: Modifying an existing atomic vector</summary>

Recall our named atomic vector `vec` from the previous examples:


```r
vec
```

```
##   a   b   c 
##   5 -10  30
```

We can loop over the index positions and use `[[]]` to modify the object:


```r
for (i in seq_along(vec)) {
  vec[[i]] <- vec[[i]] * 2  # Double each element
}

vec
```

```
##   a   b   c 
##  10 -20  60
```

</details>

<br>
<details><summary>**Example**: Modifying an existing dataframe</summary>

Recall our dataframe `df` from the previous examples:


```r
df
```

```
## # A tibble: 4 x 3
##        a      b      c
##    <dbl>  <dbl>  <dbl>
## 1  0.586  0.606 -0.284
## 2  0.709 -1.82  -0.919
## 3 -0.109  0.630 -0.116
## 4 -0.453 -0.276  1.82
```

We can loop over the index positions and use `[[]]` to modify the object:


```r
for (i in seq_along(df)) {
  df[[i]] <- df[[i]] * 2  # Double each element
}

df
```

```
## # A tibble: 4 x 3
##        a      b      c
##    <dbl>  <dbl>  <dbl>
## 1  1.17   1.21  -0.568
## 2  1.42  -3.64  -1.84 
## 3 -0.219  1.26  -0.232
## 4 -0.907 -0.552  3.63
```

</details>


### Creating a new object

So far our loops have two components: 

1. Sequence
1. Body

When we create a new object to store the results of a loop, our loops have three components:

1. Sequence
1. Body
1. **Output** (_This is the new object that will store the results created from your loop_)

<br>
Grolemund and Wickham recommend using `vector()` to create this new object __prior__ to writing the loop (rather than creating the new object within the loop):

> "Before you start loop...allocate sufficient space for the output. This is very important for efficiency: if you grow the for loop at each iteration using `c()` (for example), your for loop will be very slow."

<br>
__The `vector()` function__:


```r
?vector

# SYNTAX AND DEFAULT VALUES
vector(mode = "logical", length = 0)
```

- Function: Creates a new vector object of the given length and mode
- Arguments:
  - `mode`: Type of vector to create (e.g., `"logical"`, `"numeric"`, `"list"`)
  - `length`: Length of the vector

<br>
<details><summary>**Example**: Creating a new object to store dataframe column averages</summary>

Recall the previous example where we calculated the mean value of each column in dataframe `df`:


```r
str(df)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  3 variables:
##  $ a: num  1.171 1.419 -0.219 -0.907
##  $ b: num  1.212 -3.636 1.26 -0.552
##  $ c: num  -0.568 -1.839 -0.232 3.635
```

```r
for (i in seq_along(df)) {
  cat("mean of element at index position", i, "=", mean(df[[i]], na.rm = TRUE), fill=TRUE)
}
```

```
## mean of element at index position 1 = 0.3660972
## mean of element at index position 2 = -0.429077
## mean of element at index position 3 = 0.2487912
```

<br>
Let's create a new object to store these column averages. Specifically, we'll create a new numeric vector whose length is equal to the number of columns in `df`:


```r
output <- vector(mode = "numeric", length = length(df))
class(output)  # Specified by `mode` argument in `vector()`
```

```
## [1] "numeric"
```

```r
length(output)  # Specified by `length` argument in `vector()`
```

```
## [1] 3
```

<br>
We can loop over the index positions of `df` and use `[[]]` to modify `output`:


```r
for (i in seq_along(df)) {
  output[[i]] <- mean(df[[i]], na.rm = TRUE)  # Mean of df[[1]] assigned to output[[1]], etc.
}

output
```

```
## [1]  0.3660972 -0.4290770  0.2487912
```

</details>

## Summary

The general recipe for how to write a loop:

1. Complete the task for one instance outside a loop (this is akin to writing the __body__ of the loop)

2. Write the __sequence__ 

3. Which parts of the body need to change with each iteration

4. _If_ you are creating a new object to store output of the loop, create this outside of the loop

5. Construct the loop

<br>
<details><summary>**When to write a loop vs a function [SKIP]**</summary>

It's usually obvious when you are duplicating code, but unclear whether you should write a loop or whether you should write a function.

- Often, a repeated task can be completed with a loop or a function

In my experience, loops are better for repeated tasks when the individual tasks are __very__ similar to one another

- E.g., a loop that reads in datasets from individual years; each dataset you read in differs only by directory and name
- E.g., a loop that converts negative values to `NA` for a set of variables

Because functions can have many arguments, functions are better when the individual tasks differ substantially from one another 

- E.g., a function that runs regression and creates formatted results table
    - Function allows you to specify (as function arguments): dependent variable; independent variables; what model to run, etc.

__Note__:

- Can embed loops within functions; can call functions within loops
- But for now, just try to understand basics of functions and loops

</details>


## Practice: Download IPEDS 

EXPLAIN OBJECTIVE OF EXAMPLE

PASTE RELEVANT CODE FROM R SCRIPT INTO R CODE CHUNKS OR PROVIDE LINK TO R SCRIPT


# Conditional execution

TEXT

# Function basics

TEXT