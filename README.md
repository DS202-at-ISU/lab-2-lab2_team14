
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

Vinayak:

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

1.  Inspect the first few lines of the data set. What variables are
    there? Of what type are the variables? What does each variable mean?
    What do we expect their data range to be?

``` r
library(classdata)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
df = ames %>% filter(YearBuilt!=0) %>% filter(`LotArea(sf)`!=0) %>% filter(Acres!=0) %>% filter(`TotalLivingArea (sf)`!=0) %>% filter(`Sale Price`!=0) %>% filter(Bedrooms!=0)
ames = df
summary(ames)
```

    ##   Parcel ID           Address                        Style     
    ##  Length:4275        Length:4275        1 Story Frame    :2486  
    ##  Class :character   Class :character   2 Story Frame    : 979  
    ##  Mode  :character   Mode  :character   1 1/2 Story Frame: 460  
    ##                                        Split Level Frame: 140  
    ##                                        Split Foyer Frame: 107  
    ##                                        2 1/2 Story Frame:  57  
    ##                                        (Other)          :  46  
    ##                           Occupancy      Sale Date            Sale Price      
    ##  Condominium                   : 570   Min.   :2017-07-03   Min.   :       1  
    ##  Single-Family / Owner Occupied:3108   1st Qu.:2019-04-16   1st Qu.:  172000  
    ##  Townhouse                     : 428   Median :2020-10-14   Median :  235000  
    ##  Two-Family Conversion         :  76   Mean   :2020-06-28   Mean   : 1612816  
    ##  Two-Family Duplex             :  93   3rd Qu.:2021-11-08   3rd Qu.:  338425  
    ##                                        Max.   :2022-08-31   Max.   :20500000  
    ##                                                                               
    ##   Multi Sale          YearBuilt        Acres        TotalLivingArea (sf)
    ##  Length:4275        Min.   :1880   Min.   :0.0010   Min.   :   3        
    ##  Class :character   1st Qu.:1957   1st Qu.:0.1380   1st Qu.:1108        
    ##  Mode  :character   Median :1986   Median :0.2120   Median :1455        
    ##                     Mean   :1979   Mean   :0.2359   Mean   :1504        
    ##                     3rd Qu.:2004   3rd Qu.:0.2680   3rd Qu.:1756        
    ##                     Max.   :2021   Max.   :4.6500   Max.   :6007        
    ##                                                                         
    ##     Bedrooms      FinishedBsmtArea (sf)  LotArea(sf)          AC           
    ##  Min.   : 1.000   Min.   :  16.0        Min.   :    63   Length:4275       
    ##  1st Qu.: 3.000   1st Qu.: 480.0        1st Qu.:  6002   Class :character  
    ##  Median : 3.000   Median : 725.0        Median :  9240   Mode  :character  
    ##  Mean   : 3.326   Mean   : 766.2        Mean   : 10272                     
    ##  3rd Qu.: 4.000   3rd Qu.:1000.0        3rd Qu.: 11667                     
    ##  Max.   :10.000   Max.   :2537.0        Max.   :202554                     
    ##                   NA's   :1537                                             
    ##   FirePlace                            Neighborhood 
    ##  Length:4275        (27) Res: N Ames         : 507  
    ##  Class :character   (37) Res: College Creek  : 502  
    ##  Mode  :character   (57) Res: Investor Owned : 417  
    ##                     (29) Res: Old Town       : 285  
    ##                     (34) Res: Edwards        : 270  
    ##                     (19) Res: North Ridge Hei: 215  
    ##                     (Other)                  :2079

``` r
head(ames)
```

    ## # A tibble: 6 × 16
    ##   `Parcel ID` Address      Style Occupancy `Sale Date` `Sale Price` `Multi Sale`
    ##   <chr>       <chr>        <fct> <fct>     <date>             <dbl> <chr>       
    ## 1 0903202160  1024 RIDGEW… 1 1/… Single-F… 2022-08-12        181900 <NA>        
    ## 2 0907428215  4503 TWAIN … 1 St… Condomin… 2022-08-04        127100 <NA>        
    ## 3 0923203160  3404 EMERAL… 1 St… Townhouse 2022-08-09        245000 <NA>        
    ## 4 0907275030  4512 HEMING… 2 St… Single-F… 2022-08-16        368000 <NA>        
    ## 5 0907428446  4510 TWAIN … 1 St… Condomin… 2022-08-16        110000 <NA>        
    ## 6 0527301030  3409 EISENH… 1 St… Single-F… 2022-08-08        350000 <NA>        
    ## # ℹ 9 more variables: YearBuilt <dbl>, Acres <dbl>,
    ## #   `TotalLivingArea (sf)` <dbl>, Bedrooms <dbl>,
    ## #   `FinishedBsmtArea (sf)` <dbl>, `LotArea(sf)` <dbl>, AC <chr>,
    ## #   FirePlace <chr>, Neighborhood <fct>

``` r
str(ames)
```

    ## tibble [4,275 × 16] (S3: tbl_df/tbl/data.frame)
    ##  $ Parcel ID            : chr [1:4275] "0903202160" "0907428215" "0923203160" "0907275030" ...
    ##  $ Address              : chr [1:4275] "1024 RIDGEWOOD AVE, AMES" "4503 TWAIN CIR UNIT 105, AMES" "3404 EMERALD DR, AMES" "4512 HEMINGWAY DR, AMES" ...
    ##  $ Style                : Factor w/ 12 levels "1 1/2 Story Brick",..: 2 5 5 9 5 5 5 9 5 5 ...
    ##  $ Occupancy            : Factor w/ 5 levels "Condominium",..: 2 1 3 2 1 2 2 2 5 2 ...
    ##  $ Sale Date            : Date[1:4275], format: "2022-08-12" "2022-08-04" ...
    ##  $ Sale Price           : num [1:4275] 181900 127100 245000 368000 110000 ...
    ##  $ Multi Sale           : chr [1:4275] NA NA NA NA ...
    ##  $ YearBuilt            : num [1:4275] 1940 2006 1997 1996 2006 ...
    ##  $ Acres                : num [1:4275] 0.109 0.027 0.103 0.494 0.023 0.285 0.172 0.297 0.196 0.239 ...
    ##  $ TotalLivingArea (sf) : num [1:4275] 1030 771 1289 2223 658 ...
    ##  $ Bedrooms             : num [1:4275] 2 1 4 4 1 3 4 4 2 3 ...
    ##  $ FinishedBsmtArea (sf): num [1:4275] NA NA 890 NA NA NA 500 593 NA 929 ...
    ##  $ LotArea(sf)          : num [1:4275] 4740 1181 4500 21533 1008 ...
    ##  $ AC                   : chr [1:4275] "Yes" "Yes" "Yes" "Yes" ...
    ##  $ FirePlace            : chr [1:4275] "Yes" "No" "No" "Yes" ...
    ##  $ Neighborhood         : Factor w/ 42 levels "(0) None","(13) Apts: Campus",..: 15 40 18 24 40 13 23 13 14 13 ...

The variables of the data set are: Parcel ID, Address, Style, Occupancy,
Sale Date, Sale Price, Multi Sale, YearBuilt, Acres, TotalLivingArea
(sf), Bedrooms, FinishedBsmtArea (sf), LotArea(sf), AC, FirePlace, and
Neighborhood. That makes 17 variables. Parcel ID is of type chr, and is
a 10 digit number providing a unique ID to each residence. Address is of
type chr, and is a string representing the location of the residence.
Style is of type Factor, and represents the general size of the
residence in stories. Occupancy is of type Factor, and represents the
type of residence, such as Townhouse or Condominium. Sale date is of
type date, represents the date the residence was sold, and go from
2017-07-03 to 2022-08-31. Sale price is of type num, represents the USD
cost of the residence, and ranges from \$1 to \$20,500,000.

2.  Is there a variable of special interest or focus?

For this model, We are focusing on Sale Price.

3.  Start the exploration with the main variable. What is the range of
    the variable? Draw a histogram for a numeric variable or a bar
    chart, if the variable is categorical. What is the general pattern?
    Is there anything odd? Follow up on any oddities in step 4.

4.  Pick a variable that might be related to the main variable. What is
    the range of that variable? Plot/describe the pattern. What is it’s
    relationship to the main variable? Plot a scatterplot, boxplot, or
    faceted barcharts (depending on the types of variables involved).
    Describe overall pattern, does this variable describe any oddities
    discovered in 3? Identify/follow-up on any oddities.
