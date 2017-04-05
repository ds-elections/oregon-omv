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
```

Import and Bind 

```r
#file.choose()
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
```

```
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
head(voter_all) 
```

```
## # A tibble: 6 × 41
##    VOTER_ID FIRST_NAME MIDDLE_NAME LAST_NAME NAME_SUFFIX BIRTH_DATE
##       <int>      <chr>       <chr>     <chr>       <chr>      <chr>
## 1 100743763   CAROLINE      AMANDA    ABBOTT        <NA> 07-15-1966
## 2 100743762       JOHN        ERIC    ABBOTT        <NA> 02-17-1965
## 3 100783979   NICHOLAS    ALASDAIR    ABBOTT        <NA> 04-19-1997
## 4 100505034   ADRIANNA   CHRISTINA      ABEL        <NA> 10-04-1991
## 5  11905738      WENDY        <NA>   ABRAHAM        <NA> 01-21-1974
## 6  16765525    DEBORAH           J    ABRAMS        <NA> 08-18-1948
## # ... with 35 more variables: CONFIDENTIAL <chr>, EFF_REGN_DATE <chr>,
## #   STATUS <chr>, PARTY_CODE <chr>, PHONE_NUM <chr>, UNLISTED <chr>,
## #   COUNTY <chr>, RES_ADDRESS_1 <chr>, RES_ADDRESS_2 <chr>,
## #   HOUSE_NUM <chr>, HOUSE_SUFFIX <chr>, PRE_DIRECTION <chr>,
## #   STREET_NAME <chr>, STREET_TYPE <chr>, POST_DIRECTION <chr>,
## #   UNIT_TYPE <chr>, UNIT_NUM <chr>, ADDR_NON_STD <chr>, CITY <chr>,
## #   STATE <chr>, ZIP_CODE <chr>, ZIP_PLUS_FOUR <chr>, EFF_ADDRESS_1 <chr>,
## #   EFF_ADDRESS_2 <chr>, EFF_ADDRESS_3 <chr>, EFF_ADDRESS_4 <chr>,
## #   EFF_CITY <chr>, EFF_STATE <chr>, EFF_ZIP_CODE <chr>,
## #   EFF_ZIP_PLUS_FOUR <chr>, ABSENTEE_TYPE <chr>, PRECINCT_NAME <chr>,
## #   PRECINCT <chr>, SPLIT <chr>, X41 <chr>
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
voter_or <- voter_all %>%
  select(VOTER_ID, FIRST_NAME, LAST_NAME, COUNTY, CITY, BIRTH_DATE, STATUS, PARTY_CODE, RES_ADDRESS_1, PRECINCT_NAME, PRECINCT, ZIP_CODE) 
```

OK so how do I know who was registered through OMV? 
How should I tidy the spatial file 
