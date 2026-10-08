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

## Length
```r
v <- 5:12   
length(v)
```
## Sort
```r
v <- 5:12   
sort(v)
```
## Access
```r
v <- 5:12
# 1 to length
v[1]
v[c(1,2)]
v[c(-1)]
```

## Change
```r
v <- 5:12
# 1 to length
v[1] <- 33
```
## Multiple element vectors
```r
v <- 5:12   
v <- 3.4:10.4 
#if the last value is not in the sequence then it is left

letters
# [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q" "r" "s" "t" "u" "v" "w" "x" "y" "z"
letters[1:5]
# [1] "a" "b" "c" "d" "e"
LETTERS
# [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S" "T" "U" "V" "W" "X" "Y" "Z"
1:5
# [1] 1 2 3 4 5
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


# List
```r
thislist <- list("apple", "banana", "cherry")
v <- c(a = 1, b = 2, c = 3)
l <- list(a = 1, b = "x", c = 1:3)
```
| Operation |	Vector  v |	List l |
|--|--|--|
|[1]| c(a = 1), still a vector|list(a = 1), still a list|
|[[1]]|1|1, the element itself|
|$a|error on atomic vectors|1|
|["a"]|c(a = 1)|list(a = 1)|
|[["c"]]|3|1:3|
|Mixed types|c(1, "x") becomes c("1", "x")|kept as they are|
|Arithmetic|v * 2 works|l * 2 gives an error|
|Apply a function|sqrt(v)|lapply(l, length)|

The difference that matters most:
[ keeps the container, so on a list you get back a smaller list.
[[ and $ pull out a single element.

## exists
``` R
"apple" %in% thislist
```
## add, remove
``` R
append(thislist,"orange", after =2)
newlist <- thislist[-1] # removes first 
newlist <- thislist[-(2:5)] # removes -2,-3,-4,-5
```
## extracting a range from the list 
``` R
thislist[2:5]
```
## looping 
``` R
for (x in thislist) {
  print (x)
}
```
## Joining
``` R
newlist <-c(list1,list2,list3)
```



# Matrix
```r
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

thismatrix[c(1,2),]

# add columns
newmatrix <- cbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# add rows
newmatrix <- rbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# remove
thismatrix <- thismatrix[-c(1), -c(1)]

# exists
"apple" %in% thismatrix

# n rows and cols
dim(thismatrix)

# length
length(thismatrix)

# iterate
for (rows in 1:nrow(thismatrix)) {
  for (columns in 1:ncol(thismatrix)) {
    print(thismatrix[rows, columns])
  }
}

# combine
# Combine matrices
Matrix1 <- matrix(c("apple", "banana", "cherry", "grape"), nrow = 2, ncol = 2)
Matrix2 <- matrix(c("orange", "mango", "pineapple", "watermelon"), nrow = 2, ncol = 2)

# Adding it as a rows
Matrix_Combined <- rbind(Matrix1, Matrix2)
Matrix_Combined

# Adding it as a columns
Matrix_Combined <- cbind(Matrix1, Matrix2)
Matrix_Combined
```

# Array
```r
# one dimensional
arr <- c(1:24)
# multi dimensional
arr <= array(1:24, dim-c(4,3,2)) # rows, cols, n dimensions

thisarray <- c(1:24)

# Access all the items from the first row from matrix one
multiarray <- array(thisarray, dim = c(4, 3, 2))
multiarray[c(1),,1]

# Access all the items from the first column from matrix one
multiarray <- array(thisarray, dim = c(4, 3, 2))
multiarray[,c(1),1]
```

# Factors
```r
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

levels(music_genre)

music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"), levels = c("Classic", "Jazz", "Pop", "Rock", "Opera"))

levels(music_genre)

# Only assign to what is in the levels
music_genre[3] <- "Opera"

music_genre[3]
```


# Data Frame
```r
 L3 <- LETTERS[1:3]
 fac <- sample(L3, 10, replace = TRUE)
 d <- data.frame(x = 1, y = 1:10, fac = fac)

# add col iterating between x and y
 d2 <- cbind(d,default=c('x','y'))

# add col x 
 d2 <- cbind(d,reason='x') 
```


# stats
```r
Data_Cars <- mtcars

max(Data_Cars$hp)
min(Data_Cars$hp)

rownames(Data_Cars)[which.max(Data_Cars$hp)]
rownames(Data_Cars)[which.min(Data_Cars$hp)]

Data_Cars[which.max(Data_Cars$hp), ]
Data_Cars[which.min(Data_Cars$hp),]

mean(Data_Cars$wt)

manu <- word(rownames(mtcars), 1)
sort(-table(manu))

# c() specifies which percentile you want
quantile(Data_Cars$wt, c(0.75))

quantile(Data_Cars$wt)
```


# Read csv
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

# Data frame
```r
Data_Frame3 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame4 <- data.frame (
  Steps = c(3000, 6000, 2000),
  Calories = c(300, 400, 300)
)

New_Data_Frame1 <- cbind(Data_Frame3, Data_Frame4)
New_Data_Frame1
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

For better quality, make the values within a range
``` R
dset <- dset |>
  dplyr::mutate(
    weight_kg = pmax(40, pmin(weight_kg, 150)),
    height_cm = pmax(140, pmin(height_cm, 210))
  )
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

# Files
How could i get the file name and creation and last modified date?
Use file.info(). It returns metadata for every path supplied:
``` R
fn <- list.files(full.names = TRUE)
file_details <- file.info(fn)[, c("ctime", "mtime")]
file_details
```
Using a tibble
``` R
library(tibble)

file_details <- tibble(
  file = list.files(full.names = TRUE)
) |>
  dplyr::mutate(
    created = file.info(file)$ctime,
    modified = file.info(file)$mtime
  )

file_details
```





```
