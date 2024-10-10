Data Wrangling II
================

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"
drug_use_html = read_html(url)

drug_use_html
```

    ## {html_document}
    ## <html lang="en">
    ## [1] <head>\n<link rel="P3Pv1" href="http://www.samhsa.gov/w3c/p3p.xml">\n<tit ...
    ## [2] <body>\r\n\r\n<noscript>\r\n<p>Your browser's Javascript is off. Hyperlin ...

``` r
marji_use_df = 
  drug_use_html |>
  html_table() |>
  first() |> #see that this first table: first row is note. want to delete
  slice(-1) #select rows by number. Subtract first row
```

Read in cost of living data.

``` r
nyc_living_df = 
  read_html("https://www.bestplaces.net/cost_of_living/city/new_york/new_york") |>
  html_table(header = TRUE) |> #say that the first row is header
  first() #see that this first table: first row is note. want to delete. "?first" in console to see more options

nyc_living_df
```

    ## # A tibble: 8 × 4
    ##   Categories       `New York` `New York` `United States`
    ##   <chr>            <chr>      <chr>      <chr>          
    ## 1 Overall          172.5      121.5      100.0          
    ## 2 Grocery          116.6      103.8      100            
    ## 3 Health           127.6      120.7      100.0          
    ## 4 Housing          224.3      127.9      100.0          
    ## 5 Median Home Cost $677,200   $413,600   $338,100       
    ## 6 Utilities        150.5%     115.9%     100.0%         
    ## 7 Transportation   181.1      140.7      100.0          
    ## 8 Miscellaneous    136.4      121.8      100.0
