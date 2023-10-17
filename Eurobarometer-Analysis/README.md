Data source: [Eurobarometer 98.2
(2023)](https://search.gesis.org/research_data/ZA7953)

## Read data

From the data source above, download the file
`ZA7953_v1-0-0_eurobarometer_98.2.dta` and extract the columns for
country names and answers to the question
`sd18a - DEMOCRACY SATISFACTION - COUNTRY` (“On the whole, are you very
satisfied, fairly satisfied, not very satisfied or not at all satisfied
with the way democracy works in (OUR COUNTRY)?”)

``` r
d = haven::read_dta("../data/raw/ZA7953_v1-0-0_eurobarometer_98.2.dta") %>% 
  select("isocntry", "sd18a") %>%
  mutate(isocntry = gsub("DE-.","DE", isocntry)) #merge east and west germany

#extract metadata
meta = data.frame(values = attributes(d$sd18a)$labels %>% unname,
             labels = attributes(d$sd18a)$labels %>% names)
```

## Summarize and clean data

The raw data contains answers from every single participant. For
analysis, summarize by country and answer. Append metadata and country
names.

``` r
#calculate numbers and shares of answers
d = d %>%
  group_by(isocntry, sd18a) %>%
  summarise(n = n(), .groups = "drop") %>% 
  mutate(share = n/sum(n)) %>% 
  left_join(meta, by = c("sd18a" = "values")) %>% #merge descriptions
  left_join(read.csv("../data/processed/eurobarometer_countrycodes.csv"), by = join_by(isocntry)) #merge country names
```

## Analyze democracy satisfaction

Make dataset of democracy satisfaction shares by country and save. Print
overall satisfaction levels.

    ## # A tibble: 5 × 4
    ##   sd18a                        labels                       n  share
    ##   <dbl+lbl>                    <chr>                    <int>  <dbl>
    ## 1 1 [Very satisfied]           Very satisfied            3878 0.103 
    ## 2 2 [Fairly satisfied]         Fairly satisfied         17508 0.463 
    ## 3 3 [Not very satisfied]       Not very satisfied       10860 0.287 
    ## 4 4 [Not at all satisfied]     Not at all satisfied      5112 0.135 
    ## 5 5 [Don't know (SPONTANEOUS)] Don't know (SPONTANEOUS)   435 0.0115
