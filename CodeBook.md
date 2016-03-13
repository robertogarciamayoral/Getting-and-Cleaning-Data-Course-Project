# Code Book

## This file describes the variables, the data, and the transformations performed to clean up the data

### Variables

Variables included in the first tidy data set (data):

* subject
* activity
* tBodyAcc.mean...X
* /.../
* angle.Z.gravityMean
* tBodyAcc.std...X
* /.../
* fBodyBodyGyroJerkMag.std..

Variables included in the second tidy data set (data2):

* subject
* activity
* tBodyAcc.mean...X
* /.../
* angle.Z.gravityMean

## Data

The first data set (data) includes all the observations of the mean and the std deviation of all the features of each subject and activity

The second data set (data2) includes the average of the observations of the mean of all the features of each subject and activity

## Transformations

These transformations have been applied:

* Train and test sets have been merged
* Features labels have been added
* Subject and activity data have been added
* The activity labels have been added instead of the activity numbers
* The mean and std deviation of the features have been selected