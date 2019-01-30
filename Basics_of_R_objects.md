## Basics of R

**Maths operations**

Simple mathematical calculations can be carried out using R. Some examples are demonstrated below.


```R
> 2 + 1       # Addition
[1] 3

> 4 / 2       # Divison
[1] 2

> 7 / 2       # Fraction, Decimal
[1] 3.5

> 7 %/% 2     # integer
[1] 3

> 2 - 1       # Subtraction
[1] 1

> 1 - 2       # Subtraction
[1] -1

> 1 + 2 + 5 
[1] 8

> 4 * 4       # Multiplication
[1] 16

> 4 * (2 + 3) 
[1] 20

> 2 ** 3      # Exponent
[1] 8

> 16 ** (1/2) #`Square root
[1] 4

> 16 ** (0.5) # Square root
[1] 4
```
Spaces between operators is not required but it is a good coding practice.

Every time we do a calculation the operation is done and result is displayed.  If we have to use the result value 100 times we have to do the same operation 100 times.  It is ok if the calculations are simple but if we considera scenerio for complex mathematical calculation on large table (100,000 rows, 1000 columns) this will become coputationally intensive and waste of resources. 
In such situations **Variables** comes handy as they can store a value or result and that value can be called anytime needed.

**Variables**
Variables are essential part of any programming language.  Unlike C, R Does not require a viable to be declared. A variable can be assigned different type of objects dynamically.

Variable can be alphanumeric and can contain "." and "_", however they cannot start with a number or an underscore.

Variable assignment is carried out by using `<-` or `=` operators. `<-` supersede `=` .

e.g
```R
> x <- 2
> x
[1] 2

> y = 5
> y
[1] 5

> x="Nucleosome"
> x
[1] "Nucleosome"

> source="Bioconductor"
> source
[1] "Bioconductor"
> Source
Error: object 'Source' not found

> a <- b <- 5
> a
[1] 5
> b
[1] 5
> b <- 6
> b
[1] 6
> a
[1] 5

> assign("year",2019)
> year
[1] 2019

> NY2Boston <- 5
> NY2Boston
[1] 5

> NY2Boston <- "5h"
> NY2Boston
[1] "5h"

> NY2Boston <- 5h
Error: unexpected symbol in "NY2Boston <- 5h"

```
Variables created in a session are present in your environment.  To list all the variables use `ls()` or check the *Environment* Tab of R studio.

**Removing variables**
To remove a given variable try `rm(variableName)`.  In order to remove all the environment variables try `rm(list=ls())`.

##Data Types

**Numeric Data**
It include integers and fractions.
```R
> x <- 3
> is.numeric(x)
[1] TRUE

> is.integer(x)
[1] FALSE

> x <- 3L
> is.numeric(x)
[1] TRUE
> is.integer(x)
[1] TRUE

> y<-4.44
> is.numeric(y)
[1] TRUE
> is.integer(y)
[1] FALSE
> class(y)
[1] "numeric"

>  si <- 7L
> class(si)
[1] "integer"

>  si <- 7L * 2.2
> class(si)
[1] "numeric"

> class(4L/2L)
[1] "numeric"

> m <- ( 4L / 2L)
> m
[1] 2

> m <- as.integer( 4L / 2L)
> m
[1] 2
> class(m)
[1] "integer"
> m
[1] 2

> as.integer(2.2)
[1] 2
```
**Character Data **

Character data also known as string data type are of 2 types `character` and `factor`. While they seems similar on surface they are treated very differently in codes/execution. To count the number of characters in string use `nchar`

```R
> n <- "name"
> class(n)
[1] "character"

> f<-factor(n)
> f
[1] name
Levels: name

> nchar(n)
[1] 4

> nchar(f)
Error in nchar(f) : 'nchar()' requires a character vector

> age <- 24
> class(age)
[1] "numeric"

> age <- "24"
> class(age)
[1] "character"

> age <- as.character(24)
> class(age)
[1] "character"
```
**Logical**
Logical is the way of representing data which is either `TRUE` or `FALSE`.  Numerically `TRUE` is represented as 1 and `FALSE` as 0. So mathmatical operations can be carried out using these values, as given in examples below.

```R
> x <- 5
> y <- (10/2)
> x == y
[1] TRUE

> m <- (x == y)
> m
[1] TRUE

> m*20
[1] 20


> x != y
[1] FALSE

> t <- ( x != y )
> t*4
[1] 0

> (x != y)* 6
[1] 0

>  class(m)
[1] "logical"

> class(t)
[1] "logical"

>  3 == 4
[1] FALSE

> 3 != 4
[1] TRUE

> 3 < 4
[1] TRUE

> 3 <= 4
[1] TRUE

> m != t
[1] TRUE

> m == t
[1] FALSE

> "country" == "world"
[1] FALSE

> "country" < "world"
[1] TRUE

```
**Vectors**

A vector is collection of values/elements of the same type. A vector can be collection of exclusively `numeric` or `character` or `logical` value types. A vector cannot be of mix type. If they are not of the same type, the values will be coerced to one type.   

1) Vectors are the simplest of the containers in R holding multiple elements.  
2) R is a vectorised language that means that an operation is automatically applied to each element of the vector without  the need of loop through the vector. 
3) Vectors are without dimensions which means that there is no such thing as column vector or row vector.

The most common way of creating a vector is with `c()`. The `c` stands for combine as multiple elemets are being combined into a vector.

```R
> name <- c("Tom Owen-Hughes", "Elisa Garcia Wilson", "Nicola Wiechens", "David Dickerson", "Amanda Hughes")
> name
[1] "Tom Owen-Hughes"     "Elisa Garcia Wilson" "Nicola Wiechens"     "David Dickerson"     "Amanda Hughes"      
> class(name)
[1] "character"
> dim(name)
NULL
> length(name)
[1] 5
> nchar(name)
[1] 15 19 15 15 13

> age <- c(54, 32,42,44,34)
> class(age)
[1] "numeric"
> length(age)
[1] 5
> dim(age)
NULL

> age * 2
[1] 108  64  84  88  68

> age + 5
[1] 59 37 47 49 39

> age -10
[1] 44 22 32 34 24

> age / 2
[1] 27 16 21 22 17

> sqrt(age)
[1] 7.348469 5.656854 6.480741 6.633250 5.830952

> age < 40
[1] FALSE  TRUE FALSE FALSE  TRUE

> (age < 40) *2
[1] 0 2 0 0 2
```
Creating numeric vectors. 
Syntax: m <- c(a:b)  # create vector m containing elemets starting from a and every next element increase or decreases by 1 untill the last value <=b.
```r
> x <- c(1:10)
> x
 [1]  1  2  3  4  5  6  7  8  9 10

> y <- (-5:5)
> y
 [1] -5 -4 -3 -2 -1  0  1  2  3  4  5

> m<-c(2000:2019)
> m
 [1] 2000 2001 2002 2003 2004 2005 2006 2007 2008 2009 2010 2011 2012 2013 2014 2015 2016 2017 2018 2019

> x<-c(1:10,12,14)
> x
 [1]  1  2  3  4  5  6  7  8  9 10 12 14

> length(x)
[1] 12

> x**2
 [1]   1   4   9  16  25  36  49  64  81 100 144 196

> x+2
 [1]  3  4  5  6  7  8  9 10 11 12 14 16

> x+c(2,3)
 [1]  3  5  5  7  7  9  9 11 11 13 14 17

> x+c(2,3,7)
 [1]  3  5 10  6  8 13  9 11 16 12 15 21

> x<4
 [1]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

> (x<4)*3
 [1] 3 3 3 0 0 0 0 0 0 0 0 0
 
> x<-c(1:10)
> y<-c(5:-5)
> x
 [1]  1  2  3  4  5  6  7  8  9 10
> y
 [1]  5  4  3  2  1  0 -1 -2 -3 -4 -5
> any(x < y)
[1] TRUE
Warning message:
In x < y : longer object length is not a multiple of shorter object length

> x<-c(0:10)
> any(x < y)                          #any
[1] TRUE

> all(x < y)                          #all
[1] FALSE
 
exists("name")                        # to check if a vaiable exists in environment.
 
```
Accessing elements of a vector is done by using [ ]. example is given below

```R
> name
[1] "Tom Owen-Hughes"     "Elisa Garcia Wilson" "Nicola Wiechens"     "David Dickerson"     "Amanda Hughes"      
> name[1]
[1] "Tom Owen-Hughes"
> name[5]
[1] "Amanda Hughes"
> name[1:3]
[1] "Tom Owen-Hughes"     "Elisa Garcia Wilson" "Nicola Wiechens"    
> name[c(1,3,5)]
[1] "Tom Owen-Hughes" "Nicola Wiechens" "Amanda Hughes"
```

Naming elements in a vector;

```R
> prices <-c(2.50, 3.10, 3.25)

> names(prices) <-c("Latte","Expresso","Ice Tea")
> prices
   Latte Expresso  Ice Tea 
    2.50     3.10     3.25 

> prices[3]
Ice Tea 
   3.25 

> price_b<-c("Latte"=2.50,"Expresso"=3.10,"Ice Tea"=3.25)
> price_b
   Latte Expresso  Ice Tea 
    2.50     3.10     3.25 
```
Coercio:  Changing the type of element in a vector. character <- numeric <->integer -> character

```R
> height <- c(175, 181,164,159)
> class(height)
[1] "numeric"

> height <- c(175, 181,164,159, "NA")
> class(height)
[1] "character"

> height
[1] "175" "181" "164" "159" "NA" 
> height <- c(175, 181,164,159, NA)
> class(height)
[1] "numeric"

> height <- c(175, 181,164,159, -Inf)
> class(height)
[1] "numeric"

> height <- c(175, 181,164,159, Inf)
> class(height)
[1] "numeric"

> height <- c(175, 181,164,159, TRUE)
> class(height)
[1] "numeric"

> height <- c(175, 181,164,159, age)
> class(height)
[1] "numeric"
> height
[1] 175 181 164 159  54  32  42  44  34


> height <- c(175, 181,164,159, "left")
> class(height)
[1] "character"

> values<-c(2L,3L,5L)
> class(values)
[1] "integer"

> values<-c(2L,3L,5L,6)
> class(values)
[1] "numeric"

> values<-c(2L,3L,5L,6,"b")
> class(values)
[1] "character"
```

Adding values to vector
```R
> height
[1] 175 181 164 159 
> x=165
> height<-c(height,x)
> height
 [1] 175 181 164 159  165
```

**FACTOR Vectors**

Factor is categoring character vector into categories.
e.g: Sports opted by 10 students
```R
> choices<-c("hockey","soccer","Tennis","hockey","basketball","basketball","hockey","basketball","hockey","Tennis")

> choices
 [1] "hockey"     "soccer"     "Tennis"     "hockey"     "basketball" "basketball" "hockey"     "basketball" "hockey"    
[10] "Tennis"    

> as.factor(choices)
 [1] hockey     soccer     Tennis     hockey     basketball basketball hockey     basketball hockey     Tennis    
Levels: basketball hockey soccer Tennis

> choices.factor<-as.factor(choices)

> choices.factor
 [1] hockey     soccer     Tennis     hockey     basketball basketball hockey     basketball hockey     Tennis    
Levels: basketball hockey soccer Tennis

> as.numeric(choices.factor)
 [1] 2 3 4 2 1 1 2 1 2 4
```

In ordinary factors the order of the levels doesnot matter and one level is no different from another.  Sometimes, however it is important to understand  the order of the factors. e.g. performance of 10 dancers in a competition.

```R
> performance <- c("good","good","average","good","excellent","average","absent","average","absent","excellent")
> factor(performance,levels=c("excellent","good","average","absent"), ordered=TRUE)
 [1] good      good      average   good      excellent average   absent    average   absent    excellent
Levels: excellent < good < average < absent    
```


**Calling Functions**

Earlier we used some basic functions like `nchar` , `length`, `any` etc.  They are quite useful as they make the process of code writing easy and repitable.  The functions we have used are fairly simple ones we will encounter complex functions in future sessions. Almost every step taken in R involves using function, so it is best to learn the proper way to call them.  This means to understand what data format the function takes and what variables are set as default and which ones as a user we have to setup.

example the mean function whiich calulates mean of a vector with numeric or integer values.
```R
> gpa<-c(8.9,7.2,9.6,8.5,7.9,7.8,8.3,9.1,8.2,7.5)
> mean(gpa)
[1] 8.3
```

**Function Documentation**
The function in R have varying degree of documentation available from very well documented to no documentation at all.  The easiest  way to find a documentation is to place a question mark in front of the function.  e.g. as shown below
```R
> ?mean
> ?`+`
> ?`==`
```
Sometimes we donot remember a function but have a sense about the functio, in such cases, `apropos()` function is very useful e.g
```R
> apropos("line")
 [1] ".rs.lineDataList"              ".rs.pyStackItemToLineDataList" ".rs.readLines"                
 [4] ".rs.stepsAtLine"               "abline"                        "contourLines"                 
 [7] "findLineNum"                   "getSrcLines"                   "line"                         
[10] "linearizeMlist"                "lines"                         "lines.default"                
[13] "matlines"                      "qqline"                        "readline"                     
[16] "readLines"                     "smooth.spline"                 "spline"                       
[19] "splinefun"                     "splinefunH"                    "writeLines"                   
[22] "xspline" 
```

**Missing Data**
Missing Data is a an unavoidable instance in many large datasets.  In R they are of two types `NA` and `NULL` While they are similar they behaves differently and needs attention.

1) `NA` : Missing data is noted in datasets using different values such as dash, period or even number 99.  R uses `NA` for missing Data.  R uses `NA` as nother element in vector. `is.na` is to test each lement of vector missingness.

```R
> time<-c(2.5,3.5,6.6,NA,4.5,2.9)
> time
[1] 2.5 3.5 6.6  NA 4.5 2.9
> is.na(time)
[1] FALSE FALSE FALSE  TRUE FALSE FALSE

> students<-c("Eric","Dan","Victor",NA, "Emily")
> is.na(students)
[1] FALSE FALSE FALSE  TRUE FALSE
```
2) `NULL` :  Null is absence of anything.  It is not exactly missingness, it is nothingness.  Functions can sometime return NULL or their arguments are NULL.  example the dimensions of a vector, the output of the function is NULL. An important difference between NA and NULL is that NULL is atomical and cannot exists within a vector.  If used in vector it simply disappears.  The test for NULL is `is.null()` but since null cannot be part of a vector , is.null is not vectorised.  example

```R
> steps<-c(20,40,35,NULL,44)
> steps
[1] 20 40 35 44

> z<-NULL
> z
NULL
> is.null(z)
[1] TRUE

> is.null(steps)
[1] FALSE
```
