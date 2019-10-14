The ecologocal fallacy: Thorndike’s (1939) example
==================================================

The ecological fallacy occurs when results from group-level analyses are
wrongly extended to individuals. The fallacy is often attributed to
William S. Robinson’s (1950) paper [*Ecological Correlations and the
Behavior of
Individuals*](https://www.jstor.org/stable/2087176?origin=crossref&seq=1#page_scan_tab_contents)
and the name itself first appeared in sociologist Hanan C. Selvin’s
(1958) paper, [*Durkheim’s suicide and problems of empirical
research*](https://s3.amazonaws.com/academia.edu.documents/33024288/Durkheim-suicide_empirical-research-problems.pdf?response-content-disposition=inline%3B%20filename%3DDurkheims_Suicide_and_Problems_of_Empiri.pdf&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWOWYYGZ2Y53UL3A%2F20191014%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20191014T151247Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=4e9eeb342fa0332cd0f7ed00a4769661cb7c6921e07dd19a763595f037d35dae).
However, my fellow psychologists might be happy to learn the idea goes
back at least as far as E. L. Thorndike’s (1939) paper, [*On the fallacy
of imputing the correlations found for groups to the individuals or
smaller groups composing
them*](https://www.jstor.org/stable/1416673?seq=1#page_scan_tab_contents).
The purpose of this project is to walk out Thorndike’s original
examples.

Here’s how Thorndike began his paper:

> If the correlation between two traits, A and B (say, poverty and
> delinquency), in *n* groups (say, the residents of *w* districts) has
> a certain value, K, the correlation between A and B in the individuals
> or the families composing the groups need not be K and will not be,
> save in very special circumstances. (p. 122)

Thorndike referred to an example of this mistake from the literature of
his time, which we won’t get into, here. He then worked through the
fallacy with 12 simulated data sets. We’ll cover those in detail. In
each of his synthetic data sets, “A is supposed to be intelligence
quotient and B is supposed to be the fraction of a room or number of
rooms per person” (p. 124). That is, he was covering the correlation
between IQ and the crowdedness of one’s living conditions.

Here we’ll copy down the data into a series of
[tribble](https://tibble.tidyverse.org/reference/tribble.html)s.

``` r
library(tidyverse)

# table I
t1 <-
  tribble(
  ~a, ~b, ~n,
  -1, -3, 1,
  0, -3, 1,
  1, -3, 1,
  
  -3, -2, 1,
  -2, -2, 1,
  -1, -2, 4,
  0, -2, 6,
  1, -2, 4,
  2, -2, 1,
  3, -2, 1,
  
  -4, -1, 1,
  -3, -1, 2,
  -2, -1, 4,
  -1, -1, 7,
  0, -1, 15,
  1, -1, 7,
  2, -1, 4,
  3, -1, 2,
  4, -1, 1,
  
  -4, 0, 2,
  -3, 0, 2,
  -2, 0, 6,
  -1, 0, 8,
  0, 0, 20,
  1, 0, 8,
  2, 0, 6,
  3, 0, 2,
  4, 0, 2,
  
  -4, 1, 1,
  -3, 1, 2,
  -2, 1, 4,
  -1, 1, 7,
  0, 1, 15,
  1, 1, 7,
  2, 1, 4,
  3, 1, 2,
  4, 1, 1,
  
  -3, 2, 1,
  -2, 2, 1,
  -1, 2, 4,
  0, 2, 6,
  1, 2, 4,
  2, 2, 1,
  3, 2, 1,
  
  -1, 3, 1,
  0, 3, 1,
  1, 3, 1
) 

# table II

t2 <-
  tribble(
  ~a, ~b, ~n,
  -2, -3, 1,
  -1, -3, 1,
  0, -3, 1,
  1, -3, 1,
  
  -3, -2, 1,
  -2, -2, 2,
  -1, -2, 4,
  0, -2, 4,
  1, -2, 2,
  2, -2, 1,
  
  -3, -1, 1,
  -2, -1, 3,
  -1, -1, 6,
  0, -1, 6,
  1, -1, 3,
  2, -1, 1,
  
  -3, 0, 1,
  -2, 0, 2,
  -1, 0, 4,
  0, 0, 4,
  1, 0, 2,
  2, 0, 1,
  
  -2, 1, 1,
  -1, 1, 1,
  0, 1, 1,
  1, 1, 1,
) 

# table III

t3 <-
  tribble(
  ~a, ~b, ~n,
  -1, -2, 1,
  0, -2, 1,
  1, -2, 1,
  2, -2, 1,
  
  -3, -1, 1,
  -2, -1, 1,
  -1, -1, 2,
  0, -1, 5,
  1, -1, 5,
  2, -1, 2,
  3, -1, 1,
  
  -3, 0, 1,
  -2, 0, 3,
  -1, 0, 5,
  0, 0, 10,
  1, 0, 10,
  2, 0, 5,
  3, 0, 3,
  4, 0, 2,
  
  -3, 1, 1,
  -2, 1, 3,
  -1, 1, 5,
  0, 1, 10,
  1, 1, 10,
  2, 1, 5,
  3, 1, 3,
  4, 1, 2,
  
  -3, 2, 1,
  -2, 2, 1,
  -1, 2, 2,
  0, 2, 5,
  1, 2, 5,
  2, 2, 2,
  3, 2, 1,
  
  -1, 3, 1,
  0, 3, 1,
  1, 3, 1,
  2, 3, 1
) 

# table IV

t4 <-
  tribble(
  ~a, ~b, ~n,
  -3, -3, 1,
  -2, -3, 1,
  -1, -3, 1,
  0, -3, 1,
  
  -4, -2, 1,
  -3, -2, 2,
  -2, -2, 4,
  -1, -2, 4,
  0, -2, 2,
  1, -2, 1,
  
  -4, -1, 1,
  -3, -1, 3,
  -2, -1, 6,
  -1, -1, 6,
  0, -1, 3,
  1, -1, 1,
  
  -4, 0, 1,
  -3, 0, 2,
  -2, 0, 4,
  -1, 0, 4,
  0, 0, 2,
  1, 0, 1,
  
  -3, 1, 1,
  -2, 1, 1,
  -1, 1, 1,
  0, 1, 1,
) 

# table V

t5 <-
  tribble(
  ~a, ~b, ~n,
  -3, -4, 1,
  -2, -4, 1,
  -1, -4, 1,
  
  -4, -3, 1,
  -3, -3, 2,
  -2, -3, 4,
  -1, -3, 2,
  0, -3, 1,
  
  -4, -2, 1,
  -3, -2, 3,
  -2, -2, 6,
  -1, -2, 3,
  0, -2, 1,
  
  -4, -1, 1,
  -3, -1, 2,
  -2, -1, 4,
  -1, -1, 2,
  0, -1, 1,
  
  -3, 0, 1,
  -2, 0, 1,
  -1, 0, 1
) 

# table VI

t6 <-
  tribble(
  ~a, ~b, ~n,
  -2, -4, 1,
  -1, -4, 1,
  0, -4, 1,
  
  -3, -3, 1,
  -2, -3, 2,
  -1, -3, 4,
  0, -3, 2,
  1, -3, 1,
  
  -3, -2, 1,
  -2, -2, 3,
  -1, -2, 6,
  0, -2, 3,
  1, -2, 1,
  
  -3, -1, 1,
  -2, -1, 2,
  -1, -1, 4,
  0, -1, 2,
  1, -1, 1,
  
  -2, 0, 1,
  -1, 0, 1,
  0, 0, 1
) 

# table VII

t7 <-
  tribble(
  ~a, ~b, ~n,
  -2, -3, 1,
  -1, -3, 1,
  0, -3, 1,
  
  -3, -2, 1,
  -2, -2, 2,
  -1, -2, 4,
  0, -2, 2,
  1, -2, 1,
  
  -3, -1, 1,
  -2, -1, 3,
  -1, -1, 6,
  0, -1, 3,
  1, -1, 1,
  
  -3, 0, 1,
  -2, 0, 2,
  -1, 0, 4,
  0, 0, 2,
  1, 0, 1,
  
  -2, 1, 1,
  -1, 1, 1,
  0, 1, 1
) 

# table VIII

t8 <-
  tribble(
  ~a, ~b, ~n,
  -1, -4, 1,
  0, -4, 1,
  1, -4, 1,
  
  -2, -3, 1,
  -1, -3, 2,
  0, -3, 4,
  1, -3, 2,
  2, -3, 1,
  
  -2, -2, 1,
  -1, -2, 3,
  0, -2, 6,
  1, -2, 3,
  2, -2, 1,
  
  -2, -1, 1,
  -1, -1, 2,
  0, -1, 4,
  1, -1, 2,
  2, -1, 1,
  
  -1, 0, 1,
  0, 0, 1,
  1, 0, 1
) 

# table IX

t9 <-
  tribble(
  ~a, ~b, ~n,
  -1, -2, 1,
  0, -2, 1,
  1, -2, 1,
  
  -2, -1, 1,
  -1, -1, 2,
  0, -1, 4,
  1, -1, 2,
  2, -1, 1,
  
  -2, 0, 1,
  -1, 0, 3,
  0, 0, 6,
  1, 0, 3,
  2, 0, 1,
  
  -2, 1, 1,
  -1, 1, 2,
  0, 1, 4,
  1, 1, 2,
  2, 1, 1,
  
  -1, 2, 1,
  0, 2, 1,
  1, 2, 1
) 

# table X

t10 <-
  tribble(
  ~a, ~b, ~n,
  0, -1, 1,
  1, -1, 1,
  2, -1, 1,
  
  -1, 0, 1,
  0, 0, 2,
  1, 0, 4,
  2, 0, 2,
  3, 0, 1,
  
  -1, 1, 1,
  0, 1, 3,
  1, 1, 6,
  2, 1, 3,
  3, 1, 1,
  
  -1, 2, 1,
  0, 2, 2,
  1, 2, 4,
  2, 2, 2,
  3, 2, 1,
  
  0, 3, 1,
  1, 3, 1,
  2, 3, 1
) 

# table XI

t11 <-
  tribble(
  ~a, ~b, ~n,
  1, 0, 1,
  2, 0, 1,
  3, 0, 1,
  
  0, 1, 1,
  1, 1, 2,
  2, 1, 4,
  3, 1, 2,
  4, 1, 1,
  
  0, 2, 1,
  1, 2, 3,
  2, 2, 6,
  3, 2, 3,
  4, 2, 1,
  
  0, 3, 1,
  1, 3, 2,
  2, 3, 4,
  3, 3, 2,
  4, 3, 1,
  
  1, 4, 1,
  2, 4, 1,
  3, 4, 1
) 

# table XII

t12 <-
  tribble(
  ~a, ~b, ~n,
  2, 1, 1,
  3, 1, 1,
  4, 1, 1,
  
  1, 2, 1,
  2, 2, 2,
  3, 2, 4,
  4, 2, 2,
  5, 2, 1,
  
  1, 3, 1,
  2, 3, 3,
  3, 3, 6,
  4, 3, 3,
  5, 3, 1,
  
  1, 4, 1,
  2, 4, 2,
  3, 4, 4,
  4, 4, 2,
  5, 4, 1,
  
  2, 5, 1,
  3, 5, 1,
  4, 5, 1
) 
```

We’ll combine them, here.

``` r
t13 <-
  bind_rows(
  t1  %>% mutate(t = 1),
  t2  %>% mutate(t = 2),
  t3  %>% mutate(t = 3),
  t4  %>% mutate(t = 4),
  t5  %>% mutate(t = 5),
  t6  %>% mutate(t = 6),
  t7  %>% mutate(t = 7),
  t8  %>% mutate(t = 8),
  t9  %>% mutate(t = 9),
  t10 %>% mutate(t = 10),
  t11 %>% mutate(t = 11),
  t12 %>% mutate(t = 12)
) 
```

In Thorndike’s example, the data from each of his 12 tables corresponded
to “scores for sample persons in each of twelve districts into which a
city is divided” (p. 124). For simplicity, he gave the values in a
standardized (i.e., *z*-score) metric. Here’s a plot of all those data,
disaggregated by district. It corresponds directly to the way Thorndike
presented the tables in his article.

``` r
t13 %>% 
  mutate(table = t) %>% 
  
  ggplot(aes(x = a, y = b)) +
  geom_tile(aes(fill = n)) +
  geom_text(aes(label = n, color = n < 11),
            show.legend = F) +
  scale_fill_viridis_c(option = "C") +
  scale_color_manual(values = c("black", "white")) +
  scale_x_continuous(breaks = -4:4, position = "top") +
  scale_y_continuous(breaks = -4:4, trans = "reverse") +
  theme(panel.grid = element_blank()) +
  facet_wrap(~table, ncol = 2, labeller = label_both)
```

![](README_files/figure-markdown_github/unnamed-chunk-3-1.png)

Session info
------------

``` r
sessionInfo()
```

    ## R version 3.6.0 (2019-04-26)
    ## Platform: x86_64-apple-darwin15.6.0 (64-bit)
    ## Running under: macOS High Sierra 10.13.6
    ## 
    ## Matrix products: default
    ## BLAS:   /Library/Frameworks/R.framework/Versions/3.6/Resources/lib/libRblas.0.dylib
    ## LAPACK: /Library/Frameworks/R.framework/Versions/3.6/Resources/lib/libRlapack.dylib
    ## 
    ## locale:
    ## [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8
    ## 
    ## attached base packages:
    ## [1] stats     graphics  grDevices utils     datasets  methods   base     
    ## 
    ## other attached packages:
    ## [1] forcats_0.4.0   stringr_1.4.0   dplyr_0.8.3     purrr_0.3.2    
    ## [5] readr_1.3.1     tidyr_1.0.0     tibble_2.1.3    ggplot2_3.2.1  
    ## [9] tidyverse_1.2.1
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] Rcpp_1.0.2        cellranger_1.1.0  pillar_1.4.2     
    ##  [4] compiler_3.6.0    tools_3.6.0       zeallot_0.1.0    
    ##  [7] digest_0.6.21     viridisLite_0.3.0 lubridate_1.7.4  
    ## [10] jsonlite_1.6      evaluate_0.14     lifecycle_0.1.0  
    ## [13] nlme_3.1-139      gtable_0.3.0      lattice_0.20-38  
    ## [16] pkgconfig_2.0.3   rlang_0.4.0       cli_1.1.0        
    ## [19] rstudioapi_0.10   yaml_2.2.0        haven_2.1.0      
    ## [22] xfun_0.10         withr_2.1.2       xml2_1.2.0       
    ## [25] httr_1.4.0        knitr_1.23        hms_0.4.2        
    ## [28] generics_0.0.2    vctrs_0.2.0       grid_3.6.0       
    ## [31] tidyselect_0.2.5  glue_1.3.1        R6_2.4.0         
    ## [34] readxl_1.3.1      rmarkdown_1.13    modelr_0.1.4     
    ## [37] magrittr_1.5      backports_1.1.5   scales_1.0.0     
    ## [40] htmltools_0.4.0   rvest_0.3.4       assertthat_0.2.1 
    ## [43] colorspace_1.4-1  labeling_0.3      stringi_1.4.3    
    ## [46] lazyeval_0.2.2    munsell_0.5.0     broom_0.5.2      
    ## [49] crayon_1.3.4
