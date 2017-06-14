# Text Mining on tm pakage in R

<script type="text/javascript" src="../js/general.js"></script>

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

### Data Transformation (Corpus Handling)
---

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


d.corpus <- tm_map(d.corpus,content_transformer(removeWords),stopwords("english"))
```






