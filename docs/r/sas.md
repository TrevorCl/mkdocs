

# Reading xpt files
install.packages("haven")
library(haven)
dset <- haven::read_xpt("./adsl.xpt",
                .name_repair = tolower) 
