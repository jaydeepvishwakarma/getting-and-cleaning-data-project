
#loding reshape2 package 
library(reshape2)


#STEP 1: Merges the training and the test sets to create one data set

# read all data files into data tables
subjectTrain <- read.table("train/subject_train.txt")
subjectTest <- read.table("test/subject_test.txt")
XTrain <- read.table("train/X_train.txt")
XTest <- read.table("test/X_test.txt")
YTrain <- read.table("train/y_train.txt")
YTest <- read.table("test/y_test.txt")

# add column name for subject files
names(subjectTrain) <- "subjectId"
names(subjectTest) <- "subjectId"

# add column names for measurement files
featureNames <- read.table("features.txt")
names(XTrain) <- featureNames$V2
names(XTest) <- featureNames$V2

# add column name for label files
names(YTrain) <- "activity"
names(YTest) <- "activity"

# Column binding Train data of X and Y.
trainDataSet <- cbind(subjectTrain, XTrain, YTrain)

# Column binding Test data of X and Y.
testDataSet <- cbind(subjectTest, XTest, YTest)

# Adding both Train and Test data in single data set
data <- rbind(trainDataSet, testDataSet)


# STEP 2: Extracts only the measurements on the mean and standard deviation for each measurement.

# grepping columns which contains "mean" or "std" along with subjectID and activity columns
meanAndStd <- grepl("mean", names(data)) | grepl("std", names(data)) | grepl("activity", names(data)) | grepl("subjectId", names(data)) 

# removing noise columns
data <- data[, meanAndStd]


# STEP 3: Uses descriptive activity names to name the activities in the data set.
# STEP 4: Appropriately labels the data set with descriptive
# activity names.

# Load: activity labels
activityLabels <- read.table("activity_labels.txt")[,2]

# convert the activity column from numeric to factor by using activityLables data
data$activity <- factor(data$activity, labels = activityLabels)


# STEP 5: Creates a second, independent tidy data set with the
# average of each variable for each activity and each subject.

# creating tidy data set
melted <- melt(data, id=c("subjectId","activity"))
tidyData <- dcast(melted, subjectId+activity ~ variable, mean)

# write the tidy data set to a file
write.table(tidyData, file = "tidy_data.txt", row.name=FALSE)
