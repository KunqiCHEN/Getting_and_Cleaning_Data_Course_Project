##outcome:
column 2: activity 
Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING)

The features selected for this database come from the accelerometer and gyroscope one-axial raw signals timeAcc-X and timeGyro-X. These time domain signals (prefix 'time' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-X and tGravityAcc-X) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (timeBodyAccJerk-X and timeBodyGyroJerk-X). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (timeBodyAccMag, timeGravityAccMag, timeBodyAccJerkMag, timeBodyGyroMag, timeBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing frequenceBodyAcc-X, frequenceBodyAccJerk-X, frequenceBodyGyro-X, (Note the 'frequence' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-X' is used to denote one-axial signal in the X directions; '-y' is used to denote one-axial signal in the y directions; '-Z' is used to denote one-axial signal in the Z directions.

The set of variables that were estimated from these signals are: 

Mean(): Mean value
Std(): Standard deviation

##process:
X_train.txt was saved as train.x;
y_train.txt was saved as train. Y;
subject_train.txt was saved as train.subject;
X_test.txt was saved as test.x;
y_test.txt was saved as test.y;
subject_test.txt was saved as test.subject;

Then, train and test data were merged by 
trainData <- cbind(train.subject, train.y, train.x);
testData <- cbind(test.subject, test.y, test.x);
fullData <- rbind(trainData, testData).

And, we extract mean and standard deviation of each measurements
featureIndex <- grep(("mean\\(\\)|std\\(\\)"), featureName)
finalData <- fullData[, c(1, 2, featureIndex+2)]
colnames(finalData) <- c("subject", "activity", featureName[featureIndex])

Finally,
The column name were described by:
activityName <- read.table("./data/UCI HAR Dataset/activity_labels.txt")
finalData$activity <- factor(finalData$activity, levels = activityName[,1], labels = activityName[,2])
names(finalData) <- gsub("\\()", "", names(finalData))
names(finalData) <- gsub("^t", "time", names(finalData))
names(finalData) <- gsub("^f", "frequence", names(finalData))
names(finalData) <- gsub("-mean", "Mean", names(finalData))
names(finalData) <- gsub("-std", "Std", names(finalData))
