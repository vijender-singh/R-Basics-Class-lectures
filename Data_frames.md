### data.frames

Data frames are similar to Excel spreadsheet and has columns and rows.  It is a 2 dimensional objects with rows and columns. Each column of dataframe are vectors of same length.  That means the columns can be of only one class type  (character, numeric or integer class).  If mixed class is provided data gets coerced as we have seen in the case of vectors.


**Ways to create dataframe**
```{R}
x<-c("Gene1","Gene2","Gene3","Gene4","Gene5","Gene6","Gene7","Gene8","Gene9","Gene10")
y<-c("Chr1","Chr1","Chr1","Chr1","Chr2","Chr2","Chr2","Chr3","Chr3","Chr4")
p<-c(11234,21234,25452,32414,156009,297862,299220,312112,141789,13114)
e<-c(2,2.3,3.5,2.8,1.98,2.76,3.76,2.45,NA,3.4)

chip<-data.frame(x,y,p,e)
chip

```
In the above example we have created a dataframe `chip` with 10 rows and 4 columns.  We can create the same data frame with column labels as

```{R}
Gene<-c("Gene1","Gene2","Gene3","Gene4","Gene5","Gene6","Gene7","Gene8","Gene9","Gene10")
Chromosome<-c("Chr1","Chr1","Chr1","Chr1","Chr2","Chr2","Chr2","Chr3","Chr3","Chr4")
Position<-c(11234,21234,25452,32414,156009,297862,299220,312112,141789,13114)
Enrichment<-c(2,2.3,3.5,2.8,1.98,2.76,3.76,2.45,NA,3.4)

chip1<-data.frame(Gene,Chromosome,Position,Enrichment)
chip1

```
or

```{R}
chip2<-data.frame(Gene=c("Gene1","Gene2","Gene3","Gene4","Gene5","Gene6","Gene7","Gene8","Gene9","Gene10"), 
Chromosome = c("Chr1","Chr1","Chr1","Chr1","Chr2","Chr2","Chr2","Chr3","Chr3","Chr4"), Position=c(11234,21234,25452,32414,156009,297862,299220,312112,141789,13114), Enrichment=c(2,2.3,3.5,2.8,1.98,2.76,3.76,2.45,NA,3.4))

chip2

```

In the above example the 4 vectors each with a single data type became 4 columns of the dataframe. 



**Attributes of Dataframe**

```{R}
nrow(chip2) # Number of Rows

ncol(chip2) # Number of columns

dim(chip2)  # dimension of data frame Rows X Columns 

names(chip2) # Column Names

rownames(chip2) # Row names

rownames(chip2) <- c("ASl1","ALD1","BAS2","CKT23","DLU01","KRT2","MPP23","NSP05","VWR2","ZMN1") # Assigning rownames instead of default 1,2,3....N

rownames(chip2)    # list rownames

rownames(chip2) <- NULL      # Remove row names

colnames(chip2)    # Display column labels

colnames(chip2) <- c("GeneID","Chr","Pos","Enr")  # Reassigning the column names

class(chip2)  # object type

```

**Viewing Dataframes**
```{R}
head(chip2)   # Display top of the dataframe, default 6 rows

head(chip2,4) # Outputs first 4 rows

tail(chip2)  #Outputs last 6 rows of dataframe.  Deafult rows are 6.

tail(chip2,4)  # Displays last 4 rows.

View(chip2)  # Output full dataset

```

**Selecting Columns and Rows**

The columns of a dataframe can be selected either using column index or column names.  The indexing in R is 1 based unlike python which is zero based. 

```{R}
chip2[1]     # Select 1st column,  output is a dataframe

chip2$Chr    # Select column with name Chr same as chip2[,2], Output is a vector

#Selecting Rows

chip2[2,]   #Select 2nd row

chip2[1:5,2:4] # select 1 to 5 rows and 2 to 4 columns

chip2[3,4] # select value in 3rd row and 4th column

chip2[,c(1,3)] # Select all rows and column 1 and 3.

chip2[,c("Chr","Enr")]  # Selecting columns with colnames


chip2[1:3,2] # 2 column 1to 3 rows

class(chip2[1:3,2]) # Output is not a dataframe

chip2[1:3,2,drop=FALSE] # Output is a datatframe

```

**Selecting/Omitting columns with NA**

```{R}
#SELECTING
# Selecting the row(s) with NA in column 4 of chip2.  If there were NAs in any other column that would be ignored.

chip2[is.na(chip2[4]),]  

#or
# Selecting the row(s) with NA in Enr column of chip2. If there were NAs in any other column that would be ignored.

chip2[is.na(chip2$Enr),]  


#OMITTING

# Selecting the row(s) without NA in column 4 of chip2. If there were NAs in any other column that would be ignored.

chip2[!is.na(chip2[4]),] 

#or
# Selecting the row(s) without NA in Enr column of chip2. If there were NAs in any other column that would be ignored.clear

chip2[!is.na(chip2$Enr),]  


```

**PLease Practise different scenerios and posiblities as you can.**

#MERGING TABLES USING WITH BASE R FUNCTION merge

The excercise below demonstartes how to merge or combine two dataframes using `R`'s in built function `merge`. The help file for `merge`
 function can be obtained using `?merge` command. The syntax of `merge` changes based on the dataframes that are to be joined.
 
 Below is an example of merging 2 dataframes `chip2` and `exp` using the column name `geneID` present in both datasets.  
 **NOTE:  Be sure that the column used for merging holds the same type data.  There will be instances when the column name is same but the data under them could be of different types.**
 
```{R}
chip2<-data.frame(Gene=c("Gene1","Gene2","Gene3","Gene4","Gene5","Gene6","Gene7","Gene8","Gene9","Gene10"), 
                  Chromosome = c("Chr1","Chr1","Chr1","Chr1","Chr2","Chr2","Chr2","Chr3","Chr3","Chr4"),
                  Position=c(11234,21234,25452,32414,156009,297862,299220,312112,141789,13114), 
                  Enrichment=c(2,2.3,3.5,2.8,1.98,2.76,3.76,2.45,NA,3.4),
                  geneID=c("ASl1","ALD1","BAS2","CKT23","DLU01","KRT2","MPP23","NSP05","VWR2","ZMN1"))
chip2


exp<-data.frame(
  geneID=c("ASl1","ALD1","BAS2","CKT23","DLU01","KRT2","MPP23","NSP05","VWR2","ZMN1"),
  expression=c(231,0, 23,450,980,12,5,0,1,4))

exp

#MERGING CODE :  Both commands will work eqully well.
# since the merge dataframe is not assigned to a variable, it will be displayed and lost not stored for later use.

merge(chip2,exp, by="geneID")  # Works only when the columns used to merge has same column name in both dataframes.

merge(chip2,exp, by.x="geneID",by.y="geneID") # Useful when the columns used to merge has different column name.


# Assigning merge dataframe to a variable is a good practice.  Here chip2exp holds the merged dataframe.

chip2exp <-merge(chip2,exp, by="geneID")

chip2exp
```


In some cases the dataframes that are being merged could have different number of rows as shown in example below. `dfA` is dataframe with 5 rows X 2 columns, `dfB` with 6rows X 3columns.  There will be 4 possible ways in which we can combine these 2 data frames.

```{R}

dfA <- data.frame(geneID=c("ASF1", "GKT2","MMN34","TKT9","ZMN3"),chr=c(1,1,2,4,4))
dfA

dfB <- data.frame(geneID=c("ASF1","ELM1", "GKT2","KTN23","MMN34","TKT9"),TSS=c(1123,16766, 45532,71545,34567,45224),exp=c(213,2,453,11,32,908) )
dfB
```

**OptionA** : Merged output dataframe `dfAB1` has only the common observations (rows). 
```{R}

dfAB1 <- merge(dfA,dfB, by="geneID")
dfAB1
```

**OptionB** : Merged output dataframe `dfAB2` has all the observations (rows) of `dfA` and only the common one's from `dfB`. NA's will be introduced in columns of dfB where the values are not available.

```{R}

dfAB2 <- merge(dfA,dfB, by="geneID", all.x=T)
dfAB2
```


**OptionC** : Merged output dataframe `dfAB3` has all the observations (rows) of `dfB` and only the common one's from `dfA`. NA's will be introduced in columns of dfB where the values are not available.

```{R}

dfAB3 <- merge(dfA,dfB, by="geneID", all.y=T)
dfAB3
```

**OptionD** : Merged output dataframe `dfAB4`  has all the observations (rows) of `dfB` and `dfA`.  The common ones are represented only once. NA's will be introduced in columns where the values are not available.

```{R}

dfAB4 <- merge(dfA,dfB, by="geneID", all=T)
dfAB4
```


**Appending Dataframes with rows and columns**

Dataframes can be appended by adding new rows and columns.  The two function suitable for the purpose are `rbind` for rows and `cbind` for columns.

`rbind` : Add rows, the new data row should be supplied as dataframe.

`cbind` : Add columns, the new data columns should be supplied as vectors of same length else NA's will be introduced.

**Adding a row**

In example below, A new row is added to dataframe dfA for `geneID` "VIJ08" with `chr` value 5. To do so we first created a dataframe of 1 row and then used rbind function to add it to `dfA`.

```{R}
newgene<-data.frame(geneID="VIJ08",chr=5)
newgene

dfA<-rbind(dfA,newgene,make.row.names=T)
dfA
```

**Adding a new column**

In example below, a new column `cellcycle` is added to dataframe dfAB4.
```{R}
cellcycle<-c("G1","G2","G1","M","S","S","M")

dfAB4<-cbind(dfAB4,cellcycle)
dfAB4
```
