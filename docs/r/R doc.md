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
   v <- "TRUE"  
   v <- 'TRUE'    

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
 
# read csv
``` R
# create a file to read a csv  
file.create("tablulate.R")  

# creates a table of 1 variables and 4 obs  
votes <- read.table("votes.csv")  
View(votes)  

# add separator  
votes <- read.table("votes.csv",sep=",", header=TRUE)  

# read.csv - returns a DataFrame  
votes <- read.csv("votes.csv)"  

# accessed by 
votes[row,column]  
votes[,2]  
votes$poll  
# add a column to the dataframe with the total
votes$total <- votes$poll + votes$mail  
```


# Write csv
``` R
write.csv(votes,"totals.csv", row.names=FALSE)  
colnames(votes)  
rownames(votes)   
```

# Read from url
``` R
url <- "http:\\.....x.csv"
votes <- read.csv(url)
```


# Build tibble of random data 
``` R
library(tibble)

set.seed(123)  # Makes the random data reproducible

n <- 100

dset <- tibble(
  patient_number = sprintf("P%03d", 1:n),
  age = sample(18:85, size = n, replace = TRUE),
  sex = sample(c("Female", "Male"), size = n, replace = TRUE),
  weight_kg = round(rnorm(n, mean = 75, sd = 15), 1),
  height_cm = round(rnorm(n, mean = 170, sd = 10), 1)
)

dset
```

## Filter cols 
``` R
dset |> dplyr::filter(age >= 30)
```


## Update cols 
``` R
dset <- dset |>
  dplyr::mutate(
    weight_kg = pmax(40, pmin(weight_kg, 150)),
    height_cm = pmax(140, pmin(height_cm, 210))
  )
```

## First.Var
``` R
# create a calculated variable
dset <- dset |>
  dplyr::mutate(
    bmi = weight_kg / (height_cm / 100)^2,
    age_group = ifelse(age >= 30, "30+", "Under 30")
  )

#In SAS, first.patient identifies the first observation within each patient group. In R, sort and group the data, then use row_number():
dset <- dset |>
  dplyr::arrange(patient_number, visit_date) |>
  dplyr::group_by(patient_number) |>
  dplyr::mutate(
    first_patient = dplyr::row_number() == 1
  ) |>
  dplyr::ungroup()

# Keep only first record in group
first_records <- dset |>
  dplyr::arrange(patient_number, visit_date) |>
  dplyr::group_by(patient_number) |>
  dplyr::slice_head(n = 1) |>
  dplyr::ungroup()

# Last record
last_records <- dset |>
  dplyr::arrange(patient_number, visit_date) |>
  dplyr::group_by(patient_number) |>
  dplyr::slice_tail(n = 1) |>
  dplyr::ungroup()
```

## Last record in datafram
``` R
dset <- dset |>
  dplyr::mutate(
    end_of_file = dplyr::row_number() == dplyr::n()
  )
```

## Last record for each subject
``` R
dset <- dset |>
  dplyr::group_by(patient_number) |>
  dplyr::mutate(
    last_patient = dplyr::row_number() == dplyr::n()
  ) |>
  dplyr::ungroup()  
```

