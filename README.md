CRAN Downloads
================

This repo contains the analysis of downloads of my `R` packages: 1.
[`healthyR`](https://www.spsanderson.com/healthyR/) 2.
[`healthyR.data`](https://www.spsanderson.com/healthyR.data/) 3.
[`healthyR.ts`](https://www.spsanderson.com/healthyR.ts/) 4.
[`healthyverse`](https://www.spsanderson.com/healthyverse/)

All of which follow the [“analyses as
package”](https://rmflight.github.io/posts/2014/07/analyses_as_packages.html)
philosophy this repo itself is an `R` package that can installed using
`remotes::install_github()`.

I have forked this project itself from
[`ggcharts-analysis`](https://github.com/thomas-neitmann/ggcharts-downloads).

While I analyze `healthyverse` packages here, the functions are written
in a way that you can analyze any CRAN package with a slight
modificaiton to the `download_log` function.

This file was last updated on June 11, 2021.

``` r
library(packagedownloads)
library(ggplot2)
library(patchwork)
```

``` r
start_date <- Sys.Date() - 9
end_date <- Sys.Date() - 2
downloads <- download_logs(start_date, end_date)
daily_downloads <- compute_daily_downloads(downloads)
downloads_by_country <- compute_downloads_by_country(downloads)

p1 <- plot_daily_downloads(daily_downloads)
p2 <- plot_cumulative_downloads(daily_downloads)
p3 <- hist_daily_downloads(daily_downloads)
p4 <- plot_downloads_by_country(downloads_by_country)

f <- function(date) format(date, "%b %d, %Y")
patchwork_theme <- theme_classic(base_size = 24) +
  theme(
    plot.title = element_text(face = "bold"),
    plot.caption = element_text(size = 14)
  )
p1 + p2 + p3 + p4 +
  plot_annotation(
    title    = "healthyR packages are on the Rise",
    subtitle = "A Summary of Downloads from the RStudio CRAN Mirror",
    caption  = glue::glue("Source: RStudio CRAN Logs ({f(start_date)} to {f(end_date)})"),
    theme    = patchwork_theme
  )
```

![](man/figures/README-analysis-1.png)<!-- -->
