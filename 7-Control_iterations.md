### if...else...

Control statemenst are very useful part of the programming languages as it gives the coder the ability to decide the flow of the code depending on ceratin test or values within the code.
We will discuss some of these `flow control` options here

#### if and else
**if and else** also used as **if and (else if)n and else **

Below is an example to illusterate if...else... statement.

In a client account in a bank to keep a track of the account balance we have to monitor deposit and withdrawl the flow chrat will be some thing like this

```R

clientBalance <- function(currentBalance=0,deposit=0,withdrawl=0)
{
  newBalance=currentBalance+deposit
  if ((newBalance-withdrawl) < 0 ){ 
    print("Insufficient Funds")
    }else{ 
    newBalance=newBalance-withdrawl
    print("Transaction Successful")
    }
  print(paste("Your new account balance is: ",newBalance," USD"  ))
  return(newBalance)
  
}


clientBalance(200,20,10)

clientBalance(200,20,1000)

clientBalance(200,0,1000)

```
Being customer friendly bank the bank want to inform customer when the balance beccomes zero advising the customer to add funds to account.  Let's include that in above code.


```R

clientBalance <- function(currentBalance=0,deposit=0,withdrawl=0)
{
  newBalance=currentBalance+deposit
  if ((newBalance-withdrawl) < 0 ){ 
    print("Insufficient Funds, Withdrawl denied")
    }else if ((newBalance-withdrawl)==0 ){ 
     print("Transction is succesful.  Your funds are 0 (zero), please add more funds.")
     newBalance=newBalance-withdrawl
    }else{  
    newBalance=newBalance-withdrawl
    print("Transaction Successful")
    }
  print(paste("Your new account balance is: ",newBalance," USD"  ))
  return(newBalance)
}


clientBalance(200,20,220)

clientBalance(200,20,1000)

```
In case `if...else...` got a binary (only 2 options) output then the `if...else...` statement can be composed as showm below
```R
a=1
ifelse(a==1,"Yes","No")

```
This can be useful if the elements of a vector has to be treated differently based on certain criteria. This takes advantage of simple `ifelse` command and the fact that vectors in R are vectorised.

```R
chipEnrichment<-c(12,34,5,23,56,7,89,102,1,2,34,22,67,12,10)
threshold = mean(chipEnrichment)

#Is the enrichment above the threshold? Answer: Yes or No
ifelse(chipEnrichment>threshold,"Yes","No")
#Is the enrichment above the threshold? Answer: if value is below threshold convert it to 0.
ifelse(chipEnrichment>threshold,chipEnrichment,0)

# In order to estimate fold enrichment of values above the threshold
ifelse(chipEnrichment>threshold,chipEnrichment/threshold,0)

# The binary values can be characters as shown below
ifelse(chipEnrichment>threshold,"Enrichment","BackGround")

```

####Compound Tests
There will be scenerios when we would like to test two conditions before calling the output true. Example if we are testing that binding of a transcription factor at a promoter increases the trancription of the gene. In this case both the binding of transcription factor(enrichment at loci) in the promoter region and changes in transcription of the same gene has to happen to call that trancription factor has an effect on given gene.

```R
chipEnrichment<-c(12,34,5,23,56,97,89,102,1,2,34,22,67,12,10)
threshold = mean(chipEnrichment)

trancriptionChange <- c(1.32, 1.22, 3.1, 1.1, 4.2, 1.7, 3.3, 2.4, 8, 1, 2.8, 1, 3.33, 1, 1)

# Test if both enrichment and transcription foldchange is true

ifelse(chipEnrichment>threshold & trancriptionChange >2,"Yes","No")

options(digits=3) 

data.frame(chipEnrichment=(ifelse(chipEnrichment>threshold,chipEnrichment/threshold,0)),trancriptionChange = c(1.32, 1.22, 3.1, 1.1, 4.2, 1.7, 3.3, 2.4, 8, 1, 2.8, 1, 3.33, 1, 1),result=ifelse(chipEnrichment>threshold & trancriptionChange >2,"Yes","No") )

# Test if both enrichment or transcription foldchange is true (One of them is true)

ifelse(chipEnrichment>threshold | trancriptionChange >2,"Yes","No")

data.frame(chipEnrichment=ifelse(chipEnrichment>threshold,chipEnrichment/threshold,0),trancriptionChange = c(1.32, 1.22, 3.1, 1.1, 4.2, 1.7, 3.3, 2.4, 8, 1, 2.8, 1, 3.33, 1, 1),result=ifelse(chipEnrichment>threshold | trancriptionChange >2,"Yes","No") )

```

### for Loops
`for` loops are used to iterate over each elements of data object.  We are considering a vector as an example and multiplying each element with 3. 

```R
lst<-c(1:10)
lst
#Using for loop.
# for loop will pick up one element at a time and the picked element is assigned to a variable and then the rest of the operation is carried out on that variable.
#after that it picks next element and assign it to the variable and carry out the rest of the operation detailed in for loop. This repeats untill all the elements are finished
m<-c()
for (x in lst){
  print(x*3)
   m<-c(m,x*3)
}
m

# Above code carry out the multiplication of each element with 3, but so does the code below
lst*3

#So for loop is not ideal in such situation, what if we have to do operation based on the value.for e.g. values below 4 are multiplied by 2 and greater than equalto 4 are divided by 2.  So the code will be

for (x in lst){
  if (x<4){
    print(x*2)
  }else{
    print(x/2)
    }
  }

#Above result can be achieved by single line code below

ifelse(lst<4,lst*2,lst/2)

## SO WHY FOR LOOP? 
# For loops are useful  when we want to have more than 2 criterias to filter values.
#e.g

lst<-c(1:10)
for (x in lst){
  if (x<4){
    print(paste(x,"low"))
  }else if(x>=4 & x<=7){
    print(paste(x,"medium"))
  }else{
    print(paste(x,"high"))
  }
  }


```
### While loops
While loops are used when exit from the loop detemined by logic which we are not sure when it will be achieved.e.g Keep checking the numbers until you find 100th prime number.

e.g find the number whose square is less than 169

```R
#lets start checking from 0, so if x is a counter,  we will set it to 0
x=0

#Now keep checking the numbers for their square and stop when the square is 169.
# Be aware of running into infinite loops e.g what happens if we mistype 169 as 168.

while (x**2 != 169){
  print(x)
  x<-x+1
}

```

### Controlling loops

##### next and break

**next** 
Skip a loop/value based on criteria set
e.g donot print the value whose square root is 2

```R
x<-(1:10)
x
for (value in x){
  if (value**(1/2)==2){
    next
  }else{
    print(value)
  }
}

```
**break**
In above example, let's stop the loop once we have found the value whose square root is 3.
```R
x<-(1:20)
x
for (value in x){
  if (value**(1/2)==3){
    print(value)
    break
  }else{
    next
  }
}

```
######  *HOMEWORK* :Try writing a code/function to find nth prime number. 


