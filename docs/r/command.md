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
    <td></td>
  </tr>        
</table>
