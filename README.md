The ecologocal fallacy: Thorndike’s (1939) example
==================================================

The ecological fallacy occurs when results from group-level analyses are
wrongly extended to individuals. The fallacy is often attributed to
William S. Robinson’s ([1950](#ref-robinsonEcologicalCorrelations1950))
paper, [*Ecological correlations and the behavior of
individuals*](https://www.jstor.org/stable/2087176?origin=crossref&seq=1#page_scan_tab_contents),
and the name itself first appeared in sociologist Hanan C. Selvin’s
([1958](#ref-selvinDurkheimSuicideProblems1958)) paper, [*Durkheim’s
suicide and problems of empirical
research*](https://s3.amazonaws.com/academia.edu.documents/33024288/Durkheim-suicide_empirical-research-problems.pdf?response-content-disposition=inline%3B%20filename%3DDurkheims_Suicide_and_Problems_of_Empiri.pdf&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWOWYYGZ2Y53UL3A%2F20191014%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20191014T151247Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=4e9eeb342fa0332cd0f7ed00a4769661cb7c6921e07dd19a763595f037d35dae).
However, my fellow psychologists might be happy to learn the idea goes
back at least as far as E. L. Thorndike’s
([1939](#ref-thorndikeFallacyImputingCorrelations1939)) paper, [*On the
fallacy of imputing the correlations found for groups to the individuals
or smaller groups composing
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
[tribble](https://tibble.tidyverse.org/reference/tribble.html)s (see
Müller & Wickham, [2020](#ref-R-tibble); also Wickham,
[2019](#ref-R-tidyverse); Wickham et al.,
[2019](#ref-wickhamWelcomeTidyverse2019)).

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
  scale_fill_viridis_c(expression(italic(n)), option = "C", limits = c(0, NA)) +
  scale_color_manual(values = c("black", "white")) +
  scale_x_continuous(breaks = -4:4, position = "top") +
  scale_y_continuous(breaks = -4:4, trans = "reverse") +
  theme(panel.grid = element_blank()) +
  facet_wrap(~table, ncol = 2, labeller = label_both)
```

<img src="README_files/figure-markdown_github/unnamed-chunk-4-1.png" width="768" />

Thorndike asserted that “within each of the districts the correlation
between A and B is zero” (p. 124). Let’s check.

``` r
t13 %>% 
  uncount(n) %>% 
  group_by(t) %>% 
  summarise(r = cor(a, b))
```

    ## # A tibble: 12 x 2
    ##        t     r
    ##    <dbl> <dbl>
    ##  1     1     0
    ##  2     2     0
    ##  3     3     0
    ##  4     4     0
    ##  5     5     0
    ##  6     6     0
    ##  7     7     0
    ##  8     8     0
    ##  9     9     0
    ## 10    10     0
    ## 11    11     0
    ## 12    12     0

Yep. Those correlations are zero for each. Here’s what the data look
like if you naïvely combine the numbers from all districts.

``` r
t13 %>% 
  uncount(n) %>% 
  group_by(a, b) %>% 
  count() %>% 
  
  ggplot(aes(x = a, y = b)) +
  geom_tile(aes(fill = n)) +
  geom_text(aes(label = n, color = n < 20),
            show.legend = F) +
  scale_fill_viridis_c(expression(italic(n)), option = "C", limits = c(0, NA)) +
  scale_color_manual(values = c("black", "white")) +
  scale_x_continuous(breaks = -4:5, position = "top") +
  scale_y_continuous(breaks = -4:5, trans = "reverse") +
  theme(panel.grid = element_blank())
```

<img src="README_files/figure-markdown_github/unnamed-chunk-6-1.png" width="576" />

This corresponds to Thorndike’s Table XIII. If you look closely at his
original, you’ll see he miscounted a few cells. No worry–the overall
findings are still sound. Here’s the bivariate correlation for the
naïvely combined data.

``` r
t13 %>% 
  uncount(n) %>% 
  summarise(r = cor(a, b))
```

    ## # A tibble: 1 x 1
    ##       r
    ##   <dbl>
    ## 1 0.454

But what if we look at aggregated data? To do so, we’ll take the mean of
`a` and `b` from each of the districts. Here’s what that plot might look
like.

``` r
t13 %>%
  uncount(n) %>% 
  group_by(t) %>% 
  summarise(a = mean(a),
            b = mean(b)) %>% 
  count(a, b) %>% 
  
  ggplot(aes(x = a, y = b)) +
  geom_tile(aes(fill = n)) +
  geom_text(aes(label = n, color = n < 2),
            show.legend = F) +
  scale_fill_viridis_c(expression(italic(n)), option = "C", breaks = 1:2) +
  scale_color_manual(values = c("black", "white")) +
  scale_x_continuous(breaks = -4:5, position = "top") +
  scale_y_continuous(breaks = -4:5, trans = "reverse") +
  theme(panel.grid = element_blank())
```

<img src="README_files/figure-markdown_github/unnamed-chunk-8-1.png" width="576" />

That plot corresponds directly to Thorndike’s Table XIV. Here’s the
correlation.

``` r
t13 %>%
  uncount(n) %>% 
  group_by(t) %>% 
  summarise(mu_a = mean(a),
            mu_b = mean(b)) %>% 
  summarise(r = cor(mu_a, mu_b))
```

    ## # A tibble: 1 x 1
    ##       r
    ##   <dbl>
    ## 1 0.914

To recap, within each district the correlation is exactly 0. When we
naïvely combine all the data, the correlation is about .45. When we
aggregate the data, the correlation goes to .91. We might as well finish
right where we started.

> If the correlation between two traits, A and B (say, poverty and
> delinquency), in *n* groups (say, the residents of *w* districts) has
> a certain value, K, the correlation between A and B in the individuals
> or the families composing the groups need not be K and will not be,
> save in very special circumstances. (p. 122)

That is, the results from group-level data will not necessarily
correspond to the results of subgroup- or individual-level data. Proceed
with caution. To learn more about this phenomena, see the
([2012](#ref-hamakerWhyResearchersShould2012)) chapter by Hamaker or the
paper by Kievit et al.
([2013](#ref-kievitSimpsonParadoxPsychological2013)).

Session info
------------

``` r
sessionInfo()
```

    ## R version 3.6.3 (2020-02-29)
    ## Platform: x86_64-apple-darwin15.6.0 (64-bit)
    ## Running under: macOS Catalina 10.15.3
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
    ## [1] forcats_0.5.0   stringr_1.4.0   dplyr_1.0.1     purrr_0.3.4    
    ## [5] readr_1.3.1     tidyr_1.1.1     tibble_3.0.3    ggplot2_3.3.2  
    ## [9] tidyverse_1.3.0
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] tidyselect_1.1.0  xfun_0.13         haven_2.2.0       lattice_0.20-38  
    ##  [5] colorspace_1.4-1  vctrs_0.3.4       generics_0.0.2    htmltools_0.5.0  
    ##  [9] viridisLite_0.3.0 yaml_2.2.1        utf8_1.1.4        rlang_0.4.7      
    ## [13] pillar_1.4.6      glue_1.4.2        withr_2.2.0       DBI_1.1.0        
    ## [17] dbplyr_1.4.2      modelr_0.1.6      readxl_1.3.1      lifecycle_0.2.0  
    ## [21] munsell_0.5.0     gtable_0.3.0      cellranger_1.1.0  rvest_0.3.5      
    ## [25] evaluate_0.14     labeling_0.3      knitr_1.28        fansi_0.4.1      
    ## [29] broom_0.5.5       Rcpp_1.0.5        scales_1.1.1      backports_1.1.9  
    ## [33] jsonlite_1.7.0    farver_2.0.3      fs_1.4.1          hms_0.5.3        
    ## [37] digest_0.6.25     stringi_1.4.6     grid_3.6.3        cli_2.0.2        
    ## [41] tools_3.6.3       magrittr_1.5      crayon_1.3.4      pkgconfig_2.0.3  
    ## [45] ellipsis_0.3.1    xml2_1.3.1        reprex_0.3.0      lubridate_1.7.8  
    ## [49] assertthat_0.2.1  rmarkdown_2.1     httr_1.4.1        rstudioapi_0.11  
    ## [53] R6_2.4.1          nlme_3.1-144      compiler_3.6.3

References
----------

Hamaker, E. L. (2012). Why researchers should think "within-person": A
paradigmatic rationale. In *Handbook of research methods for studying
daily life* (pp. 43–61). The Guilford Press.
<https://www.guilford.com/books/Handbook-of-Research-Methods-for-Studying-Daily-Life/Mehl-Conner/9781462513055>

Kievit, R., Frankenhuis, W. E., Waldorp, L., & Borsboom, D. (2013).
Simpson’s paradox in psychological science: A practical guide.
*Frontiers in Psychology*, *4*.
<https://doi.org/10.3389/fpsyg.2013.00513>

Müller, K., & Wickham, H. (2020). *tibble: Simple data frames*.
<https://CRAN.R-project.org/package=tibble>

Robinson, W. S. (1950). Ecological correlations and the behavior of
individuals. *American Sociological Review*, *15*(3).
<https://doi.org/10.2307/2087176>

Selvin, H. C. (1958). Durkheim’s suicide and problems of empirical
research. *American Journal of Sociology*, *63*(6), 607–619.
<https://doi.org/10.1086/222356>

Thorndike, E. L. (1939). On the fallacy of imputing the correlations
found for groups to the individuals or smaller groups composing them.
*The American Journal of Psychology*, *52*(1), 122–124.
<https://doi.org/10.2307/1416673>

Wickham, H. (2019). *tidyverse: Easily install and load the
’tidyverse’*. <https://CRAN.R-project.org/package=tidyverse>

Wickham, H., Averick, M., Bryan, J., Chang, W., McGowan, L. D.,
François, R., Grolemund, G., Hayes, A., Henry, L., Hester, J., Kuhn, M.,
Pedersen, T. L., Miller, E., Bache, S. M., Müller, K., Ooms, J.,
Robinson, D., Seidel, D. P., Spinu, V., … Yutani, H. (2019). Welcome to
the tidyverse. *Journal of Open Source Software*, *4*(43), 1686.
<https://doi.org/10.21105/joss.01686>
