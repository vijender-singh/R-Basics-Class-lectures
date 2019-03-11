## Lists

List can be considered as containers that can hold R objects either of the same type or varying types.  A list can contain a vector , dataframe, variable, matrix, arrays or even another list in it.  Lists can be viewed as a solution to hold objects from various stages of analysis at a single place.
Lists are created with `list(element1,element2,element3,...,elementN)` function and each argument becomes the element of the list. Like `data.frames` lists can have names and also the elements too can have names using which elements can be stored and accessed.

```R
# Simple list with numeric and character elements
list(12,22,"chr")

# List with 2 vectors
list(c("chr1","chr2","chr3"),c(12312,57867,46587))


# List with mix of object types
list(c("chr1","chr2","chr3"),c(12312,57867,46587),"Sample1",124546654)



# More complex List with mix of object types, vector, numeric,character and a dataframe

chip2<-data.frame(Gene=c("Gene1","Gene2","Gene3","Gene4","Gene5","Gene6","Gene7","Gene8","Gene9","Gene10"), 
Chromosome = c("Chr1","Chr1","Chr1","Chr1","Chr2","Chr2","Chr2","Chr3","Chr3","Chr4"), Position=c(11234,21234,25452,32414,156009,297862,299220,312112,141789,13114), 
Enrichment=c(2,2.3,3.5,2.8,1.98,2.76,3.76,2.45,NA,3.4))

list(c("chr1","chr2","chr3"),c(12312,57867,46587),"Sample1",124546654, chip2)

```

As we have seen earlier that its of no use if we cannot retrieve this list later.  So we will assign it to variable, lets say list1

```R
list1 <- list(c("chr1","chr2","chr3"),c(12312,57867,46587),"Sample1",124546654, chip2)
list1
```
**Accessing elements of the list**

we can access the elemnets based on the index with syntax `list[[n]]` where n is the index of elemnet

```R
# to access the vector c(12312,57867,46587) whose index is 2 in list1 we will use
list1[[2]]

# In order to access the chip2 dataframe with index 5
list1[[5]]

```

We can access the above list "list1" anytime later during our data analysis session. If this list is expected to grow then it is a good idea to name each element so that we know their identities.

**Naming elements of the list**
Naming of elements can be done either **while creating the list** or **add names later to the elements of existing list**.  We will try the second option as we already have the list and then will try naming them while creating the list.

**Add names later to the elements of existing list**
```R
# We will add names to the list1

names(list1) <- c("selChrom","selpos","sample","EnrTable")

list1
#WHATS GONE WRONG?
```
Since the name vector `c("selChrom","selpos","sample","EnrTable") ` has only 4 names, so the first 4 elements of lists have names assigned to them and the last one is left "NA". If we donot want to name an element leave a "" empty quote at the corresponding place, otherwise provide a name to each element of the list.

```R
names(list1) <- c("selChrom","selpos","sample","","EnrTable")
list1
#OR

names(list1) <- c("selChrom","selpos","sample","ReadDepth","EnrTable")
list1

#OR

list1 <- list(selectedChrom=c("chr1","chr2","chr3"),selectedPosn=c(12312,57867,46587),SampleName="Sample1",ReadDepth=124546654, Chip2Data=chip2)

```

**Accessing elements of the list by names**

We can access elements of the list using names provided we have assigned a name to that element of the list.

```R
# we can access the vector "selpos" of list1 2 ways

list1$selpos

#and

list1[["selpos"]]

```
The both will yield the same result but their usage differs in programming.  For now lets not go in that domain.

**Excercise(1):**
what would be the correct code to access `position` column of the dataframe **EnrTable** as (Select all applicable)

a. as vector
b. as dataframe


1. `list1[[5]]$position`
2. `list1[[5]]["Position"]`
3. `list1[[5]]$Position`
4. `list1[["EnrTable"]]$Position`
5. `list1[["EnrTable"]]["Position"]`
6. `list1$EnrTable[3]`
7. `list1$EnrTable[,3]`
8. `list1$EnrTable["Position"]`
9. `list1$EnrTable$Position`
10. `list1$EnrTable[,"Position"]`


**Adding elements to the list**
```{R}
list1[["atest"]]<-346347
list1

```

**Changing value of an existing element**
```R
list1[[6]] <- 36738256
list1

#or

list1[["atest"]] <- 555555
list1
```

**Attributes of list**
```R
length(list1)

```

**Question**
If you assign 2 elements of the list a same name, which element will be reported if you retrieve the element by name.
as in example below what will be reported if I try `rank[["b"]` or `rank$b`

```R
rank <- list("a"=1,"b"=2,"b"=3)

```

------END OF LIST--------

## Matrices

Simply defined matrices are like dataframes with only one datatype either **numeric** or **integer** and never a character.

Matrices have attributes like rows, columns, rownames, colnames, dim, nrw and ncol. The important point to note is that the matrices are 2dimensional (only rows and columns) and that seperates them from arrays as they can be multidimensional.  We will discuss about arrays later.

**Creating simple matrices**

syntax of creating matrices
`matrix(data = NA, nrow = 1, ncol = 1, byrow = FALSE, dimnames = NULL)`

**data**	    :: an optional data vector (including a list or expression vector).<br />
**nrow**      :: the desired number of rows.<br /> 
**ncol**	    :: the desired number of columns.<br /> 
**byrow**     :: logical. If FALSE (the default) the matrix is filled by columns, otherwise the matrix is filled by rows.<br /> 
**dimnames**  :: A dimnames attribute for the matrix: NULL or a list of length 2 giving the row and column names respectively. <br /> 


```R
mc <- matrix(1:25,ncol=5)
mc

# above matrix can be also generated by commands
mr <- matrix(1:25,nrow=5)

mrc <-  matrix(1:25,nrow=5,ncol=5)


# If values has to be filled row wise
mrc2<- matrix(1:25,nrow=5,ncol=5,byrow=TRUE)

#using dimnames
mrc3<- matrix(1:25,nrow=5,byrow=TRUE,dimnames=list(c("a","b","c","d","e"),c("k","l","m","n","p")))

```
Try different attributes

```R
nrow(mrc3)
ncol(mrc3)
dim(mrc3)
rownames(mrc3)
colnames(mrc3)

#Adding 2 matrix

mrc3 + mrc

# Multiplying them

mrc3 * mrc

# Matrix multiplication, We will discuss the results in class.

mrc3 %*% mrc

```

**Converting dataframe to matrix and vice versa.**

Generate a counts dataframe holding expression `count` of genes from different samples.

```R

countData<-data.frame(gene=c("ATk1","CTA1","BCL5","DRA12","VKT11"),
                      sample1=c(12,220,323,452,111),
                      sample2=c(10,112,321,423,81),
                      sample3=c(23,122,142,156,344) )

countData

```
**Step1: Add RowNames**
```R
rownames(countData) <- countData$gene
countData

```
**Step2 : Drop gene column**

```R
countData<-countData[,-1]
countData
```
**Step3 : Convert into matrix**

```R
class (countData)

countDatam <-as.matrix(countData)
countDatam

class(countDatam)

```

**Matrix to Dataframe**
```{R}
countDataD <- as.data.frame(countDatam)
countDataD
class(countDatam)
class(countDataD)

```

The calculations below is to show the use of Matrices, We will discuss it in the class

```R
#Data Summary
summary(countDataD)

# Mean of all rows to be used for normalisation
normVector<-c(223.6,189.4,157.4)
normVector
#Scaling factor calculated from means
normValues<-(1/(normVector/ 157.4))
normValues

#Diagonal matrix of scalling factores
normMatrix <-diag(3) *normValues
normMatrix

#Scaled Dataframe
normCountsData <- countDatam %*% normMatrix
normCountsData

#Data Summary after Normalisation
summary(normCountsData)

```

--------------END OF MATRICES------------------


## Arrays

An array is essentially a multidemenional matrix.  The elements should be of same type and individual elements can accessed in a similar fashion using square brackets [a,b,c].  This indicates a X b X c dimensional array.
The first value a is the row, second value b is the column and third value c is the outer dimension.

```R
#create array of size 2 X 3 X 4 dimension
arrayOne <- array(1:24,dim=c(2,3,4))
arrayOne

#Get 1st row of all arrays
arrayOne[1, , ]

#Get 2nd row and 3 rd column value of all the arrays

arrayOne[2,3 , ]

# Get 2 row 3rd column and 2 dim value from array

arrayOne[2,3,2]

```

### THIS FINISHES THE DATA TYPES
