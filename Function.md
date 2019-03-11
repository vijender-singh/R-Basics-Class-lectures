## FUNCTION

As a R programmer you will find more than often circumstances when you would like to run same set of code again or reuse it. In such circumstances it is ideal that organoise our code in a way that it is reusable.  Functions is such an option to group the code together and make it reusable.

**SYNTAX**
`functionName <- function(){ #executable code here #  }`

Let us wite a code to calculate mean of a vector.

```R
vectorMean <- function(x){ 
  vectorSum <- sum(x)
  vectorLength <-length(x)
  meanOut = vectorSum/vectorLength
  print(meanOut)
  }

ages<-c(23,22,26,34,43,29)
vectorMean(ages)
```

This `vectorMean` code can be used to find the mean of any vector of any length. `x` in `vectorMean` function is refered as the `argument` of the function.  A function can have multiple arguments and also default values. e.g as we seen in the function `read.table` to read **.txt**  and **.csv** files some arguments are optional, some have preset default values.

```{R}
printName <- function(First,Last){
  print(paste("First Name: ", First," Second Name: ",Last ))
}

printName("Mac","Anderson")

#Giving only one argument will give an error "argument "second" is missing, with no default "
#printName("Mac")

```
**Setting Deault Values**

```R
printName <- function(First="NA",Last="NA"){
  print(paste("First Name: ", First," Last Name: ",Last ))
}

printName("Mac", "Anderson")

printName("Mac")

printName("Anderson")

# In all the above cases the first variable is considered as first name even if it is the lastname.
# The proper way to mention only the second name will be

printName(Last="Anderson")

#Another way of calling a function is to use do.call() methods
do.call(printName,args=list(First="John",Last="McEnroe"))

```

**Return Values**
Functions are general;ly used to compute some values so there should be a mechanism to supply these values back to the caller.  The varaibles created inside a function are temporary and will be deleted following the completion of function.
Let's revisit the `vectorMean` function and try to access the variables like `vectorSum` and `vectorLength` that were created during the execution of the function.

```R
vectorMean <- function(x){ 
  vectorSum <- sum(x)
  vectorLength <-length(x)
  meanOut = vectorSum/vectorLength
  print(meanOut)
  }

ages<-c(23,22,26,34,43,29)
vectorMean(ages)
#vectorSum
#vectorLength

```
 `Error: object 'vectorSum' not found` **and** `Error: object 'vectorLength' not found` **errors state that these variables donot exist.**
 
 To access any of the varaibles we have to return the values in the function.  There may be one or multiple `return` command at the end of the function. e.g below is the code where vectorSum, vectorLength and meanOut is returned

```R
vectorMean <- function(x){ 
  vectorSum <- sum(x)
  vectorLength <-length(x)
  meanOut = vectorSum/vectorLength
  return (list(sum=vectorSum,length=vectorLength,mean=meanOut))
  }

ages<-c(23,22,26,34,43,29)
x <- vectorMean(ages)
x$sum
x$length
x$mean

```
####################################################################################

