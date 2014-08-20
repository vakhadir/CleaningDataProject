CleaningDataProject
===================

The course project for getting and cleaning data - Coursera Data Science course.

The data has been divided into test and train folders. In this document, data is named as test data and train data to refer to 
data from test folder and data from train folder respectively.


Identify files:
==============
Following files has been identified to be processed.

1. /UCI HAR Dataset/test/subject_test.txt
2. /UCI HAR Dataset/test/X_test.txt
3. /UCI HAR Dataset/test/y_test.txt
4. /UCI HAR Dataset/train/subject_train.txt
5. /UCI HAR Dataset/train/X_train.txt
6. /UCI HAR Dataset/train/y_train.txt

The subject files(1 and 4 from above list) consisting a list of participants of the experiment. 
The y_ files (3 and 6 from above list) consisting of the activities performed by the participants during the experiment.
The X_ files (1 and 5 from above list) consisting of the data from the experiment.

Analyze the Data:
================
Read the identified files using read.table to make the following variables.
1. subtest
2. xtest
3. ytest
4. subtrain
5. xtrain
6. ytrain

Get the dimension of all test files

> dim(subtest)
[1] 2947    1
> dim(xtest)
[1] 2947  561
> dim(ytest)
[1] 2947    1

All test files has same number of row as they are related to each other in a way that subtest has a list of all participants
of the experiment in one column and ytest has one column of the activity performed during the experiment and xtest has 561 columns 
of the recorded experiment data.

Similarly get to dimension of the train data: 

> dim(subtrain)
[1] 7352    1
> dim(xtrain)
[1] 7352  561
> dim(ytrain)
[1] 7352    1


Merging the test and train data:
===============================

Merge test data together using column binding the data sets; subtest, ytest and xtest to form a new data set called 'test'.
Similarly merge train data together using column binding the data sets; subtrain,ytrain and xtrain to form a new data set called 'train'.

Now we have 2 data sets called 'test' and 'train'. See the dimensions of both

> dim(test)
[1] 2947  563
> dim(train)
[1] 7352  563

Both has exactly same number of columns. Now both of them has to be merged by row binding to form a full blown raw data set called 'rawData'.

Assign names and extract required fields from raw data:
======================================================

Copy and paste the 561 variable names from features.txt to an excel spreadsheet. The file features.txt has been supplied with the course project data.  
Add two fields Subject and Activity to the beginning of the list in the spreadsheet to make the number of variables in the list to 563.

Assign these variable names (from the spreadsheet) to the data set rawData. Refer to the assign_names() function in the source code of run_analysis.R

Go thru the list from the spreadsheet and note down the index of the required variables (mean and sd variables) to be extracted from the data set rawData. 

Using subsetting technique and above identified variable indices, extract a subset of rawData and name it 'tidyData1'.

Verify the columns of tidyData1. 

>names(tidyData1)


Calculate Averages:
==================

Following script displays the 296 rows of variable tBodyAcc-mean()-X for the Participant 1 while the Participant was WALKING. 

> tidyData1[tidyData1$Subject ==1 & tidyData1$Activity == 1,1:3]

We need to get average of all 296 rows. 

Similarly there are 29 other participants and 5 more activities. So 30 multiplied by 6 is 180 number of rows we get for each variable. 

This has been achieved by aggregate function by Activity and Subject. The resultant data set is named as 'tidyData2'.


Tidy Data:
==========

Aggregate function appends the two variable by which aggregate has been performed to the data set tidyData2. 

Using following script verify that Activity and Subject has been repeated.

>names (tidyData2)

By subsetting,  remove 2 and 3rd columns to make the final data set tidyData. Write the tidy data to the current working directory.
The name of the file is TidyData.txt.



Running the Script:
==================

The script run_analysis.R assumes that the folder 'UCI HAR Dataset' supplied with the course project is present the same director as the source file.
to run the script type the following command.

>run_analysis()

It produces TidyData.txt in the same directory where run_analysis is placed. 


Min and Max values
==================
The minimum and maximum values recorded for each variable in the CodeBook.md have been found using the follwing script

>data.frame(min=sapply(tidyData,min),max=sapply(tidyData,max))

