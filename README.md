# The ecologocal fallacy: Thorndike's (1939) example

The ecological fallacy occurs when results from group-level analyses are wrongly extended to individuals. The fallacy is often attributed to William S. Robinson's (1950) paper [*Ecological Correlations and the Behavior of Individuals*](https://www.jstor.org/stable/2087176?origin=crossref&seq=1#page_scan_tab_contents) and the name itself first appeared in sociologist Hanan C. Selvin's (1958) paper, [*Durkheim's suicide and problems of empirical research*](https://s3.amazonaws.com/academia.edu.documents/33024288/Durkheim-suicide_empirical-research-problems.pdf?response-content-disposition=inline%3B%20filename%3DDurkheims_Suicide_and_Problems_of_Empiri.pdf&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWOWYYGZ2Y53UL3A%2F20191014%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20191014T151247Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=4e9eeb342fa0332cd0f7ed00a4769661cb7c6921e07dd19a763595f037d35dae). However, my fellow psychologists might be happy to learn the idea goes back at least as far as E. L. Thorndike's (1939) paper, [*On the fallacy of imputing the correlations found for groups to the individuals or smaller groups composing them*](https://www.jstor.org/stable/1416673?seq=1#page_scan_tab_contents). The purpose of this project is to walk out Thorndike's original examples.

Here's how Thorndike began his paper:

> If the correlation between two traits, A and B (say, poverty and delinquency), in $n$ groups (say, the residents of $w$ districts) has a certain value, K, the correlation between A and B in the individuals or the families composing the groups need not be K and will not be, save in very special circumstances. (p. 122)

Thorndike referred to an example of this mistake from the literature of his time, which we won't get into, here. He then worked through the fallacy with 12 simulated data sets. We'll cover those in detail. In each of his synthetic data sets, "A is supposed to be intelligence quotient and B is supposed to be the fraction of a room or number of rooms per person" (p. 124). That is, he was covering the correlation between IQ and the crowdedness of one's living conditions. 

Here we'll copy down the data into a series of [tribble](https://tibble.tidyverse.org/reference/tribble.html)s.

```{r, warning = F, message = F}
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

We'll combine them, here.

```{r}
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
















## Session info

```{r}
sessionInfo()
```

