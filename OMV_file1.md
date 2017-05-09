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
library(tidyverse)
library(stringr)
library(tidyr)
```

Import and Bind Voter Data 

```r
#vote_particip <- read_csv("http://bit.ly/2kG37yJ")
vote_motor <- read_csv("http://bit.ly/2lCadlB")
```

```
## Parsed with column specification:
## cols(
##   VOTER_ID = col_integer(),
##   DESCRIPTION = col_character(),
##   COUNTY = col_character()
## )
```

```r
#These are the files with correct voting turnout data, however they are still missing registration type, which I join from the data used in Home Work 1. 
#file.choose()
voter1 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD1_VoterHistory_Jan2017.txt")
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
voter2 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD2_VoterHistory_Jan2017.txt")
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
voter3 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD3_VoterHistory_Jan2017.txt")
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
voter4 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD4_VoterHistory_Jan2017.txt")
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
voter5 <- read_tsv("/Users/rosa/Desktop/or_voter_history/CD5_VoterHistory_Jan2017.txt")
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
voter_all <- rbind(voter1, voter2, voter3, voter4, voter5)
---------
#These are the voter files I downloaded from Pauls google drive, I am not currently using them. 
  
#voter31 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD1_VoterList_Jan2017.txt")
#voter32 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD2_VoterList_Jan2017.txt")
#voter33 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD3_VoterList_Jan2017.txt")
#voter34 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD4_VoterList_Jan2017.txt")
#voter35 <- read_tsv("/Users/rosa/Documents/OMV project/data /CD5_VoterList_Jan2017.txt")

#voter3_all <- rbind(voter1, voter2, voter3, voter4, voter5)
 

----
# Add Registration Type 
  
voter_all2 <- left_join(x = voter_all,y = vote_motor, by = "VOTER_ID")
```

```
## Error in -------------voter_all2 <- left_join(x = voter_all, y = vote_motor, : object 'voter_all2' not found
```
Tidy Vote File 

```r
voter_or <- voter_all2 %>%
  select(VOTER_ID, FIRST_NAME, LAST_NAME, COUNTY.x, CITY, BIRTH_DATE, STATUS, PARTY_CODE, PRECINCT_NAME, PRECINCT, ZIP_CODE, `11/08/2016`, DESCRIPTION, `11/06/2012`, `11/04/2008`)
```

```
## Error in eval(expr, envir, enclos): object 'voter_all2' not found
```
Import Geographic Data

```r
#I first import Census tract data, then State Legislative district, then County. I finally import Zip Code which I use for this project. However, while the others are from the 2015 community report, the Zip Code data comes from the 2010 election, so there is not perfect demographic information. 
#file.choose()
#census <- read_csv("/Users/rosa/Desktop/SEcensus.csv")

#file.choose()
#stateleg <- read_csv("/Users/rosa/Desktop/SEstateleg.csv")

#file.choose()
#county <- read_csv("/Users/rosa/Desktop/SEcounty.csv")

#file.choose()
zipcode <- read_csv("/Users/rosa/Desktop/zipcode.csv")
```

```
## Parsed with column specification:
## cols(
##   Geo_NAME = col_character(),
##   Geo_QName = col_character(),
##   Geo_AREALAND = col_double(),
##   Geo_AREAWATR = col_integer(),
##   Geo_SUMLEV = col_integer(),
##   Geo_GEOCOMP = col_character(),
##   Geo_FIPS = col_integer(),
##   SE_T003_001 = col_integer(),
##   SE_T003_002 = col_integer(),
##   SE_T003_003 = col_integer(),
##   SE_T054_001 = col_integer(),
##   SE_T054_002 = col_integer(),
##   SE_T054_003 = col_integer(),
##   SE_T054_004 = col_integer(),
##   SE_T054_005 = col_integer(),
##   SE_T054_006 = col_integer(),
##   SE_T054_007 = col_integer(),
##   SE_T054_008 = col_integer()
## )
```
Tidy Geographic Data 

```r
zipcode <- zipcode %>%
  mutate(Geo_NAME = str_replace_all(Geo_NAME, pattern = "ZCTA5 ", replacement = ""))

# Make note of which zips have "(part)" - For later
part_zips <- zipcode %>%
  filter(grepl("part", Geo_NAME))

# Clear those out
zipcode <- zipcode %>%
    mutate(Geo_NAME = substr(Geo_NAME, 1, 5)) %>%
  rename(total_pop = SE_T003_001,
         male = SE_T003_002,
         female = SE_T003_003,
         total_pop2 = SE_T054_001,
         white = SE_T054_002,
         black = SE_T054_003, 
         ai = SE_T054_004,
         asian = SE_T054_005,
         hawaiian = SE_T054_006,
         other = SE_T054_007, 
         two = SE_T054_008,
         ZIP_CODE = Geo_NAME) 

         
# Just Sex
sex <- zipcode %>%
  select(ZIP_CODE, total_pop, male, female)

# Just Race

zipcode$p_black <- zipcode$black / zipcode$total_pop
zipcode$p_white <- zipcode$white / zipcode$total_pop

race <- zipcode %>%
  select(ZIP_CODE, total_pop, white, black, ai, asian, hawaiian, other, two, p_black, p_white)
```

Get at zip code level for Oregon registered voters

```r
total_regs <- voter_or %>%
  group_by(ZIP_CODE) %>%
  summarize(count = n())
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```
Construct Variables for Analysis: 

Proportion of registered that voted on Nov 2016 and Nov 2012 

```r
prop_voted2016 <- voter_or %>%
  group_by(ZIP_CODE) %>%
  summarize(prop_v16 = mean(`11/08/2016` == "YES"))
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```

```r
prop_voted2012 <- voter_or %>%
  group_by(ZIP_CODE) %>%
  summarize(prop_v12 = mean(`11/06/2012` == "YES"))
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```
Proportion that are not Motor Voter Registered 

```r
a <- (is.na(voter_or$DESCRIPTION))
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```

```r
voter_or$DESCRIPTION[a] <- "conventional"
```

```
## Error in voter_or$DESCRIPTION[a] <- "conventional": object 'voter_or' not found
```

```r
voter_or$DESCRIPTION <- as.factor(voter_or$DESCRIPTION)
```

```
## Error in is.factor(x): object 'voter_or' not found
```

```r
table(voter_or$DESCRIPTION)
```

```
## Error in table(voter_or$DESCRIPTION): object 'voter_or' not found
```

```r
prop_regcon <- voter_or %>%
  group_by(ZIP_CODE) %>%
  summarize(prop_reg = mean(DESCRIPTION == "conventional"))
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```

```r
prop_regOMV <- voter_or %>%
  group_by(ZIP_CODE) %>%
  summarize(prop_OMV = mean(DESCRIPTION != "conventional"))
```

```
## Error in eval(expr, envir, enclos): object 'voter_or' not found
```

Construct data sets for analysis with Voter info by Zip Code including, number of registered voters, how they registered, and the proportion that voted.

```r
zipcode_data <- inner_join(x = total_regs,
                           y = prop_voted2016,
                           by = "ZIP_CODE")
```

```
## Error in inner_join(x = total_regs, y = prop_voted2016, by = "ZIP_CODE"): object 'total_regs' not found
```

```r
zipcode_data <- inner_join(x = zipcode_data,
                           y = prop_voted2012,
                           by = "ZIP_CODE")
```

```
## Error in inner_join(x = zipcode_data, y = prop_voted2012, by = "ZIP_CODE"): object 'zipcode_data' not found
```

```r
zipcode_data <- inner_join(x = zipcode_data,
                           y = prop_regOMV,
                           by = "ZIP_CODE")
```

```
## Error in inner_join(x = zipcode_data, y = prop_regOMV, by = "ZIP_CODE"): object 'zipcode_data' not found
```

```r
# Join sex with voter reg aggregated data
sex_reg <- inner_join(x = sex, y = zipcode_data, 
                      by = "ZIP_CODE")
```

```
## Error in is.data.frame(y): object 'zipcode_data' not found
```

```r
# Join race with voter reg aggregated data
race_reg <- inner_join(x = race, y = zipcode_data, 
                      by = "ZIP_CODE")
```

```
## Error in is.data.frame(y): object 'zipcode_data' not found
```

```r
# One set with both 

zip_reg <- inner_join(x = race_reg, y = sex, 
                      by = "ZIP_CODE")
```

```
## Error in inner_join(x = race_reg, y = sex, by = "ZIP_CODE"): object 'race_reg' not found
```

```r
# Add Turnout difference 
require(dplyr)
require(tidyr)

zip_reg <- zip_reg %>%
mutate (vote_diff = prop_v16 / prop_v12)
```

```
## Error in eval(expr, envir, enclos): object 'zip_reg' not found
```
Filter Outliers and Zips under 50 people 

```r
zip_reg <- filter(zip_reg, total_pop.x > 50)
```

```
## Error in filter_(.data, .dots = lazyeval::lazy_dots(...)): object 'zip_reg' not found
```

```r
zip_reg <- filter(zip_reg, p_white > .25)
```

```
## Error in filter_(.data, .dots = lazyeval::lazy_dots(...)): object 'zip_reg' not found
```

Modeling: 

Model 1 and 2. Race and Registration

```r
# Model 1 and 2: Race and Registration Type 

# Model 1, Blackness 
 ggplot(zip_reg, aes(x = p_black, y = prop_OMV)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "mediumpurple2") +
    ggtitle("Registration Type by Zip Code Blackness") +
  labs(x="Percent Black of Zip Code",y="Proportion of Voters Registered Traditionally")
```

```
## Error in ggplot(zip_reg, aes(x = p_black, y = prop_OMV)): object 'zip_reg' not found
```

```r
m1 <- lm(p_black ~ prop_reg, data = zip_reg2)
```

```
## Error in is.data.frame(data): object 'zip_reg2' not found
```

```r
summary(m1)
```

```
## Error in summary(m1): object 'm1' not found
```

```r
# Log Transformation 
ggplot(zip_reg, aes(x = log(p_black +.005), y = prop_OMV)) +
geom_point(color= "mediumpurple2")+
  geom_smooth(method=`lm`, color= "hotpink") +
    ggtitle("Registration Type by Zip Code Blackness") +
  labs(x="Log Percet Black of Zip Code",y="Proportion of Voters Registered by OMV")
```

```
## Error in ggplot(zip_reg, aes(x = log(p_black + 0.005), y = prop_OMV)): object 'zip_reg' not found
```

```r
#log both 
ggplot(zip_reg, aes(x = log(p_black), y = log(prop_OMV))) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "mediumpurple2") +
    ggtitle("Registration Type by Zip Code Blackness") +
  labs(x="Log Percet Black of Zip Code",y="Log Proportion of Voters Registered Traditionally")
```

```
## Error in ggplot(zip_reg, aes(x = log(p_black), y = log(prop_OMV))): object 'zip_reg' not found
```

```r
#Alternative transformation

ggplot(zip_reg, aes(x = p_black +I(p_black^2), y = prop_OMV)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "mediumpurple2") +
    ggtitle("Registration Type by Zip Code Blackness") +
  labs(x="Log Percet Black of Zip Code",y="Proportion of Voters Registered Traditionally")
```

```
## Error in ggplot(zip_reg, aes(x = p_black + I(p_black^2), y = prop_OMV)): object 'zip_reg' not found
```

```r
# Linear Model 

m1b <- lm(log(p_black +.005) ~ prop_OMV, data = zip_reg)
```

```
## Error in is.data.frame(data): object 'zip_reg' not found
```

```r
summary(m1b)
```

```
## Error in summary(m1b): object 'm1b' not found
```

```r
# -3.22 with p value of .004 

# Model 2  Whiteness 

 ggplot(zip_reg, aes(x = p_white, y = prop_OMV)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "mediumpurple2") +
    ggtitle("Registration Type by Zip Code Whiteness") +
  labs(x="Percet White of Zip Code",y="Proportion of Voters Registered Traditionally")
```

```
## Error in ggplot(zip_reg, aes(x = p_white, y = prop_OMV)): object 'zip_reg' not found
```

```r
#transformation
ggplot(zip_reg, aes(x = log(p_white), y = prop_OMV)) +
geom_point(color= "mediumpurple2")+
  geom_smooth(method=`lm`, color= "hotpink") +
    ggtitle("Registration Type by Zip Code Whiteness") +
  labs(x="Log Percent White of Zip Code",y="Proportion of Voters Registered by OMV")
```

```
## Error in ggplot(zip_reg, aes(x = log(p_white), y = prop_OMV)): object 'zip_reg' not found
```

```r
#alternative transformaiton 
ggplot(zip_reg2, aes(x = p_white + I(p_white^2), y = prop_OMV +I(prop_reg^2))) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "mediumpurple2") +
    ggtitle("Registration Type by Zip Code Whiteness") +
  labs(x="Percet White of Zip Code",y="Proportion of Voters Registered Traditionally")
```

```
## Error in ggplot(zip_reg2, aes(x = p_white + I(p_white^2), y = prop_OMV + : object 'zip_reg2' not found
```

```r
ggplot(zip_reg2, aes(x = p_white, y = log(prop_reg))) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "mediumpurple2") +
    ggtitle("Registration Type by Zip Code Whiteness") +
  labs(x="Percet White of Zip Code",y="Log Proportion of Voters Registered Traditionally")
```

```
## Error in ggplot(zip_reg2, aes(x = p_white, y = log(prop_reg))): object 'zip_reg2' not found
```

```r
m2 <- lm(log(p_white) ~ prop_OMV, data = zip_reg)
```

```
## Error in is.data.frame(data): object 'zip_reg' not found
```

```r
summary(m2)
```

```
## Error in summary(m2): object 'm2' not found
```

```r
# -1.28 with P Value of  0.00 
```
Models Continued 

```r
# Model 3: Registration type and Voter turnout 
 ggplot(zip_reg, aes(x = prop_OMV, y = vote_diff)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "palegreen") +
    ggtitle("Voting Increase and Registration Type across Zip Code") +
  labs(x="Proportion of Voters Registered by OMV",y="Increase in Turnout for 2016 Election")+
   ylim(0, 3)
```

```
## Error in ggplot(zip_reg, aes(x = prop_OMV, y = vote_diff)): object 'zip_reg' not found
```

```r
#m3 <-lm vote_diff ~ prop_OMV, data = zip_reg)
#summary(m3)


# Model 4: Population and Registration Type 
 ggplot(zip_reg, aes(x = total_pop.x, y = prop_OMV)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "orange") +
    ggtitle("AVR Prevalance across ZipCode Populaiton") +
  labs(x="ZipCode Population ",y="Proportion of Voters Registered Automatically")
```

```
## Error in ggplot(zip_reg, aes(x = total_pop.x, y = prop_OMV)): object 'zip_reg' not found
```

```r
m4 <-lm(total_pop.x ~ prop_OMV, data = zip_reg)
```

```
## Error in is.data.frame(data): object 'zip_reg' not found
```

```r
summary(m4)
```

```
## Error in summary(m4): object 'm4' not found
```

```r
# -52383 P value = .017 

# Model 5: population and turnout rate
ggplot(zip_reg, aes(x = total_pop.x, y = vote_diff)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "yellowgreen") +
    ggtitle("Turnout Rates by ZipCode Populaiton") +
  labs(x="ZipCode Population ",y="Change in Turnout Rates from 2012 and 2016 Presidential Election")+
   ylim(0, 2)
```

```
## Error in ggplot(zip_reg, aes(x = total_pop.x, y = vote_diff)): object 'zip_reg' not found
```

```r
#m5 <-lm(total_pop.x ~ vote_diff, data = zip_reg)
#summary(m5)

# Model 6 and 7: turnout by race 
ggplot(zip_reg, aes(x = log(p_white), y = vote_diff)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "skyblue1") +
    ggtitle("Turnout Rates by Zip code Whitness") +
  labs(x=" Log of Zip Code Whiteness ",y="Change in Turnout Rates from 2012 and 2016 Presidential Election")+
   ylim(0, 2)
```

```
## Error in ggplot(zip_reg, aes(x = log(p_white), y = vote_diff)): object 'zip_reg' not found
```

```r
ggplot(zip_reg, aes(x = log(p_black + .005), y = vote_diff)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "skyblue1") +
    ggtitle("Turnout Rates by Zip code Blackness") +
  labs(x="Log of Zip Code Blackness ",y="Change in Turnout Rates from 2012 and 2016 Presidential Election")+
   ylim(0, 2)
```

```
## Error in ggplot(zip_reg, aes(x = log(p_black + 0.005), y = vote_diff)): object 'zip_reg' not found
```

```r
m6 <- lm(vote_diff ~ p_white, data = zip_reg)
```

```
## Error in is.data.frame(data): object 'zip_reg' not found
```

```r
summary(m6)
```

```
## Error in summary(m6): object 'm6' not found
```

```r
m7 <- lm(vote_diff ~ p_black, data = zip_reg)
```

```
## Error in is.data.frame(data): object 'zip_reg' not found
```

```r
summary(m7)
```

```
## Error in summary(m7): object 'm7' not found
```
More Plots 

```r
ggplot(zip_reg, aes(x = ZIP_CODE, y = p_white)) +
geom_point(color= "hotpink") +
    ggtitle("Whitness of Oregon Zip Codes") +
  labs(x="Zip Code",y="Percent White")
```

```
## Error in ggplot(zip_reg, aes(x = ZIP_CODE, y = p_white)): object 'zip_reg' not found
```

```r
 ggplot(zip_reg, aes(x = total_pop.x, y = prop_OMV)) +
geom_point(color= "hotpink")+
  geom_smooth(method=`lm`, color= "palegreen") +
    ggtitle("Registration Type across Zip Code Population") +
  labs(x="Zip Code Population",y="Proportion of Voters Registered by OMV")
```

```
## Error in ggplot(zip_reg, aes(x = total_pop.x, y = prop_OMV)): object 'zip_reg' not found
```

Extra Code 

```r
#race_reg2<- race_reg %>% 
  #gather(key="race", value = "number", 3:9)

#sex_reg2 <- sex_reg %>% 
 # gather(key="sex", value = "number", 3:4)

#both_regtidy <-inner_join(x = race_reg2, y = sex_reg2, 
                    #  by = "ZIP_CODE") 

#Dont need this any more, also does not work. 
#votor_or2 <- votor_or %>%
#  mutate(DESCRIPTION = stringr::str_replace_all(DESCRIPTION, NA, "Not Registered")
         
#MV <- voter_or2 %>%
  #group_by(ZIP_CODE) %>%
  #summarize(prop_MV = mean(DESCRIPTION != "conventional"))
  
  
      # prop_motorvoter <- voter_or %>%
 # group_by(ZIP_CODE) %>%
 # summarize(prop_NotMV = mean(`DESCRIPTION` == "Not Registered"))
```

