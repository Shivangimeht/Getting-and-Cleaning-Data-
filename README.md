# Getting-and-Cleaning-Data-
###Download this spread sheet.

if(!file.exists("./data")){dir.create("./data")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl,destfile="./data/Dataset.zip")

###unzipped the file
unzip(zipfile="./data/Dataset.zip",exdir="./data")

####1.Merges the training and the test sets to create one data set.

##a.Reading All files

  x_train <- read.table("./data/UCI HAR Dataset/train/x_train.txt")
  y_train <- read.table("./data/UCI HAR Dataset/train/y_train.txt")
  subject_train <- read.table("./data/UCI HAR Dataset/train/Subject_train.txt")  

  x_test <- read.table("./data/UCI HAR Dataset/test/x_test.txt")
  y_test <- read.table("./data/UCI HAR Dataset/test/y_test.txt")
  subject_test <- read.table("./data/UCI HAR Dataset/test/Subject_test.txt")
  
  Features <- read.table("./data/UCI HAR Dataset/features.txt")
  
  activitylables <- read.table("./data/UCI HAR Dataset/activity_labels.txt")

##b. Assigning name
  
  colnames(x_train) <- Features[,2]
  colnames(y_train) <- "activityID"
  colnames(subject_train) <- "subjectID"

  colnames(x_test) <- Features[,2]  
  colnames(y_test) <- "activityID"  
  colnames(subject_test) <- "subjectID"  

##c. Merging all data.
  
  mytrain <- cbind(y_train,subject_train,x_train)
  mytest <- cbind(y_test,subject_test,x_test)
  Tidy_data <- rbind(mytrain, mytest)

  dim(Tidy_data)  

##d. Reading colnames 
  
  colnames <- colnames(Tidy_data)
  
###2.Extracts only the measurements on the mean and standard deviation for each measurement. 
  
  mean_and_sd <- (grepl("activityID",colnames)|
                    grepl("subjectID",colnames)|
                    grepl("mean..",colnames)|
                    grepl("sd...",colnames)
                  )
Data_sd_mean <- Tidy_data[,mean_and_sd==TRUE]

###3.Uses descriptive activity names to name the activities in the data set

setwithactivitynames <- merge(Data_sd_mean,activitylables)

###4.Appropriately labels the data set with descriptive variable names. 

  Completed 

###5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

Tidy_data <- aggregate(.~subjectID+activityID,setwithactivitynames,mean)
Tidy_data <- Tidy_data[order(Tidy_data$subjectID, Tidy_data$activityID),]

write.table(Tidy_data, "C:/Users/Shivangi95/Desktop/TidyData.html", row.name=FALSE)
