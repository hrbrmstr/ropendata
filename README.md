
# ropendata

Query and Download ‘Rapid7’ Cybersecurity Data Sets

## Description

‘Rapid7’ collects cybersecurity data and makes it available via their
‘Open Data’ <https://opendata.rapid7.com> portal which has an ‘API’.
Tools are provided to assist in querying for available data sets and
downloading any data set authorized to a registered account.

## What’s Inside The Tin

The following functions are implemented:

  - `get_file_details`: Retrieve details for a given file from a
    specific Rapid7 Open Data study
  - `get_study_details`: Retrieve details for a specific Rapid7 Open
    Data study
  - `list_studies`: List available Rapid7 Cybersecurity Studies
  - `rapid7_api_key`: Get or set `RAPID7_OPENDATA_API_KEY` value

## Installation

``` r
devtools::install_github("brudis-47/ropendata")
```

## Usage

``` r
library(ropendata)
library(tidyverse)

# current verison
packageVersion("ropendata")
```

    ## [1] '0.1.0'

### List Studies

``` r
list_studies()
```

    ## # A tibble: 14 x 15
    ##    uniqid  name   short_desc   long_desc      study_url study_name study_venue study_bibtext contact_name contact_email
    ##  * <chr>   <chr>  <chr>        <chr>          <chr>     <chr>      <chr>       <chr>         <chr>        <chr>        
    ##  1 sonar.… Natio… Open port r… The dataset r… https://… National … Project So… ""            Rapid7 Labs  research@rap…
    ##  2 heisen… Rapid… Rapid7 Heis… This is an ex… https://… Rapid7 He… Rapid7 Hei… ""            Rapid7 Labs  research@rap…
    ##  3 sonar.… ATG 1… Project Son… The datasets … https://… ATG 10001… Project So… ""            Rapid7 Labs  research@rap…
    ##  4 sonar.… HTTP … Project Son… Ths dataset c… https://… HTTP GET … Project So… ""            Rapid7 Labs  research@rap…
    ##  5 sonar.… SSL C… Project Son… The dataset c… https://… Project S… Project So… ""            Rapid7 Labs  research@rap…
    ##  6 sonar.… TCP S… Project Son… The dataset c… https://… TCP Scans  Project So… ""            Rapid7 Labs  research@rap…
    ##  7 sonar.… More … Project Son… The dataset c… https://… Project S… ""          ""            Rapid7 Labs  research@rap…
    ##  8 sonar.… Rever… DNS IPv4 PT… This dataset … https://… Reverse D… Project So… ""            Rapid7 Labs  research@rap…
    ##  9 sonar.… UDP S… Project Son… The dataset c… https://… UDP Scans  Project So… ""            Rapid7 Labs  research@rap…
    ## 10 sonar.… Criti… The Critica… The current d… http://w… Global Vu… RSA Securi… ""            Rapid7 Labs  research@rap…
    ## 11 sonar.… HTTPS… Project Son… This study pe… https://… HTTPS GET… Project So… ""            Rapid7 Labs  research@rap…
    ## 12 sonar.… Forwa… DNS 'ANY' r… This dataset … https://… Forward D… Project So… ""            Rapid7 Labs  research@rap…
    ## 13 sonar.… Rever… DNS IPv4 PT… This dataset … https://… Reverse D… Project So… ""            Rapid7 Labs  research@rap…
    ## 14 sonar.… Forwa… DNS 'ANY', … This dataset … https://… Forward D… Project So… ""            Rapid7 Labs  research@rap…
    ## # ... with 5 more variables: organization_name <chr>, organization_website <chr>, created_at <chr>, updated_at <chr>,
    ## #   sonarfile_set <list>

### Get Study Details

``` r
get_study_details("sonar.national_exposure")
```

    ## # A tibble: 1 x 15
    ##   uniqid  name   short_desc  long_desc       study_url  study_name study_venue study_bibtext contact_name contact_email
    ##   <chr>   <chr>  <chr>       <chr>           <chr>      <chr>      <chr>       <chr>         <chr>        <chr>        
    ## 1 sonar.… Natio… Open port … The dataset re… https://g… National … Project So… ""            Rapid7 Labs  research@rap…
    ## # ... with 5 more variables: organization_name <chr>, organization_website <chr>, created_at <chr>, updated_at <chr>,
    ## #   fileset <list>

### Get Details About A Single Study File

``` r
get_file_details("sonar.fdns_v2", "2018-06-15-1529049662-fdns_aaaa.json.gz")
```

    ## # A tibble: 1 x 4
    ##   name                                    fingerprint                                   size updated_at
    ##   <chr>                                   <chr>                                        <int> <chr>     
    ## 1 2018-06-15-1529049662-fdns_aaaa.json.gz 9056f555bed59640ee5ffeadbeac8175e5873712 570536141 2018-06-17
