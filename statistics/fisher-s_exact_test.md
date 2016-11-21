# Fisher's exact test

<script type="text/javascript" src="../js/general.js"></script>

###Definition
---

![](../images/Fisher-s_exact_test.png)

$$p=\frac{\binom{a+b}{a}\binom{c+d}{c}}{\binom{n}{a+c}}=\frac{(a+b)!(c+d)!(a+c)!(b+d)!}{(a!)(b!)(c!)(d!)(n!)}$$ 

###R script
---

* package: fisher.test {stats}

* original function prototype

```R
fisher.test(
  x, 
  y = NULL, 
  workspace = 200000, 
  hybrid = FALSE, 
  control = list(), 
  or = 1, 
  alternative = c("two.sided","greater","less"), 
  conf.int = TRUE, 
  conf.level = 0.95, 
  simulate.p.value = FALSE, 
  B = 2000
)
```

* Example in R

```R
# prepare data
Testing <- matrix(
                c(1, 11, 9, 3), 
                nrow = 2, 
                dimnames = list(
                  behavior = c("Dieting", "Non-dieting"), 
                  sex = c("Men", "Women")
                )
            )
		       
# the data
#              sex
#  behavior    Men Women
#  Dieting       1     9
#  Non-dieting  11     3
		       
# start to calculate fisher's exact test and get p.value
fisher.test(Testing, alternative = "less")$p.value
```
