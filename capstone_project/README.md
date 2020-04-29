# ![GA Logo](https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67) 


# Capstone Project: Photoshop or Not?

##### Author: Joey Chew, DSI-13, 23 Apr 2020

---

## Problem Statement

We live in a world where digital images pervade all aspects of our lives. Traditional cameras still exist, primarily for hobbies or art, otherwise, the convenience of digital images, and to a wider extent, digital videos lead to them being the media of choice over traditional analog methods.

Unfortunately, with the ease of editing digital images, abuse of such has gained traction too. Tampering of images may range from the helpful, sharpening of desired features, to benign/minor mischief spliced joke photos, to malicious intent such as misleading, swaying of public opinions, or even fraud.

Due to limitations on computational power and resources, I have chosen to limit my addressing of these issues by creating a supervised machine learning model which, upon being presented with a RGB image (full colored image made up of primary colors), executes a binary classification prediction based on trained weights into Class 0 (Unmodified Image) and Class 1 (Modified Image).

My model's predictions will not be limited to any specific domain (eg. humans, specific sports activities). I have set the target for my intended model have better accuracy than a baseline naive prediction of the majority class, as well as aim for a minimum of 85% accuracy on test set used in the model.

---

## Executive Summary

The goal was to train a model to do a binary classification prediction between Unmodified and Modified Images.

Data was extracted from https://github.com/dbisUnibas/PS-Battles, compiled by the Databases and Information Systems Research Group at the Department of Mathematics and Computer Science, University of Basel, Switzerland.

This set of data in turn was generated via a script collecting images from a photoshop battle subreddit, which allowed for the available data to keep growing over time. Format was typically one unmodified image, with subreddit contributors uploading modified versions of that image.

Out of the 100,000 or so images, about 200 original images were chosen, then bootstrapped up to balance against their photoshopped images (approximately 3,000).
After data cleaning and munging, there were about 2500 images having a mix of 53% photoshopped images.

Metric chosen would be primarily based on Test Set Accuracy, with some discussion on Confusion Matrix Classification Metrics.

My trained model was able to achieve 85% Test Accuracy, with Sensitivity/Recall of 0.930, Specificity of 0.780, Precision of 0.788, F1-Score of 0.853, and AUC-ROC Score of 0.905.

Based on the principle of erring on the side of caution, and primary usage of this model to flag out modified photos, due to the negative impact they can cause, a false negative (Type 2 Error) is more damaging than a false positive (Type 1 Error). Hence, Sensitivity/Recall is more important than Specificity here.

The model definitely needs further improvement, but a 85% accuracy on test data with 0.93 Sensitivity/Recall seems to indicate a good start.

---

## Data Collection

In order for a general category image model to be built, the datasets chosen had to reflect the variety needed. Hence, many datasets such as MNIST, and IRIS were rejected as they were specialised in specific domains.

Other considerations were the image formats, the amount of space required to hold the images, and the computing power required to load all these data and model.

Eventually, the PS-Battles dataset, with no focus on any specific domain, was chosen. Out of the 100,000 or so images, resampling together with batch processing was done to better manage the above limitations.

---

## Data Cleaning, Munging & EDA

Due to the 'live' nature of the images scraped from the subreddit, some images were damaged or had broken links and led to unreadable files.

These were taken out during the data cleaning process; they made up an insignificant number compared to the 100,000 total images available.

Of note also is that images in the wild have no fixed format size, nor file type.

During Data Cleaning, it was discovered that png files are generally larger than jpg files, and save their data in float formats, with the values already scaled down from between 0 & 255 to being between 0 & 1.

Images in jpg format seem to come in numerical arrays of integers between 0 & 255.

Part of data cleaning led to synchronizing image data storage format, scaled down to between 0 and 1.

RAM memory of 32GB was insufficient, and so the images were also resized into a maximum of 256 by 256 pixels, with only full color images with 3 color channels of Red, Green and Blue selected.

This addressed the issue of mixing with 4 channel (RGBA) images with the 4th channel being transparency, and 1 channel greyscale images, as these 2 types of images significantly in the minority compared to RGB images in the dataset.

Image aspect ratio was maintained via the thumbnail() method provided by PILLOW, a library for processing images.

Padding of black pixels was then done to fill up images smaller in either dimension, to achieve a uniform image size for modeling.

---

## Preprocessing and Modeling

Image data was successfully converted to array representation for modelling use. Convolutional Neural Networks were chosen for this, based on the industry acceptance of it being the method with the best recent results for image classification.

Even at this stage, data size was an issue, and saving and transferring of files which could be as large as 4GB, and the multi-dimensional nature of the image data, with commas, made it not viable for CSVs, nor even Pickle to work.

HDF5 format was eventually chosen, which allowed for seemingly large files around 4GB to be saved and transferred without much issue.
CSV files were still used for smaller dataframe objects.

Due to memory issues, GridSearchCV and RandomSearch were not practical for the processing power on hand, so different values for hyperparameters like filter size and nodes were chosen for the CNN model used.

Optimal weights across epochs were then saved for future use via keras's model_from_json method.
Post-model treatment consisted of identifying the optimal threshold, and new predictions based on the threshold.

---

## Evaluation and Conceptual Understanding

Baseline Score of dataset is accuracy of 0.53, based on naive assumption of all images belonging to majority class, in this case that is Class 1, Modified Images.

A more in-depth look at metrics used to address problem objective and interpret results of the model:

Sensitivity/Recall (True Positives/All Positives)
Interpretation: Among those which were actually Class 1, Modified Images, what was the fraction that was correct?

Specificity (True Negative/All Negative)
Interpretation: Among those which were actually Class 0, Unmodified Images, what was the fraction that was correct?

Precision (True Positive/Predicted Positive)
Interpretation: Among those the model predicted to be Class 1, Modified Images, what was the fraction that was correct?

F1 score (2*(Recall * Precision) / (Recall + Precision))
Interpretation: F1 Score is the weighted average of Precision and Recall. Therefore, this score takes both false positives and false negatives into account.

ROC AUC score
One ROC curve was generated per model by varying the threshold from 0 to 1. Optimal threshold was determined to be 0.485. This led to slight but not significant improvements to the Confusion Matrix metrics, as the default threshold is 0.5, and the figures are close enough that not much changed.

---

## Conclusion and Recommendations

Given the relatively high accuracy of the model, it will be a good launchpad to explore improving it further. It can still be used in non-commercial settings, however, a higher accuracy would be needed for industry deployment.

This would require the access to much more computational power, which allows for images to be handled without being resized, and to handle transparency channels if needed.
More data needs to be fed in, perhaps original images taken from different angles, instead of bootstrapping.

The goal is also eventually be able to process video snippets. Note that the typical video is 60 frames per second, meaning 60 images per second, this would exponentially increase the storage, RAM and processing power needed.

I look forward to exploring the above further, and in conjunction with other methods such as masking and extracting parts of the image as pre-processing.

---
