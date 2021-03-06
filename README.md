
<!-- README.md is generated from README.Rmd. Please edit that file -->

# underground

London Underground performance data is published in spreadsheets. This R
package makes it available in [csv
files](https://github.com/nacnudus/underground/tree/master/inst/extdata),
or in an R data frame.

The secret sauce is [tidyxl](https://nacnudus.github.io/tidyxl) with a
dash of [unpivotr](https://nacnudus.github.io/unpivotr).

## Installation

``` r
devtools::install_github("nacnudus/underground")
```

## Example

``` r
library(underground)
library(dplyr)
library(ggplot2)

underground %>%
  filter(metric == "Train delays longer than 15 minutes",
         year == "2016/17",
         is.na(fourweek),
         is.na(quarter),
         line != "All Lines") %>%
  mutate(fill= underground_colours[line]) %>%
  select(line, value, fill) %>%
  ggplot(aes(line, value, fill = fill)) +
  geom_bar(stat = "identity") +
  scale_fill_identity("", labels = underground_lines, guide = "legend") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  xlab("") +
  ylab("") +
  ggtitle("Train delays longer than 15 minutes (2016/17)")
```

<img src="man/figures/README-unnamed-chunk-1-1.png" width="100%" />
