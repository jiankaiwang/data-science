# Support Vector Machines

<script src="../js/general.js"></script>

* SVM 是分類中相當著名的方法，尤其是針對多維度的資料。其概念為先將資料轉換成超幾何分布，而後透過投影至二維平面上，並依照二維平面的結果進行分類。

###Training dataset
---

* label 為專家定義之分類結果；欄位 1 - 10 為每個特徵値。

```text
label          1           2           3           4           5           6           7           8           9          10
2.84  0.58333333  0.66666667  0.91666667  0.91666667  0.58333333        0.75  0.66666667  0.58333333  0.66666667        0.75
1.59  0.66666667  0.66666667        0.75        0.75  0.66666667  0.66666667  0.66666667  0.58333333  0.58333333        0.75
0.92  0.66666667        0.75        0.75        0.75        0.75  0.66666667  0.83333333  0.66666667        0.75  0.66666667
1.2         0.75        0.75  0.66666667        0.75        0.75  0.66666667  0.66666667  0.66666667        0.75  0.66666667
1.66  0.66666667  0.66666667        0.75  0.83333333  0.66666667  0.66666667  0.66666667  0.66666667  0.66666667        0.75
1.62  0.66666667  0.66666667        0.75        0.75        0.75  0.66666667  0.66666667  0.58333333  0.66666667        0.75
1.39  0.66666667  0.66666667        0.75  0.66666667  0.66666667  0.66666667  0.66666667  0.58333333  0.58333333  0.66666667
2.56  0.58333333  0.66666667  0.83333333  0.83333333  0.66666667        0.75  0.58333333  0.58333333  0.58333333  0.83333333
0.23        0.75  0.66666667  0.66666667  0.66666667  0.83333333  0.66666667        0.75        0.75        0.75  0.66666667
```

###Testing dataset
---

* label 為要產生分類的結果，欄位 1 - 10 為該筆資料的特徵値。

```text
label           1           2           3           4           5           6           7           8           9          10
    1        0.75        0.75        0.75  0.83333333  0.58333333        0.75  0.66666667  0.58333333  0.66666667  0.66666667
    1  0.66666667        0.75        0.75        0.75  0.58333333  0.66666667        0.75  0.66666667  0.58333333  0.66666667
    1  0.66666667  0.66666667  0.83333333        0.75  0.58333333  0.66666667  0.66666667  0.66666667  0.66666667  0.66666667
    1  0.66666667  0.58333333  0.66666667        0.75  0.66666667  0.66666667  0.66666667  0.66666667        0.75  0.66666667
    1  0.58333333        0.75  0.83333333        0.75  0.66666667  0.66666667  0.66666667  0.58333333  0.58333333  0.66666667
    1  0.66666667  0.66666667  0.83333333  0.83333333  0.66666667  0.66666667        0.75        0.75  0.66666667  0.66666667
    1  0.66666667  0.66666667        0.75        0.75  0.66666667        0.75  0.66666667  0.66666667  0.66666667  0.66666667
    1  0.83333333        0.75  0.83333333        0.75  0.66666667  0.66666667        0.75        0.75        0.75  0.66666667
    1  0.58333333        0.75  0.66666667        0.75  0.58333333        0.75        0.75  0.58333333  0.66666667  0.58333333
```

###Code in R
---

* SVM 是透過多個分類特徵來建立起分類依據，但並非所有特徵皆須納入考慮，可以透過簡單的資料分散性來取出資料較為分散的特徵，並透過訓練此篩選出的特徵進行分類訓練即可。

```R
# read data
getOriData <- read.table("training.12-mer.features.csv",header=T,sep=",")
getTest <- read.table("testing.12-mer.features.csv",header=T,sep=",")
#-------------------------------------------
# data distribution
sdData <- function(data) {
	return(sd(data))
}
getDataDistribution <- apply(getOriData[,-1],2,sdData)

# sort
getMaxMin <- as.matrix(sort(getDataDistribution))
#--------------------------------
# selection range
lRange <- which(getMaxMin[] > 0.062)
sRange <- which(getMaxMin[] < 0.043)

# total
getMaxCol <- rownames(getMaxMin)[lRange]
getMinCol <- rownames(getMaxMin)[sRange]
getTtlFeatures <- c(getMaxCol,getMinCol)

# get for trainning
train <- getOriData[,getTtlFeatures]
labels <- getOriData[,"label"]
test <- getTest[,getTtlFeatures]
# -------------------------------------------
# svm
install.packages("e1071")
library("e1071")

newFactor <- factor(labels)
model <- svm(train,newFactor,type="C-classification")
svmClass <- predict(model,test)

write.table(svmClass,"output2.txt",sep=",",quote=FALSE,eol = "\n",row.names = FALSE,col.names= FALSE)
```


