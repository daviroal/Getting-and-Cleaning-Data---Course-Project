The run_analysis.R script performs the preparation and then followed by the 5 steps required.
1. Download the dataset
o Dataset downloaded and extracted under the folder called UCI HAR Dataset
2. Assign each data to variables
o features <- features.txt : 561 rows, 2 columns
The features selected for this database come from the Accelerometer and Gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ.
o activities <- activities_labels.txt : 6 rows, 2 columns 
List of activities performed when the corresponding measurements were taken and its codes (labels)
o test <- test/subject_test.txt : 2947 rows, 1 column 
contains test data of 9/30 volunteer test subjects being observed
o x_test <- test/X_test.txt : 2947 rows, 561 columns 
contains recorded features test data
o y_test <- test/y_test.txt : 2947 rows, 1 columns 
contains test data of activities’code labels
o train <- test/subject_train.txt : 7352 rows, 1 column 
contains train data of 21/30 volunteer subjects being observed
o x_train <- test/X_train.txt : 7352 rows, 561 columns 
contains recorded features train data
o y_train <- test/y_train.txt : 7352 rows, 1 columns 
contains train data of activities’code labels
 
3. Merges the training and the test sets to create one data set
o X (10299 rows, 561 columns) is created by merging x_train and x_test using rbind() function
o Y (10299 rows, 1 column) is created by merging y_train and y_test using rbind() function
o subject (10299 rows, 1 column) is created by merging train and test using rbind() function
o Merge_D (10299 rows, 563 column) is created by merging subject, Y and X using cbind() function
 
4. Extracts only the measurements on the mean and standard deviation for each measurement
o TidyD (10299 rows, 88 columns) is created by subsetting Merge_D, selecting only columns: subject, code and the measurements on the mean and standard deviation (std) for each measurement
 
5. Uses descriptive activities names to name the activities in the data set
o Entire numbers in code column of the TidyD replaced with corresponding activities taken from second column of the activities variable
 
6. Appropriately labels the data set with descriptive variable names
o All Mag in column’s name replaced by Magnitude
o code column in TidyD renamed into activities
o All start with character t in column’s name replaced by time
o All Acc in column’s name replaced by Accelerometer
o All BodyBody in column’s name replaced by Body
o All start with character f in column’s name replaced by frequency
o All Gyro in column’s name replaced by Gyroscope
 
7. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activities and each subject
o WorkedData (180 rows, 88 columns) is created by sumarizing TidyD taking the means of each variable for each activities and each subject, after groupped by subject and activities.
o Export WorkedData into WorkedData.txt file.
 
