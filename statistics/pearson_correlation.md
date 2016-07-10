# Pearson Correlation

<script src="../js/general.js"></script>

###Pearson Correlation Definition
---

* For a population

$$$$

* For a sample

###Calculate Correlation in R
---

```R
# use cor{stats}
data1 <- rnorm(10, mean = 2, sd = 1)
data2 <- rnorm(10, mean = 4, sd = 2)

# start to calculate pearson correlation coefficient
pearsonRes <- cor(data1, data2, use = "everything", method = "pearson")
```

###Test of pearson correlation in R
---

```R
# use cor{stats}
data1 <- rnorm(10, mean = 2, sd = 1)
data2 <- rnorm(10, mean = 4, sd = 2)

# start statistics test of pearson correlation
pearsonTest <- cor.test(data1, data2, alternative = "two.sided", method = "pearson")
pearsonTestCor <- pearsonTest$estimate
pearsonTestPvalue <- pearsonTest$p.value
```