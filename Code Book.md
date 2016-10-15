# Code Book

## Getting and Cleaning Data Course Project

## Description
####Additional information about the variables, data and transformations used in the course project for the Johns Hopkins Getting and Cleaning Data course.

## Instruction
1. You have to download sourse data from link below and unzip it to working directory of R Studio.
2. You have to perform R script.

## Source Data
As sourse data for work was used Human Activity Recognition Using Smartphones Data Set. 

A full description is available at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

## Data Set Information
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

## Attribute Information

For each record in the dataset it is provided:

* Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
* Triaxial Angular velocity from the gyroscope.
* A 561-feature vector with time and frequency domain variables.
* Its activity label.
* An identifier of the subject who carried out the experiment.


## R script
File with R code "run_analysis.R" perform following steps to clean the data (in accordance assigned task of course work):   

i.	**Read training data set**
Read X_train.txt, y_train.txt and subject_train.txt from the "train" folder and store them in trainData,trainLabel and trainSubject variables respectively.


ii.		**Read test data set**

Read X_test.txt, y_test.txt and subject_test.txt from the "test" folder and store them in testData, testLabeland testsubject variables respectively.

iii.	**Concatenate test dataset to training dataset**

Concatenate testData to trainData to generate a 10299x561 data frame, joinData; concatenate testLabel totrainLabel to generate a 10299x1 data frame, joinLabel; concatenate testSubject to trainSubject to generate a 10299x1 data frame, joinSubject.

iv.	**Read features file**

Read the features.txt file from the "data" folder and store the data in a variable called features. We only extract the measurements on the mean and standard deviation. This results in a 66 indices list. We get a subset ofjoinData with the 66 corresponding columns.

v.	**Clean the column names of the subset**

Clean the column names of the subset. We remove the "()" and "-" symbols in the names, as well as make the first letter of "mean" and "std" a capital letter "M" and "S" respectively.

vi.	**Read the activity_labels**

Read the activity_labels.txt file from the "data" folder and store the data in a variable called activity.

vii.	**Clean the activity names in the second column of activity**

Clean the activity names in the second column of activity. We first make all names to lower cases. If the name has an underscore between letters, we remove the underscore and capitalize the letter immediately after the underscore.

viii.	**Transform the values of joinLabel**

Transform the values of joinLabel according to the activity data frame.

ix.	**Combine the joinSubject, joinLabel and joinData**

Combine the joinSubject, joinLabel and joinData by column to get a new cleaned 10299x68 data frame,cleanedData. Properly name the first two columns, "subject" and "activity". The "subject" column contains integers that range from 1 to 30 inclusive; the "activity" column contains 6 kinds of activity names; the last 66 columns contain measurements that range from -1 to 1 exclusive.

x.	**Write tidy dataset**

Write the cleanedData out to "merged_data.txt" file in current working directory.

xi.	**Generate a second independent tidy data set for average of each measurement**

Finally, generate a second independent tidy data set with the average of each measurement for each activity and each subject. We have 30 unique subjects and 6 unique activities, which result in a 180 combinations of the two. Then, for each combination, we calculate the mean of each measurement with the corresponding combination. So, after initializing the result data frame and performing the two for-loops, we get a 180x68 data frame.

xii.	**Write the result out to "data_with_means.txt"**

Write the result out to "data_with_means.txt" file in current working directory.
