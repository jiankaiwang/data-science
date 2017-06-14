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

# Data Preparation
# reader : getReaders() to see supported list
# language : ISO 639-2 codes
d.corpus <- VCorpus(
  VectorSource(doc.text), 
  list(
    reader = readPlain,
    language = "zho"
  )
)
```









