
# ropendata

Query and Download ‘Rapid7’ Cybersecurity Data Sets

## Description

‘Rapid7’ collects cybersecurity data and makes it available via their
‘Open Data’ <https://opendata.rapid7.com> portal which has an ‘API’.
Tools are provided to assist in querying for available data sets and
downloading any data set authorized to a registered account.

## More Info

You will need to request a free account on Open Data via
<https://opendata.rapid7.com/#register> and then navigate to the “Open
Data API” link there to create both an organizational key and a user
key. You can only use **user keys** with the Open Data API and you will
receive error messages indicating so if you try to use an organizational
key.

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
devtools::install_github("brudis-r7/ropendata")
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
studies <- list_studies()

studies
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

``` r
glimpse(studies)
```

    ## Observations: 14
    ## Variables: 15
    ## $ uniqid               <chr> "sonar.national_exposure", "heisenberg.cowrie", "sonar.atg_10001_tcp", "sonar.http", "...
    ## $ name                 <chr> "National Exposure TCP SYN Scans", "Rapid7 Heisenberg Cloud Honeypot cowrie Logs", "AT...
    ## $ short_desc           <chr> "Open port results for Rapid7's National Exposure reports", "Rapid7 Heisenberg Cloud H...
    ## $ long_desc            <chr> "The dataset represents the raw data collected that was used in the production of Rapi...
    ## $ study_url            <chr> "https://github.com/rapid7/data/tree/master/national-exposure", "https://www.rapid7.co...
    ## $ study_name           <chr> "National Exposure Scans", "Rapid7 Heisenberg Cloud Honeypot cowrie Logs", "ATG 10001/...
    ## $ study_venue          <chr> "Project Sonar", "Rapid7 Heisenberg Cloud Honeypot", "Project Sonar", "Project Sonar",...
    ## $ study_bibtext        <chr> "", "", "", "", "", "", "", "", "", "", "", "", "", ""
    ## $ contact_name         <chr> "Rapid7 Labs", "Rapid7 Labs", "Rapid7 Labs", "Rapid7 Labs", "Rapid7 Labs", "Rapid7 Lab...
    ## $ contact_email        <chr> "research@rapid7.com", "research@rapid7.com", "research@rapid7.com", "research@rapid7....
    ## $ organization_name    <chr> "Rapid7", "Rapid7", "Rapid7", "Rapid7", "Rapid7", "Rapid7", "Rapid7", "Rapid7", "Rapid...
    ## $ organization_website <chr> "https://github.com/rapid7/data/tree/master/national-exposure", "http://www.rapid7.com...
    ## $ created_at           <chr> "2018-06-12", "2018-05-15", "2018-05-15", "2018-06-19", "2018-06-07", "2018-06-20", "2...
    ## $ updated_at           <chr> "2017-06-13", "2016-12-01", "2017-04-07", "2018-03-12", "2018-03-14", "2018-03-21", "2...
    ## $ sonarfile_set        <list> [<"2018-04-11-1523483529-nei_2018-udp_sip_5060.csv.gz", "2018-04-02-1522680455-nei_20...

### Get Study Details

``` r
glimpse(
  get_study_details("sonar.national_exposure")
)
```

    ## Observations: 1
    ## Variables: 15
    ## $ uniqid               <chr> "sonar.national_exposure"
    ## $ name                 <chr> "National Exposure TCP SYN Scans"
    ## $ short_desc           <chr> "Open port results for Rapid7's National Exposure reports"
    ## $ long_desc            <chr> "The dataset represents the raw data collected that was used in the production of Rapi...
    ## $ study_url            <chr> "https://github.com/rapid7/data/tree/master/national-exposure"
    ## $ study_name           <chr> "National Exposure Scans"
    ## $ study_venue          <chr> "Project Sonar"
    ## $ study_bibtext        <chr> ""
    ## $ contact_name         <chr> "Rapid7 Labs"
    ## $ contact_email        <chr> "research@rapid7.com"
    ## $ organization_name    <chr> "Rapid7"
    ## $ organization_website <chr> "https://github.com/rapid7/data/tree/master/national-exposure"
    ## $ created_at           <chr> "2018-06-12"
    ## $ updated_at           <chr> "2017-06-13"
    ## $ fileset              <list> [<"2018-04-11-1523483529-nei_2018-udp_sip_5060.csv.gz", "2018-04-02-1522680455-nei_20...

### Get Details About A Single Study File

``` r
glimpse(
  get_file_details("sonar.fdns_v2", "2018-06-15-1529049662-fdns_aaaa.json.gz")
)
```

    ## Observations: 1
    ## Variables: 4
    ## $ name        <chr> "2018-06-15-1529049662-fdns_aaaa.json.gz"
    ## $ fingerprint <chr> "9056f555bed59640ee5ffeadbeac8175e5873712"
    ## $ size        <int> 570536141
    ## $ updated_at  <chr> "2018-06-17"
