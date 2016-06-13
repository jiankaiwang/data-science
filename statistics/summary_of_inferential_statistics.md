# Summary of Inferential Statistics

<script src="../js/general.js"></script>

###下列表格整理出針對不同狀況而使用的假說性統計方法
---

| 檢定條件 | 兩組<br>獨立樣本 | 兩組<br>相依樣本 | 三組以上<br>獨立樣本 | 三組以上<br>相依樣本 | 連續性 |
| -- | -- | -- | -- | -- | -- |
| 連續與否 | 檢定目的<br>集中趨勢 (Central tendency) | 檢定目的<br>集中趨勢 (Central tendency) | 檢定目的<br>集中趨勢 (Central tendency) | 檢定目的<br>集中趨勢 (Central tendency) | 相關分析 |
| 常態假設或<br>中央極限定理成立<br>(Shapiro-Wilk Test) | Independent<br> t-test | Paired<br> t-test | ANOVA (with Multiple Comprison) | Repeated measures ANOVA | Pearson's<br>correlation |
| 非常態假設或<br>中央極限定理不成立 | Wilcoxon rank-sum test<br> (or Wilcoxon-Mann-Whitney<br> Two-Sample Test) | Wilcoxon signed-rank test | Kruskal-Wallis test	| Friedman test	| Spearman`s correlation |

| 檢定條件 | 兩組<br>獨立樣本<br>關聯性 (Association) | 兩組<br>相依樣本<br>關聯性 (Association) | 三組以上<br>獨立樣本<br>關聯性 (Association) | 三組以上<br>相依樣本<br>關聯性 (Association) |
| -- | -- | -- | -- | -- |
| 檢定方法 <br>(皆 non-parameteric) | 1. Chi-square test (with correlation [2])<br>2. Fisher's exact test ([3])<br>3. Hypergeometeric test | McNemar`s test | Pearson's chi-square test | Cochran`s test |
| 連續性<br>相關分析 | Logistic regression | Logistic regression | Multinomial / Ordinal<br>logistic regression | Multinomial / Ordinal<br>logistic regression |

###重要說明
---

1. ANOVA 並無法得知各組間的比較，如 (Sample1, Sample2)、(Sample1, Sample3)、...。透過 Multiple comparison 可以進行 pairwise 的比較而挑出各組間是否有顯著差異，常用的方法如 Tukey's method、Fisher's Least Significant Difference 與 Duncan's New Multiple Range Test 等。

2. 常見的 correltion 方式如 Yate's correlation 等。

3. Chi-square test 與 Fisher's exact test 主要差異為 2x2 相關聯表中的數值大或小 (或者說 frequency 大小)。一般而言，Fisher's exact test 更常用於數值小的 p-value 計算，且較為合理。The test based on the hypergeometric distribution (hypergeometric test) is identical to the corresponding one-tailed version of Fisher's exact test. Reciprocally, the p-value of a two-sided Fisher's exact test can be calculated as the sum of two appropriate hypergeometric tests.

4. 當比較兩個未成對的群組時 (two unpaired groups)，在有參數(parametric)/常態假說/中央極限定理下，應使用未成對 t 檢定 (unpaired t-test)。


