# R Commands


| command | desc | examples |
|----|-------|------|
| setwd() | | |
| rm(list=ls()) | delete vars in workspace | |
| paste or paste0() | concatenate string  | |
| paste or paste0() | concatenate string  | |
| str | Compactly display the internal structure of an R object Ideally, only one line for each ‘basic’ structure is displayed. It is especially well suited to compactly display the (abbreviated) contents of (possibly nested) lists|   str(dm) <br/> tibble [100 x 5] (S3: tbl_df/tbl/data.frame) <br/>  $ USUBJID  : chr [1:100] "PT1.000000e+00d" "PT2.000000e+00d" "PT3.000000e+00d" "PT4.000000e+00d" ... <br/> $ age      : int [1:100] 48 68 31 84 59 67 60 31 42 74 ...<br/> $ sex      : chr [1:100] "Male" "Male" "Female" "Female" ...<br/> $ weight_kg: num [1:100] 74.7 73.7 51.1 87.8 64.3 91 67 83 47.6 47.8 ...<br/><br/>$ height_cm: num [1:100] 166 156 167 160 177 ... |
| word | | library(stringr) \n dset <- mtcars \n dim(dset) \n rname=rownames(dset) \n rname \m manu <- unique(word(rownames(mtcars), 1))  |
| gsub | | |
| str_c | |  |

<table>
   <tr>
    <td>t</td>
    <td>Transpose
       
```r
ex1 <- c(pt = 1,site = 2, position = 3, test=4)
#  pt     site position     test 
#   1        2        3        4 
ex2 <- t(ex1)
#      pt site position test
# [1,]  1    2        3    4
```

    
</td>
  </tr>        
  <tr>
    <td>word</td>
    <td>
       
```r
library(stringr) 
dset <- mtcars 
dim(dset) 
rname=rownames(dset) 
manu <- unique(word(rownames(mtcars), 1))
```

      
</td>
  </tr>
  <tr>
    <td>cut</td>
    <td>

```r
incomes <- sample(35:100, 20, replace = TRUE)
factor(cut(incomes, breaks = 35+10*(0:7))) -> incomef
#[1] (85,95]  (75,85]  (65,75]  (35,45]  (75,85]  (35,45]  (95,105] (85,95]  (85,95]  (35,45]  (35,45]  (85,95]  (35,45] 
[14] (75,85]  (75,85]  (45,55]  (35,45]  (35,45]  (45,55]  (65,75] 
Levels: (35,45] (45,55] (65,75] (75,85] (85,95] (95,105]
 # As data frame with income and cut
df <- data.frame(income = incomes, incomef = incomef)
df                      # prints every row  
#    income  incomef
# 1      86  (85,95]
# 2      80  (75,85]
# 3      67  (65,75]
# 4      37  (35,45]

# Cut into 3 groups
  l1 <- sample(1:99,50)
  l2 <- cut(l1,3)
#  [1] (34.3,66.7] (66.7,99.1] (34.3,66.7] (34.3,66.7] (66.7,99.1] (66.7,99.1] (34.3,66.7] (34.3,66.7] (34.3,66.7]
[10] (34.3,66.7] (1.9,34.3]  (34.3,66.7] (1.9,34.3]  (1.9,34.3]  (66.7,99.1] (66.7,99.1] (1.9,34.3]  (34.3,66.7]
[19] (34.3,66.7] (66.7,99.1] (66.7,99.1] (1.9,34.3]  (66.7,99.1] (34.3,66.7] (66.7,99.1] (66.7,99.1] (1.9,34.3] 
[28] (1.9,34.3]  (34.3,66.7] (66.7,99.1] (1.9,34.3]  (66.7,99.1] (66.7,99.1] (1.9,34.3]  (66.7,99.1] (66.7,99.1]
[37] (1.9,34.3]  (1.9,34.3]  (1.9,34.3]  (34.3,66.7] (66.7,99.1] (34.3,66.7] (66.7,99.1] (1.9,34.3]  (66.7,99.1]
[46] (1.9,34.3]  (66.7,99.1] (1.9,34.3]  (66.7,99.1] (1.9,34.3] 
Levels: (1.9,34.3] (34.3,66.7] (66.7,99.1]
  class(l2)
# [1] "factor"
  attributes(l2)
# $levels
# [1] "(1.9,34.3]"  "(34.3,66.7]" "(66.7,99.1]"
# $class
# [1] "factor"
  table(l2)
# (1.9,34.3] (34.3,66.7] (66.7,99.1] 
#         16          14          20

# FIND values of l1 that grouped into l2
split(l1, l2) 
# $`(1.9,34.3]`
# [1] 22 17  3  6  2 19 26 31  7  9 13 25 21 33 30 15
# $`(34.3,66.7]`
# [1] 53 52 43 48 62 45 49 60 46 56 54 57 41 51
# $`(66.7,99.1]`
# [1] 89 68 96 71 77 79 81 67 92 70 88 85 94 82 80 95 78 90 99 72
```
       
</td>
  </tr>        
</table>
