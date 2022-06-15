---
title: "Bike-Share Navigate Speedy Success"
author: "THANSEER"
date: '2022-06-15'
output: html_document
---

## Case study: How Does a Bike-Share Navigate Speedy Success?

## Introduction

You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights,
your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives
must approve your recommendations, so they must be backed up with compelling data insights and professional data
visualizations.


## Ask

Three questions will guide the future marketing program:

* How do annual members and casual riders use Cyclistic bikes differently?
* Why would casual riders buy Cyclistic annual memberships?
* How can Cyclistic use digital media to influence casual riders to become members?

## Prepare

* Verify data’s integrity
* Check data credibility and reliability
* Check data types
* Merge datasets

## Process

* Clean, Remove and Transform data
* Document cleaning processes and results

## Analyze

* Identify patterns
* Draw conclusions
* Make predictions

## Share

* Create effective visuals
* Create a story for data
* Share insights to stakeholders

## Act

* Give recommendations based on insights
* Solve problems
* Create something new



## install libraries


```r
install.packages("tidyverse")
```

```
## Installing package into 'C:/Users/Thanseer L/AppData/Local/R/win-library/4.2'
## (as 'lib' is unspecified)
```

```
## package 'tidyverse' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\Thanseer L\AppData\Local\Temp\RtmpkdqNCR\downloaded_packages
```

```r
install.packages("janitor")
```

```
## Installing package into 'C:/Users/Thanseer L/AppData/Local/R/win-library/4.2'
## (as 'lib' is unspecified)
```

```
## package 'janitor' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\Thanseer L\AppData\Local\Temp\RtmpkdqNCR\downloaded_packages
```

```r
install.packages("scales")
```

```
## Installing package into 'C:/Users/Thanseer L/AppData/Local/R/win-library/4.2'
## (as 'lib' is unspecified)
```

```
## package 'scales' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\Thanseer L\AppData\Local\Temp\RtmpkdqNCR\downloaded_packages
```
Load libraries

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
## ✔ tibble  3.1.7     ✔ dplyr   1.0.9
## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
## ✔ readr   2.1.2     ✔ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(ggplot2)
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(dplyr)
library(readr)
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(data.table)
```

```
## data.table 1.14.2 using 4 threads (see ?getDTthreads).  Latest news: r-datatable.com
```

```
## 
## Attaching package: 'data.table'
```

```
## The following objects are masked from 'package:lubridate':
## 
##     hour, isoweek, mday, minute, month, quarter, second, wday, week,
##     yday, year
```

```
## The following objects are masked from 'package:dplyr':
## 
##     between, first, last
```

```
## The following object is masked from 'package:purrr':
## 
##     transpose
```

```r
library(tidyr)
```



Load datasets


```r
tripdata_202004 <- read.csv("all/202004-divvy-tripdata.csv")
tripdata_202005 <- read.csv("all/202005-divvy-tripdata.csv")
tripdata_202006 <- read.csv("all/202006-divvy-tripdata.csv")
tripdata_202007 <- read.csv("all/202007-divvy-tripdata.csv")
tripdata_202008 <- read.csv("all/202008-divvy-tripdata.csv")
tripdata_202009 <- read.csv("all/202009-divvy-tripdata.csv")
tripdata_202010 <- read.csv("all/202010-divvy-tripdata.csv") 
tripdata_202011 <- read.csv("all/202011-divvy-tripdata.csv")
tripdata_202012 <- read.csv("all/202012-divvy-tripdata.csv")
tripdata_202101 <- read.csv("all/202101-divvy-tripdata.csv")
tripdata_202102 <- read.csv("all/202102-divvy-tripdata.csv")
tripdata_202103 <- read.csv("all/202103-divvy-tripdata.csv")
```


Check column names of each dataset for consistency


```r
colnames(tripdata_202004)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202005)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202006)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202007)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202008)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202009)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202010)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202011)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202012)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202101)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202102)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(tripdata_202103)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```
Check data structures and data types for all data frames

```r
str(tripdata_202004)
```

```
## 'data.frame':	84776 obs. of  13 variables:
##  $ ride_id           : chr  "A847FADBBC638E45" "5405B80E996FF60D" "5DD24A79A4E006F4" "2A59BBDF5CDBA725" ...
##  $ rideable_type     : chr  "docked_bike" "docked_bike" "docked_bike" "docked_bike" ...
##  $ started_at        : chr  "2020-04-26 17:45:14" "2020-04-17 17:08:54" "2020-04-01 17:54:13" "2020-04-07 12:50:19" ...
##  $ ended_at          : chr  "2020-04-26 18:12:03" "2020-04-17 17:17:03" "2020-04-01 18:08:36" "2020-04-07 13:02:31" ...
##  $ start_station_name: chr  "Eckhart Park" "Drake Ave & Fullerton Ave" "McClurg Ct & Erie St" "California Ave & Division St" ...
##  $ start_station_id  : int  86 503 142 216 125 173 35 434 627 377 ...
##  $ end_station_name  : chr  "Lincoln Ave & Diversey Pkwy" "Kosciuszko Park" "Indiana Ave & Roosevelt Rd" "Wood St & Augusta Blvd" ...
##  $ end_station_id    : int  152 499 255 657 323 35 635 382 359 508 ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.7 -87.7 -87.6 -87.7 -87.6 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 42 ...
##  $ end_lng           : num  -87.7 -87.7 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr  "member" "member" "member" "member" ...
```

```r
str(tripdata_202005)
```

```
## 'data.frame':	200274 obs. of  13 variables:
##  $ ride_id           : chr  "02668AD35674B983" "7A50CCAF1EDDB28F" "2FFCDFDB91FE9A52" "58991CF1DB75BA84" ...
##  $ rideable_type     : chr  "docked_bike" "docked_bike" "docked_bike" "docked_bike" ...
##  $ started_at        : chr  "2020-05-27 10:03:52" "2020-05-25 10:47:11" "2020-05-02 14:11:03" "2020-05-02 16:25:36" ...
##  $ ended_at          : chr  "2020-05-27 10:16:49" "2020-05-25 11:05:40" "2020-05-02 15:48:21" "2020-05-02 16:39:28" ...
##  $ start_station_name: chr  "Franklin St & Jackson Blvd" "Clark St & Wrightwood Ave" "Kedzie Ave & Milwaukee Ave" "Clarendon Ave & Leland Ave" ...
##  $ start_station_id  : int  36 340 260 251 261 206 261 180 331 219 ...
##  $ end_station_name  : chr  "Wabash Ave & Grand Ave" "Clark St & Leland Ave" "Kedzie Ave & Milwaukee Ave" "Lake Shore Dr & Wellington Ave" ...
##  $ end_station_id    : int  199 326 260 157 206 22 261 180 300 305 ...
##  $ start_lat         : num  41.9 41.9 41.9 42 41.9 ...
##  $ start_lng         : num  -87.6 -87.6 -87.7 -87.7 -87.7 ...
##  $ end_lat           : num  41.9 42 41.9 41.9 41.8 ...
##  $ end_lng           : num  -87.6 -87.7 -87.7 -87.6 -87.6 ...
##  $ member_casual     : chr  "member" "casual" "casual" "casual" ...
```

```r
str(tripdata_202006)
```

```
## 'data.frame':	343005 obs. of  13 variables:
##  $ ride_id           : chr  "8CD5DE2C2B6C4CFC" "9A191EB2C751D85D" "F37D14B0B5659BCF" "C41237B506E85FA1" ...
##  $ rideable_type     : chr  "docked_bike" "docked_bike" "docked_bike" "docked_bike" ...
##  $ started_at        : chr  "2020-06-13 23:24:48" "2020-06-26 07:26:10" "2020-06-23 17:12:41" "2020-06-20 01:09:35" ...
##  $ ended_at          : chr  "2020-06-13 23:36:55" "2020-06-26 07:31:58" "2020-06-23 17:21:14" "2020-06-20 01:28:24" ...
##  $ start_station_name: chr  "Wilton Ave & Belmont Ave" "Federal St & Polk St" "Daley Center Plaza" "Broadway & Cornelia Ave" ...
##  $ start_station_id  : int  117 41 81 303 327 327 41 115 338 84 ...
##  $ end_station_name  : chr  "Damen Ave & Clybourn Ave" "Daley Center Plaza" "State St & Harrison St" "Broadway & Berwyn Ave" ...
##  $ end_station_id    : int  163 81 5 294 117 117 81 303 164 53 ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.7 -87.6 -87.6 -87.6 -87.7 ...
##  $ end_lat           : num  41.9 41.9 41.9 42 41.9 ...
##  $ end_lng           : num  -87.7 -87.6 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr  "casual" "member" "member" "casual" ...
```

```r
str(tripdata_202007)
```

```
## 'data.frame':	551480 obs. of  13 variables:
##  $ ride_id           : chr  "762198876D69004D" "BEC9C9FBA0D4CF1B" "D2FD8EA432C77EC1" "54AE594E20B35881" ...
##  $ rideable_type     : chr  "docked_bike" "docked_bike" "docked_bike" "docked_bike" ...
##  $ started_at        : chr  "2020-07-09 15:22:02" "2020-07-24 23:56:30" "2020-07-08 19:49:07" "2020-07-17 19:06:42" ...
##  $ ended_at          : chr  "2020-07-09 15:25:52" "2020-07-25 00:20:17" "2020-07-08 19:56:22" "2020-07-17 19:27:38" ...
##  $ start_station_name: chr  "Ritchie Ct & Banks St" "Halsted St & Roscoe St" "Lake Shore Dr & Diversey Pkwy" "LaSalle St & Illinois St" ...
##  $ start_station_id  : int  180 299 329 181 268 635 113 211 176 31 ...
##  $ end_station_name  : chr  "Wells St & Evergreen Ave" "Broadway & Ridge Ave" "Clark St & Wellington Ave" "Clark St & Armitage Ave" ...
##  $ end_station_id    : int  291 461 156 94 301 289 140 31 191 142 ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num  41.9 42 41.9 41.9 41.9 ...
##  $ end_lng           : num  -87.6 -87.7 -87.6 -87.6 -87.6 ...
##  $ member_casual     : chr  "member" "member" "casual" "casual" ...
```

```r
str(tripdata_202008)
```

```
## 'data.frame':	622361 obs. of  13 variables:
##  $ ride_id           : chr  "322BD23D287743ED" "2A3AEF1AB9054D8B" "67DC1D133E8B5816" "C79FBBD412E578A7" ...
##  $ rideable_type     : chr  "docked_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : chr  "2020-08-20 18:08:14" "2020-08-27 18:46:04" "2020-08-26 19:44:14" "2020-08-27 12:05:41" ...
##  $ ended_at          : chr  "2020-08-20 18:17:51" "2020-08-27 19:54:51" "2020-08-26 21:53:07" "2020-08-27 12:53:45" ...
##  $ start_station_name: chr  "Lake Shore Dr & Diversey Pkwy" "Michigan Ave & 14th St" "Columbus Dr & Randolph St" "Daley Center Plaza" ...
##  $ start_station_id  : int  329 168 195 81 658 658 196 67 153 177 ...
##  $ end_station_name  : chr  "Clark St & Lincoln Ave" "Michigan Ave & 14th St" "State St & Randolph St" "State St & Kinzie St" ...
##  $ end_station_id    : int  141 168 44 47 658 658 49 229 225 305 ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.6 -87.6 -87.6 -87.6 -87.7 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num  -87.6 -87.6 -87.6 -87.6 -87.7 ...
##  $ member_casual     : chr  "member" "casual" "casual" "casual" ...
```

```r
str(tripdata_202009)
```

```
## 'data.frame':	532958 obs. of  13 variables:
##  $ ride_id           : chr  "2B22BD5F95FB2629" "A7FB70B4AFC6CAF2" "86057FA01BAC778E" "57F6DC9A153DB98C" ...
##  $ rideable_type     : chr  "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : chr  "2020-09-17 14:27:11" "2020-09-17 15:07:31" "2020-09-17 15:09:04" "2020-09-17 18:10:46" ...
##  $ ended_at          : chr  "2020-09-17 14:44:24" "2020-09-17 15:07:45" "2020-09-17 15:09:35" "2020-09-17 18:35:49" ...
##  $ start_station_name: chr  "Michigan Ave & Lake St" "W Oakdale Ave & N Broadway" "W Oakdale Ave & N Broadway" "Ashland Ave & Belle Plaine Ave" ...
##  $ start_station_id  : int  52 NA NA 246 24 94 291 NA NA NA ...
##  $ end_station_name  : chr  "Green St & Randolph St" "W Oakdale Ave & N Broadway" "W Oakdale Ave & N Broadway" "Montrose Harbor" ...
##  $ end_station_id    : int  112 NA NA 249 24 NA 256 NA NA NA ...
##  $ start_lat         : num  41.9 41.9 41.9 42 41.9 ...
##  $ start_lng         : num  -87.6 -87.6 -87.6 -87.7 -87.6 ...
##  $ end_lat           : num  41.9 41.9 41.9 42 41.9 ...
##  $ end_lng           : num  -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ member_casual     : chr  "casual" "casual" "casual" "casual" ...
```

```r
str(tripdata_202010)
```

```
## 'data.frame':	388653 obs. of  13 variables:
##  $ ride_id           : chr  "ACB6B40CF5B9044C" "DF450C72FD109C01" "B6396B54A15AC0DF" "44A4AEE261B9E854" ...
##  $ rideable_type     : chr  "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : chr  "2020-10-31 19:39:43" "2020-10-31 23:50:08" "2020-10-31 23:00:01" "2020-10-31 22:16:43" ...
##  $ ended_at          : chr  "2020-10-31 19:57:12" "2020-11-01 00:04:16" "2020-10-31 23:08:22" "2020-10-31 22:19:35" ...
##  $ start_station_name: chr  "Lakeview Ave & Fullerton Pkwy" "Southport Ave & Waveland Ave" "Stony Island Ave & 67th St" "Clark St & Grace St" ...
##  $ start_station_id  : int  313 227 102 165 190 359 313 125 NA 174 ...
##  $ end_station_name  : chr  "Rush St & Hubbard St" "Kedzie Ave & Milwaukee Ave" "University Ave & 57th St" "Broadway & Sheridan Rd" ...
##  $ end_station_id    : int  125 260 423 256 185 53 125 313 199 635 ...
##  $ start_lat         : num  41.9 41.9 41.8 42 41.9 ...
##  $ start_lng         : num  -87.6 -87.7 -87.6 -87.7 -87.7 ...
##  $ end_lat           : num  41.9 41.9 41.8 42 41.9 ...
##  $ end_lng           : num  -87.6 -87.7 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr  "casual" "casual" "casual" "casual" ...
```

```r
str(tripdata_202011)
```

```
## 'data.frame':	259716 obs. of  13 variables:
##  $ ride_id           : chr  "BD0A6FF6FFF9B921" "96A7A7A4BDE4F82D" "C61526D06582BDC5" "E533E89C32080B9E" ...
##  $ rideable_type     : chr  "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : chr  "2020-11-01 13:36:00" "2020-11-01 10:03:26" "2020-11-01 00:34:05" "2020-11-01 00:45:16" ...
##  $ ended_at          : chr  "2020-11-01 13:45:40" "2020-11-01 10:14:45" "2020-11-01 01:03:06" "2020-11-01 00:54:31" ...
##  $ start_station_name: chr  "Dearborn St & Erie St" "Franklin St & Illinois St" "Lake Shore Dr & Monroe St" "Leavitt St & Chicago Ave" ...
##  $ start_station_id  : int  110 672 76 659 2 72 76 NA 58 394 ...
##  $ end_station_name  : chr  "St. Clair St & Erie St" "Noble St & Milwaukee Ave" "Federal St & Polk St" "Stave St & Armitage Ave" ...
##  $ end_station_id    : int  211 29 41 185 2 76 72 NA 288 273 ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.6 -87.6 -87.6 -87.7 -87.6 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num  -87.6 -87.7 -87.6 -87.7 -87.6 ...
##  $ member_casual     : chr  "casual" "casual" "casual" "casual" ...
```

```r
str(tripdata_202012)
```

```
## 'data.frame':	131573 obs. of  13 variables:
##  $ ride_id           : chr  "70B6A9A437D4C30D" "158A465D4E74C54A" "5262016E0F1F2F9A" "BE119628E44F871E" ...
##  $ rideable_type     : chr  "classic_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : chr  "2020-12-27 12:44:29" "2020-12-18 17:37:15" "2020-12-15 15:04:33" "2020-12-15 15:54:18" ...
##  $ ended_at          : chr  "2020-12-27 12:55:06" "2020-12-18 17:44:19" "2020-12-15 15:11:28" "2020-12-15 16:00:11" ...
##  $ start_station_name: chr  "Aberdeen St & Jackson Blvd" "" "" "" ...
##  $ start_station_id  : chr  "13157" "" "" "" ...
##  $ end_station_name  : chr  "Desplaines St & Kinzie St" "" "" "" ...
##  $ end_station_id    : chr  "TA1306000003" "" "" "" ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.8 ...
##  $ start_lng         : num  -87.7 -87.7 -87.7 -87.7 -87.6 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 41.8 ...
##  $ end_lng           : num  -87.6 -87.7 -87.7 -87.7 -87.6 ...
##  $ member_casual     : chr  "member" "member" "member" "member" ...
```

```r
str(tripdata_202101)
```

```
## 'data.frame':	96834 obs. of  13 variables:
##  $ ride_id           : chr  "E19E6F1B8D4C42ED" "DC88F20C2C55F27F" "EC45C94683FE3F27" "4FA453A75AE377DB" ...
##  $ rideable_type     : chr  "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : chr  "2021-01-23 16:14:19" "2021-01-27 18:43:08" "2021-01-21 22:35:54" "2021-01-07 13:31:13" ...
##  $ ended_at          : chr  "2021-01-23 16:24:44" "2021-01-27 18:47:12" "2021-01-21 22:37:14" "2021-01-07 13:42:55" ...
##  $ start_station_name: chr  "California Ave & Cortez St" "California Ave & Cortez St" "California Ave & Cortez St" "California Ave & Cortez St" ...
##  $ start_station_id  : chr  "17660" "17660" "17660" "17660" ...
##  $ end_station_name  : chr  "" "" "" "" ...
##  $ end_station_id    : chr  "" "" "" "" ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.7 -87.7 -87.7 -87.7 -87.7 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num  -87.7 -87.7 -87.7 -87.7 -87.7 ...
##  $ member_casual     : chr  "member" "member" "member" "member" ...
```

```r
str(tripdata_202102)
```

```
## 'data.frame':	49622 obs. of  13 variables:
##  $ ride_id           : chr  "89E7AA6C29227EFF" "0FEFDE2603568365" "E6159D746B2DBB91" "B32D3199F1C2E75B" ...
##  $ rideable_type     : chr  "classic_bike" "classic_bike" "electric_bike" "classic_bike" ...
##  $ started_at        : chr  "2021-02-12 16:14:56" "2021-02-14 17:52:38" "2021-02-09 19:10:18" "2021-02-02 17:49:41" ...
##  $ ended_at          : chr  "2021-02-12 16:21:43" "2021-02-14 18:12:09" "2021-02-09 19:19:10" "2021-02-02 17:54:06" ...
##  $ start_station_name: chr  "Glenwood Ave & Touhy Ave" "Glenwood Ave & Touhy Ave" "Clark St & Lake St" "Wood St & Chicago Ave" ...
##  $ start_station_id  : chr  "525" "525" "KA1503000012" "637" ...
##  $ end_station_name  : chr  "Sheridan Rd & Columbia Ave" "Bosworth Ave & Howard St" "State St & Randolph St" "Honore St & Division St" ...
##  $ end_station_id    : chr  "660" "16806" "TA1305000029" "TA1305000034" ...
##  $ start_lat         : num  42 42 41.9 41.9 41.8 ...
##  $ start_lng         : num  -87.7 -87.7 -87.6 -87.7 -87.6 ...
##  $ end_lat           : num  42 42 41.9 41.9 41.8 ...
##  $ end_lng           : num  -87.7 -87.7 -87.6 -87.7 -87.6 ...
##  $ member_casual     : chr  "member" "casual" "member" "member" ...
```

```r
str(tripdata_202103)
```

```
## 'data.frame':	228496 obs. of  13 variables:
##  $ ride_id           : chr  "CFA86D4455AA1030" "30D9DC61227D1AF3" "846D87A15682A284" "994D05AA75A168F2" ...
##  $ rideable_type     : chr  "classic_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : chr  "2021-03-16 08:32:30" "2021-03-28 01:26:28" "2021-03-11 21:17:29" "2021-03-11 13:26:42" ...
##  $ ended_at          : chr  "2021-03-16 08:36:34" "2021-03-28 01:36:55" "2021-03-11 21:33:53" "2021-03-11 13:55:41" ...
##  $ start_station_name: chr  "Humboldt Blvd & Armitage Ave" "Humboldt Blvd & Armitage Ave" "Shields Ave & 28th Pl" "Winthrop Ave & Lawrence Ave" ...
##  $ start_station_id  : chr  "15651" "15651" "15443" "TA1308000021" ...
##  $ end_station_name  : chr  "Stave St & Armitage Ave" "Central Park Ave & Bloomingdale Ave" "Halsted St & 35th St" "Broadway & Sheridan Rd" ...
##  $ end_station_id    : chr  "13266" "18017" "TA1308000043" "13323" ...
##  $ start_lat         : num  41.9 41.9 41.8 42 42 ...
##  $ start_lng         : num  -87.7 -87.7 -87.6 -87.7 -87.7 ...
##  $ end_lat           : num  41.9 41.9 41.8 42 42.1 ...
##  $ end_lng           : num  -87.7 -87.7 -87.6 -87.6 -87.7 ...
##  $ member_casual     : chr  "casual" "casual" "casual" "casual" ...
```
### Data transformation and cleaning

tart_station_id & end_station_id are not consistent in all datasets.Convert the inconsistent ones from int to char datatype.

```r
tripdata_202004 <- tripdata_202004 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202005 <- tripdata_202005 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202006 <- tripdata_202006 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202008 <- tripdata_202008 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202009 <- tripdata_202009 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202010 <- tripdata_202010 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202011 <- tripdata_202011 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
tripdata_202007 <- tripdata_202007 %>% mutate(start_station_id = as.character(start_station_id), end_station_id = as.character(end_station_id))
```


###  3. Process
Combine all the datasets into one single dataframe


```r
all_trips <- bind_rows(tripdata_202004,tripdata_202005,tripdata_202006,tripdata_202007,tripdata_202008,tripdata_202009,tripdata_202010,tripdata_202011,tripdata_202012,tripdata_202101,tripdata_202102,tripdata_202103)

str(all_trips)
```

```
## 'data.frame':	3489748 obs. of  13 variables:
##  $ ride_id           : chr  "A847FADBBC638E45" "5405B80E996FF60D" "5DD24A79A4E006F4" "2A59BBDF5CDBA725" ...
##  $ rideable_type     : chr  "docked_bike" "docked_bike" "docked_bike" "docked_bike" ...
##  $ started_at        : chr  "2020-04-26 17:45:14" "2020-04-17 17:08:54" "2020-04-01 17:54:13" "2020-04-07 12:50:19" ...
##  $ ended_at          : chr  "2020-04-26 18:12:03" "2020-04-17 17:17:03" "2020-04-01 18:08:36" "2020-04-07 13:02:31" ...
##  $ start_station_name: chr  "Eckhart Park" "Drake Ave & Fullerton Ave" "McClurg Ct & Erie St" "California Ave & Division St" ...
##  $ start_station_id  : chr  "86" "503" "142" "216" ...
##  $ end_station_name  : chr  "Lincoln Ave & Diversey Pkwy" "Kosciuszko Park" "Indiana Ave & Roosevelt Rd" "Wood St & Augusta Blvd" ...
##  $ end_station_id    : chr  "152" "499" "255" "657" ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.7 -87.7 -87.6 -87.7 -87.6 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 42 ...
##  $ end_lng           : num  -87.7 -87.7 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr  "member" "member" "member" "member" ...
```


### Clean-up further!
Hold on! started_at & ended_at should be in datetime datatype instead of char. Convert all from char to datetime


```r
all_trips[['started_at']] <- ymd_hms(all_trips[['started_at']])
all_trips[['ended_at']] <- ymd_hms(all_trips[['ended_at']])

str(all_trips)
```

```
## 'data.frame':	3489748 obs. of  13 variables:
##  $ ride_id           : chr  "A847FADBBC638E45" "5405B80E996FF60D" "5DD24A79A4E006F4" "2A59BBDF5CDBA725" ...
##  $ rideable_type     : chr  "docked_bike" "docked_bike" "docked_bike" "docked_bike" ...
##  $ started_at        : POSIXct, format: "2020-04-26 17:45:14" "2020-04-17 17:08:54" ...
##  $ ended_at          : POSIXct, format: "2020-04-26 18:12:03" "2020-04-17 17:17:03" ...
##  $ start_station_name: chr  "Eckhart Park" "Drake Ave & Fullerton Ave" "McClurg Ct & Erie St" "California Ave & Division St" ...
##  $ start_station_id  : chr  "86" "503" "142" "216" ...
##  $ end_station_name  : chr  "Lincoln Ave & Diversey Pkwy" "Kosciuszko Park" "Indiana Ave & Roosevelt Rd" "Wood St & Augusta Blvd" ...
##  $ end_station_id    : chr  "152" "499" "255" "657" ...
##  $ start_lat         : num  41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num  -87.7 -87.7 -87.6 -87.7 -87.6 ...
##  $ end_lat           : num  41.9 41.9 41.9 41.9 42 ...
##  $ end_lng           : num  -87.7 -87.7 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr  "member" "member" "member" "member" ...
```

###  Remove columns not required or beyond the scope of project

```r
all_trips <- all_trips %>%
    select(-c(start_lat:end_lng))
glimpse(all_trips)
```

```
## Rows: 3,489,748
## Columns: 9
## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4…
## $ rideable_type      <chr> "docked_bike", "docked_bike", "docked_bike", "docke…
## $ started_at         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-…
## $ ended_at           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-…
## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu…
## $ start_station_id   <chr> "86", "503", "142", "216", "125", "173", "35", "434…
## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "…
## $ end_station_id     <chr> "152", "499", "255", "657", "323", "35", "635", "38…
## $ member_casual      <chr> "member", "member", "member", "member", "casual", "…
```


###  Rename columns for better readability

```r
all_trips <- all_trips %>%
    rename(ride_type = rideable_type, 
           start_time = started_at,
           end_time = ended_at,
           customer_type = member_casual)
glimpse(all_trips)
```

```
## Rows: 3,489,748
## Columns: 9
## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4…
## $ ride_type          <chr> "docked_bike", "docked_bike", "docked_bike", "docke…
## $ start_time         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-…
## $ end_time           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-…
## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu…
## $ start_station_id   <chr> "86", "503", "142", "216", "125", "173", "35", "434…
## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "…
## $ end_station_id     <chr> "152", "499", "255", "657", "323", "35", "635", "38…
## $ customer_type      <chr> "member", "member", "member", "member", "casual", "…
```

### Removing duplicates

```r
new_all_trips <- all_trips[!duplicated(all_trips$ride_id), ]

glimpse(new_all_trips)
```

```
## Rows: 3,489,539
## Columns: 9
## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4…
## $ ride_type          <chr> "docked_bike", "docked_bike", "docked_bike", "docke…
## $ start_time         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-…
## $ end_time           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-…
## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu…
## $ start_station_id   <chr> "86", "503", "142", "216", "125", "173", "35", "434…
## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "…
## $ end_station_id     <chr> "152", "499", "255", "657", "323", "35", "635", "38…
## $ customer_type      <chr> "member", "member", "member", "member", "casual", "…
```
###  Add new columns that can be used for aggregate functions


```r
new_all_trips$day_of_the_week <- format(as.Date(new_all_trips$start_time),'%a')
new_all_trips$month <- format(as.Date(new_all_trips$start_time),'%b_%y')
```




```r
new_all_trips$time <- format(new_all_trips$start_time, format = "%H:%M")
new_all_trips$time <- as.POSIXct(new_all_trips$time, format = "%H:%M")
```


### find time duration


```r
new_all_trips$trip_duration <- (as.double(difftime(new_all_trips$end_time, new_all_trips$start_time)))/60
```





```r
glimpse(new_all_trips)
```

```
## Rows: 3,489,539
## Columns: 13
## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4…
## $ ride_type          <chr> "docked_bike", "docked_bike", "docked_bike", "docke…
## $ start_time         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-…
## $ end_time           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-…
## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu…
## $ start_station_id   <chr> "86", "503", "142", "216", "125", "173", "35", "434…
## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "…
## $ end_station_id     <chr> "152", "499", "255", "657", "323", "35", "635", "38…
## $ customer_type      <chr> "member", "member", "member", "member", "casual", "…
## $ day_of_the_week    <chr> "Sun", "Fri", "Wed", "Tue", "Sat", "Thu", "Thu", "T…
## $ month              <chr> "Apr_20", "Apr_20", "Apr_20", "Apr_20", "Apr_20", "…
## $ time               <dttm> 2022-06-15 17:45:00, 2022-06-15 17:08:00, 2022-06-…
## $ trip_duration      <dbl> 26.816667, 8.150000, 14.383333, 12.200000, 52.91666…
```


Let's check to see if the trip_duration column has any negative values, as this may cause problem while creating visualizations. Also, we do not want to include the trips that were part of quality tests by the company. These trips are usually identified by string 'test' in the start_station_name column.


```r
nrow(subset(new_all_trips,trip_duration < 0))
```

```
## [1] 10343
```
### checking for testrides that were made by company for quality checks


```r
nrow(subset(new_all_trips, start_station_name %like% "TEST"))
```

```
## [1] 3364
```

```r
nrow(subset(new_all_trips, start_station_name %like% "test"))
```

```
## [1] 3
```

```r
nrow(subset(new_all_trips, start_station_name %like% "Test"))
```

```
## [1] 0
```
As there are 10343 rows with trip_dration less than 0 mins and 3367 trips that were test rides, we will remove these observations from our dataframe as they contribute to only about 0.3% of the total rows. We will create a new dataframe deviod of these obseravtions without making any changes to the existing dataframe.


```r
all_trips_v2 <- new_all_trips[!(new_all_trips$trip_duration < 0),]
```


```r
all_trips_v2<- all_trips_v2[!((all_trips_v2$start_station_name %like% "TEST" | all_trips_v2$start_station_name %like% "test")),]
```



```r
glimpse(all_trips_v2)
```

```
## Rows: 3,475,844
## Columns: 13
## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4…
## $ ride_type          <chr> "docked_bike", "docked_bike", "docked_bike", "docke…
## $ start_time         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-…
## $ end_time           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-…
## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu…
## $ start_station_id   <chr> "86", "503", "142", "216", "125", "173", "35", "434…
## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "…
## $ end_station_id     <chr> "152", "499", "255", "657", "323", "35", "635", "38…
## $ customer_type      <chr> "member", "member", "member", "member", "casual", "…
## $ day_of_the_week    <chr> "Sun", "Fri", "Wed", "Tue", "Sat", "Thu", "Thu", "T…
## $ month              <chr> "Apr_20", "Apr_20", "Apr_20", "Apr_20", "Apr_20", "…
## $ time               <dttm> 2022-06-15 17:45:00, 2022-06-15 17:08:00, 2022-06-…
## $ trip_duration      <dbl> 26.816667, 8.150000, 14.383333, 12.200000, 52.91666…
```

It is important to make sure that customer_type column has only two distinct values. Let's confirm the same.

```r
table(all_trips_v2$customer_type)
```

```
## 
##  casual  member 
## 1423876 2051968
```



```r
setNames(aggregate(trip_duration ~ customer_type, all_trips_v2, sum), c("customer_type", "total_trip_duration(mins)"))
```

```
##   customer_type total_trip_duration(mins)
## 1        casual                  64176592
## 2        member                  33068730
```



## Analyze and Share the Data


```r
summary(all_trips_v2$trip_duration)
```

```
##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
##     0.00     7.95    14.58    27.98    26.70 58720.03
```




```r
all_trips_v2 %>%
    group_by(customer_type) %>%
    summarise(min_trip_duration = min(trip_duration),max_trip_duration = max(trip_duration),
              median_trip_duration = median(trip_duration), mean_trip_duration = mean(trip_duration))
```

```
## # A tibble: 2 × 5
##   customer_type min_trip_duration max_trip_duration median_trip_duration
##   <chr>                     <dbl>             <dbl>                <dbl>
## 1 casual                        0            55684.                 21.3
## 2 member                        0            58720.                 11.5
## # … with 1 more variable: mean_trip_duration <dbl>
```


The mean trip duration of member riders is lower than the mean trip duration of all trips, while it is exactly the opposite for casual riders, whose mean trip duration is higher than the the mean trip duration of all trips. This tells us that casual riders usually take the bikes out for a longer duration compared to members

### Total number of trips by customer type and day of the week


```r
all_trips_v2$day_of_the_week <- ordered(all_trips_v2$day_of_the_week, levels=c("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"))
```



```r
all_trips_v2$month <- ordered(all_trips_v2$month, levels=c("Apr_20", "May_20", "Jun_20", "Jul_20", "Aug_20", "Sep_20", "Oct_20","Nov_20", "Dec_20", "Jan_21", "Feb_21", "Mar_21", "Apr_21", "May_21", "Jun_21", "Jul_21"))
```


```r
all_trips_v2 %>% 
  group_by(customer_type, day_of_the_week) %>%  
  summarise(number_of_rides = n(),average_duration_mins = mean(trip_duration)) %>% 
  arrange(customer_type, desc(number_of_rides))
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

```
## # A tibble: 14 × 4
## # Groups:   customer_type [2]
##    customer_type day_of_the_week number_of_rides average_duration_mins
##    <chr>         <ord>                     <int>                 <dbl>
##  1 casual        Sat                      334933                  47.0
##  2 casual        Sun                      262183                  50.8
##  3 casual        Fri                      207852                  42.9
##  4 casual        Thu                      165806                  43.1
##  5 casual        Wed                      157849                  40.5
##  6 casual        Mon                      150590                  45.1
##  7 casual        Tue                      144663                  40.7
##  8 member        Sat                      323109                  17.8
##  9 member        Fri                      306388                  15.8
## 10 member        Wed                      305049                  15.3
## 11 member        Thu                      300439                  15.2
## 12 member        Tue                      284366                  15.1
## 13 member        Mon                      267326                  15.3
## 14 member        Sun                      265291                  18.2
```



###  Visualization:


```r
all_trips_v2 %>%  
  group_by(customer_type, day_of_the_week) %>% 
  summarise(number_of_rides = n()) %>% 
  arrange(customer_type, day_of_the_week)  %>% 
  ggplot(aes(x = day_of_the_week, y = number_of_rides, fill = customer_type)) +
  labs(title ="Total trips by customer type Vs. Day of the week") +
  geom_col(width=0.5, position = position_dodge(width=0.5)) +
  scale_y_continuous(labels = function(x) format(x, scientific = FALSE))
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

![plot of chunk unnamed-chunk-28](figure/unnamed-chunk-28-1.png)
From the table and graph above, casual customers are most busy on Sundays followed by Saturdays, while members are most busy on later half of the week extending into the weekend. Interesting pattern to note though is the consistent trip numbers among members with less spread over entire week as compared to casual riders who don't seem to use the bikeshare services much during weekdays


### Average number of trips by customer type and month

```r
unique(new_all_trips$month)
```

```
##  [1] "Apr_20" "May_20" "Jun_20" "Jul_20" "Aug_20" "Sep_20" "Oct_20" "Nov_20"
##  [9] "Dec_20" "Jan_21" "Feb_21" "Mar_21"
```


```r
all_trips_v2 %>% 
  group_by(customer_type, month) %>%  
  summarise(number_of_rides = n(),`average_duration_(mins)` = mean(trip_duration)) %>%
  arrange(customer_type,desc(number_of_rides))
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

```
## # A tibble: 24 × 4
## # Groups:   customer_type [2]
##    customer_type month  number_of_rides `average_duration_(mins)`
##    <chr>         <ord>            <int>                     <dbl>
##  1 casual        Aug_20          287171                      45.2
##  2 casual        Jul_20          268549                      60.0
##  3 casual        Sep_20          229435                      38.3
##  4 casual        Jun_20          154401                      51.7
##  5 casual        Oct_20          143850                      30.4
##  6 casual        Nov_20           87810                      31.9
##  7 casual        May_20           86786                      51.3
##  8 casual        Mar_21           84032                      38.2
##  9 casual        Dec_20           29997                      26.8
## 10 casual        Apr_20           23597                      73.2
## # … with 14 more rows
```



```r
all_trips_v2 %>%  
  group_by(customer_type, month) %>% 
  summarise(number_of_rides = n()) %>% 
  arrange(customer_type, month)  %>% 
  ggplot(aes(x = month, y = number_of_rides, fill = customer_type)) +
  labs(title ="Total trips by customer type Vs. Month") +
  theme(axis.text.x = element_text(angle = 30)) +
  geom_col(width=0.5, position = position_dodge(width=0.5)) +
  scale_y_continuous(labels = function(x) format(x, scientific = FALSE))
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

![plot of chunk unnamed-chunk-31](figure/unnamed-chunk-31-1.png)

### Visualizaton of average trip duration by customer type on each day of the week

```r
all_trips_v2 %>%  
  group_by(customer_type, day_of_the_week) %>% 
  summarise(average_trip_duration = mean(trip_duration)) %>%
  ggplot(aes(x = day_of_the_week, y = average_trip_duration, fill = customer_type)) +
  geom_col(width=0.5, position = position_dodge(width=0.5)) + 
  labs(title ="Average trip duration by customer type Vs. Day of the week")
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

![plot of chunk unnamed-chunk-32](figure/unnamed-chunk-32-1.png)

### Visualizaton of average trip duration by customer type Vs. month

```r
all_trips_v2 %>%  
  group_by(customer_type, month) %>% 
  summarise(average_trip_duration = mean(trip_duration)) %>%
  ggplot(aes(x = month, y = average_trip_duration, fill = customer_type)) +
  geom_col(width=0.5, position = position_dodge(width=0.5)) + 
  labs(title ="Average trip duration by customer type Vs. Month") +
  theme(axis.text.x = element_text(angle = 30))
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

![plot of chunk unnamed-chunk-33](figure/unnamed-chunk-33-1.png)

Average trip duration of member riders is anywhere between 10-20 minutes throughout the year, exception being April when it goes slightly over 20 minutes. However, there seems to be a distinct pattern when it comes to casual riders, whose average trip duration swings wildly from as low as ~25 minutes to more than an hour depending on time of the year. It is worth noting unusually long trip durations by casual riders in the month of April



```r
all_trips_v2 %>%  
  group_by(customer_type, time) %>% 
  summarise(number_of_trips = n()) %>%
  ggplot(aes(x = time, y = number_of_trips, color = customer_type, group = customer_type)) +
  geom_line() +
  scale_x_datetime(date_breaks = "1 hour", minor_breaks = NULL,
                   date_labels = "%H:%M", expand = c(0,0)) +
  theme(axis.text.x = element_text(angle = 90)) +
  labs(title ="Demand over 24 hours of a day", x = "Time of the day")
```

```
## `summarise()` has grouped output by 'customer_type'. You can override using the
## `.groups` argument.
```

![plot of chunk unnamed-chunk-34](figure/unnamed-chunk-34-1.png)

```r
all_trips_v2 %>%
  group_by(ride_type, customer_type) %>%
  summarise(number_of_trips = n()) %>%  
  ggplot(aes(x= ride_type, y=number_of_trips, fill= customer_type))+
              geom_bar(stat='identity') +
  scale_y_continuous(labels = function(x) format(x, scientific = FALSE)) +
  labs(title ="Ride type Vs. Number of trips")
```

```
## `summarise()` has grouped output by 'ride_type'. You can override using the
## `.groups` argument.
```

![plot of chunk unnamed-chunk-35](figure/unnamed-chunk-35-1.png)
 Docked bikes are in most demand and equally used by both members
 
### Creating a csv file of the clean data for futher analysis or visualizations in other tools like SQL, Tableau, Power BI, etc
 
 
 

```r
clean_data <- aggregate(all_trips_v2$trip_duration ~ all_trips_v2$customer_type + all_trips_v2$day_of_the_week, FUN = mean)
```
 
 

```r
write.csv(clean_data, "Clean Data.csv", row.names = F)
```
 
## 6. Act

### Key Takeaways

*  Casual customers use bikeshare services more during weekends, while members use them consistently over the entire week.

*  Average trip duration of casual riders is more than twice that of member rider over any given day of the week cumulatively.

*  Casual riders ride longer during first half of the year compared to the second half, while members clock relatively similar average trip duration month over month.


## Recommendations

* Provide attractive promotions for casual riders on weekdays so that casual members use the bikeshare services ore uniformly across the entire week

* Offer discounted membership fee for renewals after the first year. It might nudge casual riders to take up membership.

*  Offer discounted pricing during non-busy hours so that casual riders might choose to use bikes more often and level out demand over the day
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 


