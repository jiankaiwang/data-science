# Pearson Correlation

<script type="text/javascript" src="../js/general.js"></script>

###Pearson Correlation Definition
---

* For a population

$$\rho_{X,Y} = \frac{cov(X,Y)}{\sigma_X\sigma_Y} = \frac{E[(X - \mu_X)(Y - \mu_Y)]}{\sigma_X\sigma_Y}$$

where, cov is the covariance, $$\sigma_X$$ is the standard deviation of X

$$\mu_X$$ is the mean of X, and E is the exceptation.

* For a sample

$$r = \frac{\Sigma_{i=1}^{n}(X_i-\bar{X})(Y_i-\bar{Y})}{\sqrt{\Sigma_{i=1}^{n}(X_i-\bar{X})^2}\sqrt{\Sigma_{i=1}^{n}(Y_i-\bar{Y})^2}}$$

where, an equivalent expression is the following:

$$r = \frac{1}{n-1}\Sigma_{i=1}^{n}(\frac{X_i-\bar{X}}{S_X})(\frac{Y_i-\bar{Y}}{S_Y})$$

where,

$$\bar{X} = \frac{1}{n}\Sigma_{i=1}^{n}X_i,\ and\ S_X = \sqrt{\frac{1}{n-1}\Sigma_{i=1}^{n}(X_i-\bar{X})^{2}}$$

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