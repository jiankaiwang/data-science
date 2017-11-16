# Spearman Rank Correlation



##Calculate Correlation in R
```R
# use cor{stats}
data1 <- rnorm(10, mean = 2, sd = 1)
data2 <- rnorm(10, mean = 4, sd = 2)

# start calculating spearman rank correlation
spearmanRes <- cor(data1, data2, use = "everything", method = "spearman")
```



##Test of pearson correlation in R

```R
# use cor{stats}
data1 <- rnorm(10, mean = 2, sd = 1)
data2 <- rnorm(10, mean = 4, sd = 2)

# start statistics test of spearman correlation
spearmanTest <- cor.test(data1, data2, alternative = "two.sided", method = "spearman")
spearmanTestCor <- spearmanTest$estimate
spearmanTestPvalue <- spearmanTest$p.value
```