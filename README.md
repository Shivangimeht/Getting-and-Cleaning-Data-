# Getting-and-Cleaning-Data-
###Download this spread sheet.

if(!file.exists("./data")){dir.create("./data")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl,destfile="./data/Dataset.zip")

###unzipped the file
unzip(zipfile="./data/Dataset.zip",exdir="./data")

####1.Merges the training and the test sets to create one data set.

##a.Reading All files

 
##b. Assigning name
  
  
##c. Merging all data.
  
 
  
##d. Reading colnames 
  
  
  
###2.Extracts only the measurements on the mean and standard deviation for each measurement. 
  
 

###3.Uses descriptive activity names to name the activities in the data set

setwithactivitynames <- merge(Data_sd_mean,activitylables)

###4.Appropriately labels the data set with descriptive variable names. 

  Completed 

###5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.


