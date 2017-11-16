# Text Mining on tm pakage in R



### Dependency
---

* tm package in R

```r
# necessary for text mining
install.packages("tm")

# necessary for fetching web content
install.packages("RCurl")
install.packages("XML")

# import the library
library("tm")
library("RCurl")
library("XML")
```

### Processing Flow
---

* Data import
* Corpus Handling
* Preprocessing
* Metadata management
* Creation of term-document matrices
* Data analysis
* Dictionary list

### Data import
---

* Parse the web content, parse it and prepare a corpus object

```r
# fetch html content
doc.html = htmlTreeParse(
  'http://www.asahichinese-f.com/?iref=comtop_usnavi', 
  useInternal = TRUE
)

# detail with html content
doc.text = unlist(xpathApply(doc.html, '//a', xmlValue))
doc.text = gsub('\\n', '', doc.text, fixed = TRUE)
doc.text = gsub(' ', '', doc.text, fixed = TRUE)
doc.text = gsub('\\t', '', doc.text, fixed = TRUE)
```

### Corpus Handling
---

```R
# Data (Corpus) Preparation on VCorpus (Volatile)
# reader : getReaders() to see supported list
# language : ISO 639-2 codes
# |- zho : chinese
d.corpus <- VCorpus(
  VectorSource(doc.text), 
  list(
    reader = readPlain,
    language = "zho"
  )
)
```

### Data Transformation (Preprocessing)
---

* character-based transformations

```r
# remove punctuation
d.corpus <- tm_map(d.corpus, content_transformer(removePunctuation))

# remove numbers
d.corpus <- tm_map(d.corpus, content_transformer(removeNumbers))

# remove numbers and alphabets
d.corpus <- tm_map(d.corpus, content_transformer(function(word) {
  gsub("[A-Za-z0-9]", "", word)
}))

# prepare as the plain text document
d.corpus <- tm_map(d.corpus, content_transformer(PlainTextDocument))

# strip the white space
d.corpus <- tm_map(d.corpus, content_transformer(stripWhitespace))

# stopping words
d.corpus <- tm_map(d.corpus,content_transformer(removeWords),stopwords("english"))
```

* rule-based `filters`

```r
# Data filter
getIdx <- tm_filter(
  d.corpus,
  FUN = function(x){ 
    any(grep("旅遊",content(x)))
  }
)

# remove unnecessary words
myStopWords <- c(stopwordsCN(), "編輯", "時間", "標題", "發信", "實業", "作者")
d.corpus <- tm_map(
  d.corpus, 
  content_transformer(removeWords), 
  myStopWords
)
head(myStopWords, 20)
```

### Metadata management
---

There are two methods in `tm` package to manage the metadata,
1. DublinCore
2. meta
  , and `meta` further includes two types of metadata,
3. metadata on corpus level (corpus)
4. individual documents (indexed) in form of a data frame.

* by `DublinCore()`

```r
# by DublinCore()
DublinCore(d.corpus[[27]], "keyword") <- "關鍵字"
meta(d.corpus[[27]])
```

* by `meta()`

```r
# by meta()
meta(d.corpus[[27]], tag = "keylist", type = "corpus") <- "關鍵字清單"
meta(d.corpus[[27]], type = "corpus")
```

### Creation of term-document matrices
---

* Term-Document Matrix (terms as the row and docs as the column)

```r 
tdm <- TermDocumentMatrix(
  d.corpus, 
  control = list(
    wordLengths = c(2, 10),
    removePunctuation = TRUE,
    stopwords = FALSE,
    weighting = function(x)weightTfIdf(x,normalize = TRUE)
  )
)
inspect(tdm)
```

* Document-Term matrix (docs as the row and terms as the column)

```r
dtm <- DocumentTermMatrix(
  d.corpus, 
  control = list(
    wordLengths = c(2, 10),
    removePunctuation = TRUE,
    stopwords = FALSE,
    weighting = function(x)weightTfIdf(x,normalize = TRUE)
  )  
)
inspect(dtm)
```

### Data analysis
---

* find terms by frequencies

```r
allTerms <- findFreqTerms(tdm,5)
```

* find terms by association

```r
findAssocs(tdm, allTerms[3], 0.1)
```

* remove terms by sparsing

```r
inspect(
  removeSparseTerms(dtm, 0.4)
)
```

### Dictionary List
---

```r
# Dictionary
inspect(
  DocumentTermMatrix(
    d.corpus, 
    list(dictionary = c(allTerms[1],allTerms[2]))
  )
)
```







