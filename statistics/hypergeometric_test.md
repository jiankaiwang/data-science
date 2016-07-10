# Hypergeometric test

<script src="../js/general.js"></script>

###Definition
---

$$p=\sum_{i=E}^{n}\frac{\binom{M}{i}\binom{N-M}{n-i}}{\binom{N}{n}}$$

* N = size of population
* M = number of items in population with property 'E'
* N-M = number of items in population without property 'E'
* n = number of items sampled
* i = number of items in the sample with property 'E'

###Example
---

| desc | format |
| -- | -- |
| A gene ontology reference database contains 1000 genes. | i = 3, n = 10 |
| There are 200 genes involving type "DNA repair". | M = 200, N = 1000 |
| Now, one group contains 10 genes. what is p-value that contains at least 3 genes with the type? | p-value = p(3) + p(4) + p(5) + ... + p(10) = 0.2021 + 0.0877 + ... + 8.52e-08 = 0.32189479 |

###R script
---

* package: Hypergeometric {stats}

* original function prototype

```R
# dhyper gives the density
dhyper(x, m, n, k, log = FALSE)

# phyper gives the distribution function
phyper(q, m, n, k, lower.tail = TRUE, log.p = FALSE)

# qhyper gives the quantile function
qhyper(p, m, n, k, lower.tail = TRUE, log.p = FALSE)

# rhyper generates random deviates.
rhyper(nn, m, n, k)
```

* parameters

```R
x,q: vector of quantiles representing the number of white balls drawn without replacement from an urn which contains both black and white balls.
m: the number of white balls in the urn.
n: the number of black balls in the urn.
k: the number of balls drawn from the urn.
```

* Example.1 in R

```R
# prepare data
m <- 10; n <- 7; k <- 8
x <- 0:(k+1)
		       
# start to calculate hypergeometric test
phyper(x, m, n, k)	# test result
dhyper(x, m, n, k)	# distribution density
```

* Example.2 in R

```R
# prepare data
# pop size : 5260
# sample size : 131
# Number of items in the pop that are classified as successes : 1998
# Number of items in the sample that are classified as successes : 62

# data
#			population			
# condition		sample		others		total
#	success		62		1936		1998
#	failure		69		3193		3262
# total			131		5129		5260

# start calculate hypergeometric test (phyper)
# with description
# phyper(white balls drawn, total white balls, total black balls, totally drawn)
phyper(62, 1998, 5260-1998, 131)
```



