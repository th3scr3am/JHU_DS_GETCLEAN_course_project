---
title: "codebook.md"
author: "th3scr3am (but you can call me Blair)"
date: "15/04/2020"
output: pdf_document
---


# **Course Project**
## Getting and Cleaning Data
## Data Science Specialization
## Johns Hopkins Univeristy

**About the project**
The project takes data from 7 files and matches & merges them into one tidy dataset.
These datasets have a combined 561 variables.  We are interested in all variables
that contain "mean" or "std" (standard deviation) in the descriptive variable name.
We then create a second tidy data set which averages each of these variables, grouping
these averages by six different activity types. Please refer to the README.txt file
for more information on the contents of this data.

**Step 1**
The first step was to open the test files (call them ytest and xtest).
y_test.txt contained 1 column with 2947 rows
X_test.txt contained 561 column with 2947 rows
activity_labels.txt contained 2 columns with 6 rows
features.txt contained 1 column with 561 rows
I checked table(ytest) to ensure each value in ytest did indeed correlate
to one of the values (1-6) in the first column of activity_labels. The result 
can be seen here:

```{r eval=TRUE}
print("test")
```

```{r}
  library(dplyr)
  ytest <- tbl_df(read.table("dataset/test/y_test.txt"))
  print(table(ytest))
```

I repeated these steps with y_train.txt and X_ train.txt, which had dimensions
of 7352 x 1 and 7352 x 561, respectively.I checked table(ytrain) to ensure each 
value in ytrain did indeed correlate to one of the values (1-6) in the first column 
of activity_labels. The result can be seen here:

```{r}
  
  ytrain <- tbl_df(read.table("dataset/train/y_train.txt"))
  print(table(ytrain))
```

**Step 2: I complete the following in R script run_analysis.R. See comments in that
R script for more information**
I first correlated activity_labels to ytest
I observed that the activity labels used variables V1 and V2. I was interested 
in V2 (which were the names)since the V1 variables correlated to V2 by way of 
indices so V1 was redundant. I then converted the ytest numbers into these 
activity labels which are clearly descriptive.  I took xtest and renamed the variables 
according to best practices. The variable names are based on the features_info.txt
file which shows their descriptions (and thus the variables are descriptive).  See the
README.txt file where I've copied and pasted this info. 

I added the converted ytest data as a new variable called activity and then 
assigned a new data set to xtest for variables including "mean" or "standard deviation (std)"
as well as the activity labels.

**Step 3: Also in the run_analysis.R script, I create a 2nd data set. See R script
comments for more information**
I grouped the first dataset by activity to create a 2nd dataset.  I then summarized each
of the variables in this new data set in order to get the average of each variable.

**Step 4: Auditing the new data sets**
