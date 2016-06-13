# Summary of Inferential Statistics

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
