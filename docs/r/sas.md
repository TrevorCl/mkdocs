# SAS equivalents

# Reading xpt files
``` R
install.packages("haven")
library(haven)
dset <- haven::read_xpt("./adsl.xpt",
                .name_repair = tolower) 
```


# Proc contents
``` R
library(haven)
library(purrr)
library(dplyr)

lib_path <- "C:/path/to/sas/library"

files <- list.files(lib_path, pattern = "\\.sas7bdat$", full.names = TRUE)

contents <- map_dfr(files, function(f) {
  df <- read_sas(f)
  tibble(
    dataset = tools::file_path_sans_ext(basename(f)),
    variable = names(df),
    label = sapply(df, function(x) attr(x, "label") %||% NA_character_),
    type = sapply(df, class)
  )
})

datasets_with_fl <- contents |>
  filter(grepl("FL$", variable)) |>
  distinct(dataset)

datasets_with_fl
```


# replicate powershell for-each
``` R
fn <- list.files()
paste0("The file is ", fn)
```

For an explicit per-item operation, similar to PowerShell’s ForEach-Object, use purrr::walk():
``` R
library(purrr)
fn |>
  walk(\(file) cat("The file is", file, "\n"))
```

Or use base R:
``` R
for (file in fn) {
  cat("The file is", file, "\n")
}
```  

