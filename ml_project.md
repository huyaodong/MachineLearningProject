Title
========================================================

This is an R Markdown document. Markdown is a simple formatting syntax for authoring web pages (click the **Help** toolbar button for more details on using R Markdown).

When you click the **Knit HTML** button a web page will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


```r
setwd('C:/Users/Badger/Dropbox')
library(caret)
```

```
## Loading required package: lattice
## Loading required package: ggplot2
```

```r
library(kernlab)
training <- read.csv('pml-training.csv')
testing  <- read.csv('pml-testing.csv')
```

After reading the data to R, columns without any value were removed to create dataset with fewer columns.



Record 5373 could be an outlier since the x, y, z coordinates for forearm gyros are very extreme so this record will be removed from the training set. For the same reason, records 152 and 9274 could be outliers for the y coordinate of magnet dumbbell and gyros dumbbell, respectively.


```r
training <- training[-5373, ]
training <- training[-9273, ]
training <- training[-152]
```


```r
modelfit <- train(classe ~ ., data = training, method = 'svmRadial')
```

