### Code Book

This code book will help to describe the data and variable used in this project, It will also help to understand all transformation 
done on various steps.

## Overview

30 volunteers performed 6 different activities while wearing a smartphone. All those activities are WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING. The smartphone captured various data about their movements.

## All datasets

* `features.txt`: It have information about the variables that used on the feature vector.
* `activity_labels.txt`: It consist the Names and IDs of all activities.

* `train/subject_train.txt`: Keeps subject IDs for train data.
* `test/subject_test.txt`: Keeps subject IDs for test data.

* `train/X_train.txt`: obeservations data.
* `train/Y_train.txt`:activity related to each of the observations in above file.
* `test/X_test.txt`: observations data of test.
* `test/y_test.txt`: activity related to each of the observations in above file.

## Operation Details for the datasets
* Merges the training and the test sets to create one data set.
* Extracts only the measurements on the mean and standard deviation for each measurement.
* Uses descriptive activity names to name the activities in the data set
* Appropriately labels the data set with descriptive variable names.
* From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

## Implementation of above steps in `run_analysis.R`
* Load reshapre2 and data.table librareis.
* Load all files in data table.
* Add column names for subject files, measurement files and label files.
* Column binding Train data of X and Y files.
* Column binding Test data of X and Y files.
* Adding both Train and Test data in single data set
* Grepping columns which contains "mean" or "std" along with subjectID and activity columns and remove noise column
* Convert the activity column from numeric to factor by using activityLables data
* DataSet is melted to create tidy data.
