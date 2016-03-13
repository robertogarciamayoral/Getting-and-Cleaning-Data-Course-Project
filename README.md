# READ ME

## This file contains the script 'run_analysis.R'

This script does the following:

1) Merges the training and the test sets to create one data set
2) Extracts only the measurements on the mean and standard deviation for each measurement
3) Uses descriptive activity names to name the activities in the data set
4) Appropriately labels the data set with descriptive variable names 
5) From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject

Script:

```{r}

library(dplyr)

## Read and merge features data from training and test data sets 
## Add column names from features labels data
## Rename duplicated column names
X_test <- read.table('X_test.txt')
X_train <- read.table('X_train.txt')
X <- rbind(X_test, X_train)
features_labels <- read.table('features.txt')
names(X) <- make.names(features_labels[,2], unique = TRUE)

## Read and merge activity data from training and test data sets
## Add column name
## Replace activity numbers by labels from activity labels data
y_test <- read.table('y_test.txt')
y_train <- read.table('y_train.txt')
y <- rbind(y_test, y_train)
names(y) <- 'activity'
activity_labels <- read.table('activity_labels.txt')
for (m in 1:length(y[,1])){        
        for (n in 1:length(activity_labels[,1])){
                if (y[m,1] == n){y[m,1] <- as.character(activity_labels[n,2]);break}
        }
}

## Read and merge subject data from training and test data sets
## Add column name
subject_test <- read.table('subject_test.txt')
subject_train <- read.table('subject_train.txt')
subject <- rbind(subject_test, subject_train)
names(subject) <- 'subject'

## Bind features, activity and subject data
data <- cbind(subject, y, X)

## Select mean and std deviation measurements
data <- select(data, contains('mean'), contains('std'), subject, activity)

## Creates a second, independent tidy data set
## with the average of each variable for each activity and each subject

data2 <- data %>% select(-contains('std')) %>%
        group_by(activity, subject) %>%
        summarize_each(funs(mean))
        
```