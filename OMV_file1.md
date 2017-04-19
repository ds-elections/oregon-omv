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

Import and Bind Voter Data 

```r
#This link attempts to make the data importable to anyone, however I can not get it to work 

voterfull <- read_tsv('https://www.dropbox.com/s/khywm89j8myn5t0/or_voter_history.zip?dl=0')
```

```
## Parsed with column specification:
## cols(
##   `<!DOCTYPE html><html lang="en" xmlns:fb="http://ogp.me/ns/fb#" xml:lang="en" class="maestro" xmlns="http://www.w3.org/1999/xhtml">` = col_character()
## )
```

```r
#These are the files with correct voting turnout data, however they are still missing registration type, I am not sure where to find that 

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
#These are the voter files I downloaded from Pauls google drive, tho they do not seem to have all the information that I need. 
  
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
Tidy Vote File 

```r
#Here I select the columns I need. I would like to select the "11/08/2016" file but it will not let me, I think becuase the title is numeric. 
votern_or <- votern_all %>%
  select(VOTER_ID, FIRST_NAME, LAST_NAME, COUNTY, CITY, BIRTH_DATE, STATUS, PARTY_CODE, RES_ADDRESS_1, PRECINCT_NAME, PRECINCT, ZIP_CODE)

# Exluding 11/08/2016 
```
Import Geographic Data

```r
#I first import Census tract data, then State Legislative district, then County. 
#file.choose()
census <- read_csv("/Users/rosa/Desktop/SEcensus.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   Geo_FIPS = col_double(),
##   Geo_SUMLEV = col_integer(),
##   Geo_STATE = col_integer(),
##   SE_T004_001 = col_integer(),
##   SE_T004_002 = col_integer(),
##   SE_T004_003 = col_integer(),
##   SE_T007_001 = col_integer(),
##   SE_T007_002 = col_integer(),
##   SE_T007_003 = col_integer(),
##   SE_T007_004 = col_integer(),
##   SE_T007_005 = col_integer(),
##   SE_T007_006 = col_integer(),
##   SE_T007_007 = col_integer(),
##   SE_T007_008 = col_integer(),
##   SE_T007_009 = col_integer(),
##   SE_T007_010 = col_integer(),
##   SE_T007_011 = col_integer(),
##   SE_T007_012 = col_integer(),
##   SE_T007_013 = col_integer(),
##   SE_T013_001 = col_integer()
##   # ... with 8 more columns
## )
```

```
## See spec(...) for full column specifications.
```

```r
#file.choose()
stateleg <- read_csv("/Users/rosa/Desktop/SEstateleg.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   Geo_FIPS = col_integer(),
##   Geo_SUMLEV = col_integer(),
##   Geo_STATE = col_integer(),
##   SE_T004_001 = col_integer(),
##   SE_T004_002 = col_integer(),
##   SE_T004_003 = col_integer(),
##   SE_T007_001 = col_integer(),
##   SE_T007_002 = col_integer(),
##   SE_T007_003 = col_integer(),
##   SE_T007_004 = col_integer(),
##   SE_T007_005 = col_integer(),
##   SE_T007_006 = col_integer(),
##   SE_T007_007 = col_integer(),
##   SE_T007_008 = col_integer(),
##   SE_T007_009 = col_integer(),
##   SE_T007_010 = col_integer(),
##   SE_T007_011 = col_integer(),
##   SE_T007_012 = col_integer(),
##   SE_T007_013 = col_integer(),
##   SE_T013_001 = col_integer()
##   # ... with 8 more columns
## )
## See spec(...) for full column specifications.
```

```r
#file.choose()
county <- read_csv("/Users/rosa/Desktop/SEcounty.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   Geo_FIPS = col_integer(),
##   Geo_SUMLEV = col_integer(),
##   Geo_GEOCOMP = col_integer(),
##   Geo_LOGRECNO = col_integer(),
##   Geo_STATE = col_integer(),
##   Geo_COUNTY = col_integer(),
##   TotalPopSex = col_integer(),
##   PopMale = col_integer(),
##   PopFemale = col_integer(),
##   TotalPopAge = col_integer(),
##   PopFive = col_integer(),
##   PopNine = col_integer(),
##   PopFourteen = col_integer(),
##   PopSeventeen = col_integer(),
##   PopTwentyfour = col_integer(),
##   PopThirtyfour = col_integer(),
##   PopFortyfour = col_integer(),
##   PopFiftyfour = col_integer(),
##   PopSixtyfour = col_integer(),
##   PopSeventyfour = col_integer()
##   # ... with 11 more columns
## )
## See spec(...) for full column specifications.
```
Tidy Geographic Data 

```r
#Here I would like to seperate the columns into ones with County and tract in seperate columns, but I am not sure how to do that. 

#censust <- census %>%
  #select(Geo_NAME, Geo_COUNTY)
```

 County Join 

```r
votern_all2 <- votern_all %>%
  mutate(COUNTY = tolower(COUNTY))
county2 <- county %>%
  mutate(COUNTY = tolower(COUNTY))
join <- inner_join(votern_all2, county2, by = "COUNTY")

#voter_or %>% count(COUNTY)
#voter_or %>% count(COUNTY, PARTY_CODE)
```
Visualize 

```r
#ggplot(join, aes(x= PopWhite))+
#facet_grid(.~COUNTY)
```

