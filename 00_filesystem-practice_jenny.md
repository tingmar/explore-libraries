00\_filesystem-practice\_jenny.R
================
tma
Wed Jan 31 14:11:28 2018

``` r
## First attempt: Just get it to work ----
normalizePath("~")
```

    ## [1] "/Users/tma"

``` r
list.files("~/Desktop/day1_s1_explore-libraries")
```

    ## [1] "01_explore-libraries_comfy.R"    "01_explore-libraries_jenny.R"   
    ## [3] "01_explore-libraries_spartan.R"  "day1_s1_explore-libraries.Rproj"
    ## [5] "r_code.R"

``` r
list.files("~/Desktop/day1_s1_explore-libraries", pattern = "\\.R$")
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R" "r_code.R"

``` r
list.files(
  "~/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)
```

    ## [1] "/Users/tma/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R"  
    ## [2] "/Users/tma/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R"  
    ## [3] "/Users/tma/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R"
    ## [4] "/Users/tma/Desktop/day1_s1_explore-libraries/r_code.R"

``` r
from_files <- list.files(
  "~/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)

(to_files <- basename(from_files))
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R" "r_code.R"

``` r
file.copy(from_files, to_files)
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
list.files()
```

    ##  [1] "00_filesystem-practice_comfy.R"       
    ##  [2] "00_filesystem-practice_jenny.R"       
    ##  [3] "00_filesystem-practice_jenny.spin.R"  
    ##  [4] "00_filesystem-practice_jenny.spin.Rmd"
    ##  [5] "00_filesystem-practice_spartan.html"  
    ##  [6] "00_filesystem-practice_spartan.R"     
    ##  [7] "01_explore-libraries_comfy.R"         
    ##  [8] "01_explore-libraries_jenny.R"         
    ##  [9] "01_explore-libraries_spartan.R"       
    ## [10] "explore-libraries.Rproj"              
    ## [11] "r_code.R"                             
    ## [12] "README.md"

``` r
## Clean it out, so we can refine ----
file.remove(to_files)
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "00_filesystem-practice_comfy.R"       
    ## [2] "00_filesystem-practice_jenny.R"       
    ## [3] "00_filesystem-practice_jenny.spin.R"  
    ## [4] "00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "00_filesystem-practice_spartan.html"  
    ## [6] "00_filesystem-practice_spartan.R"     
    ## [7] "explore-libraries.Rproj"              
    ## [8] "README.md"

``` r
## Copy again, tighter code ----
from_dir <- file.path("~", "Desktop", "day1_s1_explore-libraries")
from_files <- list.files(from_dir, pattern = "\\.R$", full.names = TRUE)
to_files <- basename(from_files)
file.copy(from_files, to_files)
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
list.files()
```

    ##  [1] "00_filesystem-practice_comfy.R"       
    ##  [2] "00_filesystem-practice_jenny.R"       
    ##  [3] "00_filesystem-practice_jenny.spin.R"  
    ##  [4] "00_filesystem-practice_jenny.spin.Rmd"
    ##  [5] "00_filesystem-practice_spartan.html"  
    ##  [6] "00_filesystem-practice_spartan.R"     
    ##  [7] "01_explore-libraries_comfy.R"         
    ##  [8] "01_explore-libraries_jenny.R"         
    ##  [9] "01_explore-libraries_spartan.R"       
    ## [10] "explore-libraries.Rproj"              
    ## [11] "r_code.R"                             
    ## [12] "README.md"

``` r
## Clean it out, so we can use fs ----
file.remove(to_files)
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "00_filesystem-practice_comfy.R"       
    ## [2] "00_filesystem-practice_jenny.R"       
    ## [3] "00_filesystem-practice_jenny.spin.R"  
    ## [4] "00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "00_filesystem-practice_spartan.html"  
    ## [6] "00_filesystem-practice_spartan.R"     
    ## [7] "explore-libraries.Rproj"              
    ## [8] "README.md"

``` r
####***********************#####
## Copy again, using fs ----
library(fs)
(from_dir <- path_home("Desktop", "day1_s1_explore-libraries"))
```

    ## /Users/tma/Desktop/day1_s1_explore-libraries

``` r
(from_files <- dir_ls(from_dir, glob = "*.R"))
```

    ## /Users/tma/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R
    ## /Users/tma/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R
    ## /Users/tma/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R
    ## /Users/tma/Desktop/day1_s1_explore-libraries/r_code.R

``` r
(to_files <- path_file(from_files))
```

    ## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
    ## 01_explore-libraries_spartan.R r_code.R

``` r
(out <- file_copy(from_files, to_files))
```

    ## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
    ## 01_explore-libraries_spartan.R r_code.R

``` r
dir_ls()
```

    ## 00_filesystem-practice_comfy.R
    ## 00_filesystem-practice_jenny.R
    ## 00_filesystem-practice_jenny.spin.R
    ## 00_filesystem-practice_jenny.spin.Rmd
    ## 00_filesystem-practice_spartan.R
    ## 00_filesystem-practice_spartan.html
    ## 01_explore-libraries_comfy.R
    ## 01_explore-libraries_jenny.R
    ## 01_explore-libraries_spartan.R
    ## README.md
    ## explore-libraries.Rproj
    ## r_code.R

``` r
dir_info()
```

    ##                                     path type    size permissions
    ## 1         00_filesystem-practice_comfy.R file    2.3K   rw-r--r--
    ## 2         00_filesystem-practice_jenny.R file   1.77K   rw-r--r--
    ## 3    00_filesystem-practice_jenny.spin.R file   1.77K   rw-r--r--
    ## 4  00_filesystem-practice_jenny.spin.Rmd file   1.87K   rw-r--r--
    ## 5       00_filesystem-practice_spartan.R file     814   rw-r--r--
    ## 6    00_filesystem-practice_spartan.html file 719.51K   rw-r--r--
    ## 7           01_explore-libraries_comfy.R file   1.19K   rw-r--r--
    ## 8           01_explore-libraries_jenny.R file   1.62K   rw-r--r--
    ## 9         01_explore-libraries_spartan.R file     850   rw-r--r--
    ## 10                             README.md file      74   rw-r--r--
    ## 11               explore-libraries.Rproj file     205   rw-r--r--
    ## 12                              r_code.R file       0   rw-r--r--
    ##      modification_time user group device_id hard_links special_device_id
    ## 1  2018-01-31 13:55:17  tma staff  16777220          1                 0
    ## 2  2018-01-31 14:11:28  tma staff  16777220          1                 0
    ## 3  2018-01-31 14:11:28  tma staff  16777220          1                 0
    ## 4  2018-01-31 14:11:28  tma staff  16777220          1                 0
    ## 5  2018-01-31 13:56:21  tma staff  16777220          1                 0
    ## 6  2018-01-31 13:56:25  tma staff  16777220          1                 0
    ## 7  2018-01-31 10:56:51  tma staff  16777220          1                 0
    ## 8  2018-01-31 10:32:16  tma staff  16777220          1                 0
    ## 9  2018-01-31 09:57:12  tma staff  16777220          1                 0
    ## 10 2018-01-31 13:37:31  tma staff  16777220          1                 0
    ## 11 2018-01-31 13:31:43  tma staff  16777220          1                 0
    ## 12 2018-01-31 11:23:55  tma staff  16777220          1                 0
    ##      inode block_size blocks flags generation         access_time
    ## 1  3439490       4096      8     0          0 2018-01-31 14:08:52
    ## 2  3439642       4096      8     0          0 2018-01-31 14:11:28
    ## 3  3442099       4096      8     0          0 2018-01-31 14:11:28
    ## 4  3442100       4096      8     0          0 2018-01-31 14:11:28
    ## 5  3439501       4096      8     0          0 2018-01-31 14:08:52
    ## 6  3439631       4096   1440     0          0 2018-01-31 14:08:55
    ## 7  3442109       4096      8     0          0 2018-01-31 14:11:29
    ## 8  3442110       4096      8     0          0 2018-01-31 14:11:29
    ## 9  3442111       4096      8     0          0 2018-01-31 14:11:29
    ## 10 3439075       4096      8     0          0 2018-01-31 13:40:31
    ## 11 3439076       4096      8     0          0 2018-01-31 13:40:31
    ## 12 3442112       4096      0     0          0 2018-01-31 14:11:29
    ##            change_time          birth_time
    ## 1  2018-01-31 13:55:17 2018-01-31 13:50:31
    ## 2  2018-01-31 14:11:28 2018-01-31 13:57:11
    ## 3  2018-01-31 14:11:28 2018-01-31 14:11:28
    ## 4  2018-01-31 14:11:28 2018-01-31 14:11:28
    ## 5  2018-01-31 13:56:21 2018-01-31 13:51:05
    ## 6  2018-01-31 13:56:25 2018-01-31 13:56:24
    ## 7  2018-01-31 14:11:29 2018-01-31 10:56:51
    ## 8  2018-01-31 14:11:29 2018-01-31 10:32:16
    ## 9  2018-01-31 14:11:29 2018-01-31 09:57:12
    ## 10 2018-01-31 13:37:31 2018-01-31 13:31:42
    ## 11 2018-01-31 13:31:43 2018-01-31 13:31:42
    ## 12 2018-01-31 14:11:29 2018-01-31 11:23:55

``` r
## Sidebar: Why does Jenny name files this way? ----
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1.9000     ✔ purrr   0.2.4     
    ## ✔ tibble  1.4.2          ✔ dplyr   0.7.4     
    ## ✔ tidyr   0.7.2          ✔ stringr 1.2.0     
    ## ✔ readr   1.1.1          ✔ forcats 0.2.0

    ## Warning: package 'tibble' was built under R version 3.4.3

    ## ── Conflicts ───────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
ft <- tibble(files = dir_ls(glob = "*.R"))
ft
```

    ## # A tibble: 8 x 1
    ##   files                              
    ##   <fs::path>                         
    ## 1 00_filesystem-practice_comfy.R     
    ## 2 00_filesystem-practice_jenny.R     
    ## 3 00_filesystem-practice_jenny.spin.R
    ## 4 00_filesystem-practice_spartan.R   
    ## 5 01_explore-libraries_comfy.R       
    ## 6 01_explore-libraries_jenny.R       
    ## 7 01_explore-libraries_spartan.R     
    ## 8 r_code.R

``` r
ft %>%
  filter(str_detect(files, "explore"))
```

    ## # A tibble: 3 x 1
    ##   files                         
    ##   <fs::path>                    
    ## 1 01_explore-libraries_comfy.R  
    ## 2 01_explore-libraries_jenny.R  
    ## 3 01_explore-libraries_spartan.R

``` r
ft %>%
  mutate(files = path_ext_remove(files)) %>%
  separate(files, into = c("i", "topic", "flavor"), sep = "_")
```

    ## Warning: Too few values at 1 locations: 8

    ## # A tibble: 8 x 3
    ##   i     topic               flavor    
    ## * <chr> <chr>               <chr>     
    ## 1 00    filesystem-practice comfy     
    ## 2 00    filesystem-practice jenny     
    ## 3 00    filesystem-practice jenny.spin
    ## 4 00    filesystem-practice spartan   
    ## 5 01    explore-libraries   comfy     
    ## 6 01    explore-libraries   jenny     
    ## 7 01    explore-libraries   spartan   
    ## 8 r     code                <NA>

``` r
dirs <- dir_ls(path_home("Desktop"), type = "directory")
(dt <- tibble(dirs = path_file(dirs)))
```

    ## # A tibble: 22 x 1
    ##    dirs           
    ##    <fs::path>     
    ##  1 ART_ASCO       
    ##  2 ASCO_2018      
    ##  3 BMS            
    ##  4 Benefit_2018   
    ##  5 CCGA           
    ##  6 Compare        
    ##  7 Conference_2018
    ##  8 Personal       
    ##  9 R              
    ## 10 RShiny         
    ## # ... with 12 more rows

``` r
dt %>%
  separate(dirs, into = c("day", "session", "topic"), sep = "_")
```

    ## Warning: Too few values at 20 locations: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11,
    ## 12, 13, 14, 15, 18, 19, 20, 21, 22

    ## # A tibble: 22 x 3
    ##    day        session topic
    ##  * <chr>      <chr>   <chr>
    ##  1 ART        ASCO    <NA> 
    ##  2 ASCO       2018    <NA> 
    ##  3 BMS        <NA>    <NA> 
    ##  4 Benefit    2018    <NA> 
    ##  5 CCGA       <NA>    <NA> 
    ##  6 Compare    <NA>    <NA> 
    ##  7 Conference 2018    <NA> 
    ##  8 Personal   <NA>    <NA> 
    ##  9 R          <NA>    <NA> 
    ## 10 RShiny     <NA>    <NA> 
    ## # ... with 12 more rows

``` r
## Principled use of delimiters --> meta-data can be recovered from filename

## Clean it out, so we reset for workshop ----
file_delete(to_files)
dir_ls()
```

    ## 00_filesystem-practice_comfy.R
    ## 00_filesystem-practice_jenny.R
    ## 00_filesystem-practice_jenny.spin.R
    ## 00_filesystem-practice_jenny.spin.Rmd
    ## 00_filesystem-practice_spartan.R
    ## 00_filesystem-practice_spartan.html
    ## README.md
    ## explore-libraries.Rproj
