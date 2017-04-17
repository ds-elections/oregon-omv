title: "OMV file 1"
author: "RosaKalish"
output: github_document
========================================================

Load Packages

```r
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

```r
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following object is masked from 'package:base':
## 
##     date
```

```r
library(car)      # John Fox program for his regression text, nice recode command
```

```
## Error in library(car): there is no package called 'car'
```

```r
library(rms)      # Frank Harrell regression modeling strategies package
```

```
## Loading required package: Hmisc
```

```
## Loading required package: lattice
```

```
## Loading required package: survival
```

```
## Loading required package: Formula
```

```
## Error: package 'Hmisc' could not be loaded
```

```r
library(Hmisc)    # Frank Harrell miscellaneous commands package
```

```
## Error: package or namespace load failed for 'Hmisc'
```

```r
library(broom)    # Create "tidy" data frames from statistical results
library(popbio)   # Matrix population package, has beautiful logit+histogram plot command
library(tidyverse)
library(data.table)
```

```
## Error in library(data.table): there is no package called 'data.table'
```

Import and Bind 

```r
voterfull <- read_tsv('https://www.dropbox.com/s/khywm89j8myn5t0/or_voter_history.zip?dl=0')
```

```
## Parsed with column specification:
## cols(
##   `<!DOCTYPE html><html lang="en" xmlns:fb="http://ogp.me/ns/fb#" xml:lang="en" class="maestro" xmlns="http://www.w3.org/1999/xhtml">` = col_character()
## )
```

```r
file.choose()
```

```
## Error in file.choose(): file choice cancelled
```

```r
votern1 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD1_VoterHistory_Jan2017.txt")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   HOUSE_NUM = col_integer(),
##   ZIP_CODE = col_integer(),
##   ZIP_PLUS_FOUR = col_integer(),
##   EFF_ZIP_CODE = col_integer()
## )
```

```
## See spec(...) for full column specifications.
```

```
## Warning: 813 parsing failures.
##  row           col   expected   actual
## 1157 HOUSE_NUM     an integer XXXXXXXX
## 1157 ZIP_CODE      an integer XXXXXXXX
## 1157 ZIP_PLUS_FOUR an integer XXXXXXXX
## 1552 HOUSE_NUM     an integer XXXXXXXX
## 1552 ZIP_CODE      an integer XXXXXXXX
## .... ............. .......... ........
## See problems(...) for more details.
```

```r
votern2 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD2_VoterHistory_Jan2017.txt")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   SPLIT = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 47880 parsing failures.
##    row   col               expected actual
## 220875 SPLIT no trailing characters      A
## 221380 SPLIT no trailing characters      A
## 221474 SPLIT no trailing characters      A
## 222477 SPLIT no trailing characters      A
## 222880 SPLIT no trailing characters      A
## ...... ..... ...................... ......
## See problems(...) for more details.
```

```r
votern3 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD3_VoterHistory_Jan2017.txt")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   EFF_ZIP_CODE = col_integer(),
##   EFF_ZIP_PLUS_FOUR = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 150 parsing failures.
##   row               col   expected actual
##  1739 VOTER_ID          an integer    ACP
##  1739 EFF_ZIP_CODE      an integer    ACP
##  1739 EFF_ZIP_PLUS_FOUR an integer    ACP
## 35253 VOTER_ID          an integer    ACP
## 35253 EFF_ZIP_CODE      an integer    ACP
## ..... ................. .......... ......
## See problems(...) for more details.
```

```r
votern4 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD4_VoterHistory_Jan2017.txt")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   HOUSE_NUM = col_integer(),
##   ZIP_CODE = col_integer(),
##   ZIP_PLUS_FOUR = col_integer(),
##   EFF_ZIP_CODE = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 975 parsing failures.
##  row           col   expected   actual
## 1125 HOUSE_NUM     an integer XXXXXXXX
## 1125 ZIP_CODE      an integer XXXXXXXX
## 1125 ZIP_PLUS_FOUR an integer XXXXXXXX
## 5192 HOUSE_NUM     an integer XXXXXXXX
## 5192 ZIP_CODE      an integer XXXXXXXX
## .... ............. .......... ........
## See problems(...) for more details.
```

```r
votern5 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD5_VoterHistory_Jan2017.txt")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer()
## )
## See spec(...) for full column specifications.
```

```r
votern_all <- rbind(votern1, votern2, votern3, votern4, votern5)
---------
voter1 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD1_VoterList_Jan2017.txt")
```

```
## Warning: Missing column names filled in: 'X41' [41]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   HOUSE_NUM = col_integer(),
##   ZIP_CODE = col_integer(),
##   ZIP_PLUS_FOUR = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 590173 parsing failures.
## row col   expected     actual
##   1  -- 41 columns 40 columns
##   2  -- 41 columns 40 columns
##   3  -- 41 columns 40 columns
##   4  -- 41 columns 40 columns
##   5  -- 41 columns 40 columns
## ... ... .......... ..........
## See problems(...) for more details.
```

```
## Error in ---------voter1 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD1_VoterList_Jan2017.txt"): object 'voter1' not found
```

```r
voter2 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD2_VoterList_Jan2017.txt")
```

```
## Warning: Missing column names filled in: 'X41' [41]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   EFF_ZIP_CODE = col_integer(),
##   SPLIT = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 645693 parsing failures.
## row col   expected     actual
##   1  -- 41 columns 40 columns
##   2  -- 41 columns 40 columns
##   3  -- 41 columns 40 columns
##   4  -- 41 columns 40 columns
##   5  -- 41 columns 40 columns
## ... ... .......... ..........
## See problems(...) for more details.
```

```r
voter3 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD3_VoterList_Jan2017.txt")
```

```
## Warning: Missing column names filled in: 'X41' [41]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   EFF_ZIP_CODE = col_integer(),
##   EFF_ZIP_PLUS_FOUR = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 656632 parsing failures.
## row col   expected     actual
##   1  -- 41 columns 40 columns
##   2  -- 41 columns 40 columns
##   3  -- 41 columns 40 columns
##   4  -- 41 columns 40 columns
##   5  -- 41 columns 40 columns
## ... ... .......... ..........
## See problems(...) for more details.
```

```r
voter4 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD4_VoterList_Jan2017.txt")
```

```
## Warning: Missing column names filled in: 'X41' [41]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   HOUSE_NUM = col_integer(),
##   ZIP_CODE = col_integer(),
##   ZIP_PLUS_FOUR = col_integer(),
##   EFF_ZIP_CODE = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 601871 parsing failures.
## row col   expected     actual
##   1  -- 41 columns 40 columns
##   2  -- 41 columns 40 columns
##   3  -- 41 columns 40 columns
##   4  -- 41 columns 40 columns
##   5  -- 41 columns 40 columns
## ... ... .......... ..........
## See problems(...) for more details.
```

```r
voter5 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD5_VoterList_Jan2017.txt")
```

```
## Warning: Missing column names filled in: 'X41' [41]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   VOTER_ID = col_integer(),
##   EFF_ZIP_CODE = col_integer()
## )
## See spec(...) for full column specifications.
```

```
## Warning: 564068 parsing failures.
## row col   expected     actual
##   1  -- 41 columns 40 columns
##   2  -- 41 columns 40 columns
##   3  -- 41 columns 40 columns
##   4  -- 41 columns 40 columns
##   5  -- 41 columns 40 columns
## ... ... .......... ..........
## See problems(...) for more details.
```

```r
voter_all <- rbind(voter1, voter2, voter3, voter4, voter5)
```

```
## Error in rbind(voter1, voter2, voter3, voter4, voter5): object 'voter1' not found
```

```r
head(voter_all) 
```

```
## Error in head(voter_all): object 'voter_all' not found
```

```r
#file.choose()
spatial <- read_csv("/Users/rosa/Downloads/SPATIAL_INFO.csv")
```

```
## Warning: Missing column names filled in: 'X66' [66], 'X67' [67],
## 'X68' [68], 'X69' [69], 'X70' [70], 'X71' [71], 'X72' [72], 'X73' [73],
## 'X74' [74], 'X75' [75], 'X76' [76], 'X77' [77], 'X78' [78], 'X79' [79],
## 'X80' [80], 'X81' [81], 'X82' [82], 'X83' [83], 'X84' [84], 'X85' [85],
## 'X86' [86], 'X87' [87], 'X88' [88], 'X89' [89], 'X90' [90], 'X91' [91],
## 'X92' [92], 'X93' [93], 'X94' [94], 'X95' [95]
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   X66 = col_integer(),
##   X67 = col_integer(),
##   X68 = col_integer(),
##   X69 = col_double(),
##   X70 = col_double(),
##   X71 = col_double(),
##   X72 = col_double(),
##   X73 = col_double(),
##   X74 = col_double(),
##   X75 = col_double(),
##   X76 = col_double(),
##   X77 = col_double(),
##   X78 = col_double(),
##   X79 = col_double(),
##   X80 = col_double(),
##   X81 = col_integer(),
##   X82 = col_integer(),
##   X83 = col_integer(),
##   X84 = col_integer(),
##   X85 = col_integer()
##   # ... with 10 more columns
## )
## See spec(...) for full column specifications.
```
Tidy Vote FIle 

```r
votern_or <- votern_all %>%
  select(VOTER_ID, FIRST_NAME, LAST_NAME, COUNTY, CITY, BIRTH_DATE, STATUS, PARTY_CODE, RES_ADDRESS_1, PRECINCT_NAME, PRECINCT, ZIP_CODE, 11/08/2016)
         
         11/08/2016) 
```

```
## Error: <text>:4:20: unexpected ')'
## 3:          
## 4:          11/08/2016)
##                       ^
```
Import Geographic dta 

```r
#file.choose()
geo <- read_csv("/Users/rosa/Desktop/socialexplorer-zipcode.csv")
voter_geo <- inner_join(voter_or, spatial) 
by COUNTY
```

```
## Error: <text>:4:4: unexpected symbol
## 3: voter_geo <- inner_join(voter_or, spatial) 
## 4: by COUNTY
##       ^
```


```r
voter_or2 <- voter_or %>%
  mutate(COUNTY = tolower(COUNTY))
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```

```r
spatial2 <- spatial %>%
  mutate(COUNTY = tolower(COUNTY))
join <- inner_join(voter_or2, spatial2, by = "COUNTY")
```

```
## Error in inner_join(voter_or2, spatial2, by = "COUNTY"): object 'voter_or2' not found
```


```r
voter_or %>% count(COUNTY)
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```

```r
voter_or %>% count(COUNTY, PARTY_CODE)
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```
What info is in the voter_all and voter_or files, what should I be looking at and how should I tidy? 
