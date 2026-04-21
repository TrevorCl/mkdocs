---
tags:
  - HTML5
  - JavaScript
  - CSS
  - R
---

# r documentation 

=== "Notes"
    1. case sensitive

=== "Comments" 
    1. comments use hash
    2. comment followed by 4 dashs ---- is section header
    3. ctrl + shift + c comments out a block
    4. ctrl + shift + R adds sections


# Data types
Vectors
Lists
Matrices
Arrays
Factors
Data Frames

# VECTORS
## 6 types of atomic vectors
The simplest of these objects is the vector object and there are six data types of these atomic vectors, also termed as six classes of vectors. The other R-Objects are built upon the atomic vectors

Even when you write a single value it is a vector of length 1

=== "Logical"   
    v<- TRUE  

=== "Numeric"  
    v <- 23.8  

=== "Integer"  
    v <- 23L  

=== "Complex"  
    v <- 23+5i  

=== "Character"  
```  
   v <- "TRUE"  
   v <- 'TRUE'    
```  
=== "RAW"  
   v <- charToRaw("TRUE")  

## Multiple element vectors
```r
v <- 5:12   
v <- 3.4:10.4 
#if the last value is not in the sequence then it is left  
```

## seq operator  
```r
seq(from, to by = )  
v <- seq(5,9, by = 0.4)  
```

## c function  
```r
v <- c("apple", 5, TRUE) converts all to character type  
```

### indexing
```r
t <- c("Sun","Mon","Tue","Wed","Thurs","Fri","Sat")
```

#### Accessing vector elements using position
```r
u <- t[c(2,3,6)]
> "Mon" "Tue" "Fri"
```

#### Accessing vector elements using logical indexing
```r
v <- t[c(TRUE,FALSE,FALSE,FALSE,FALSE,TRUE,FALSE)]
> "Sun" "Fri"
```

#### Accessing vector elements using negative indexing
```r
# negative drops from the vector
x <- t[c(-2,-5)]
> "Sun" "Tue" "Wed" "Fri" "Sat"
```

#### Accessing vector elements using 0/1 indexing
```r
y <- t[c(0,0,0,0,0,0,1)]
> "Sun"
```
 
| command | desc |
|----|-------|
| setwd() | |
| rm(list=ls()) | delete vars in workspace |
| paste or paste0() | concatenate string  |
| paste or paste0() | concatenate string  |