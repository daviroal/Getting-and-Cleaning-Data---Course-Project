library(dplyr)
 
 
features <- read.table("UCI HAR Dataset/features.txt", col.names = c("n","functions"))
activities <- read.table("UCI HAR Dataset/activity_labels.txt", col.names = c("code", "activities"))
test <- read.table("UCI HAR Dataset/test/subject_test.txt", col.names = "subject")
x_test <- read.table("UCI HAR Dataset/test/X_test.txt", col.names = features$functions)
y_test <- read.table("UCI HAR Dataset/test/y_test.txt", col.names = "code")
train <- read.table("UCI HAR Dataset/train/subject_train.txt", col.names = "subject")
x_train <- read.table("UCI HAR Dataset/train/X_train.txt", col.names = features$functions)
y_train <- read.table("UCI HAR Dataset/train/y_train.txt", col.names = "code")
 
X <- rbind(x_train, x_test)
Y <- rbind(y_train, y_test)
subject <- rbind(train, test)
Merge_D <- cbind(subject, Y, X)
 
TidyD <- Merge_D %>% select(subject, code, contains("mean"), contains("std"))
 
names(TidyD)[2] = "activities"
names(TidyD)<-gsub("BodyBody", "Body", names(TidyD))
names(TidyD)<-gsub("^t", "time", names(TidyD))
names(TidyD)<-gsub("^f", "frequency", names(TidyD))
names(TidyD)<-gsub("Mag", "Magnitude", names(TidyD))
names(TidyD)<-gsub("Acc", "Accelerometer", names(TidyD))
names(TidyD)<-gsub("Gyro", "Gyroscope", names(TidyD))
 
WorkedData <- TidyD %>%
group_by(subject, activities) %>%
summarise_all(funs(mean))
write.table(WorkedData, "WorkedData.txt", row.name=FALSE)
str(WorkedData)
WorkedData
