# Neural Network Charity Analysis

## Overview of the Analysis
The goal of this week's analysis was to use machine learning and neural networks to accurately predict what charity requests our foundation should invest in and those to avoid.  Using the features of the data set, we attempted to preprocess the data and build a neural network as a baseline, then optimize the results by modifying parameters of the model.  The target was 75% accuracy.

## Results

### Preprocessing
- Our target variable is the "IS_SUCCESSFUL" column of data.  We want to know if we invest the money into whatever request is being made by that individual or organization, were they successful in what they were hoping to accomplish with the funds.
- The features of the model are: application type, affiliation, classification, use case, organization type, active status, income classification, whether or not the application requested a special consideraiton, and the amount being requested.
- The EIM and Name variables are neither targets nor features and can be dropped.  In this case, those variables are likely unique to each row of data and will provide no information to the model that we build.

### Compiling, Training, and Evaluating the Model

The below table summarizes the results of the 9 different variations I attempted in order to reach 75% accuracy, with my best results highlighted in green:

![Summary Table](/Resources/summary_table.png)

I used what we did in Deliverable 2 (2 hidden layers) as my baseline and elected to use 80 and 30 nodes for layers 1 and 2 respectively.  The rule of thumb from the module was 2 to 6 nodes per input, and in this case we had 43 columns in our features dataframe so I used 80 (x2) as a starting point.  I then chose a number slightly less than half of that for the second layer.  I used the Relu node activation for the baseline.  I got 56% accuracy.  That is Attempt 0 on the table.

Then, for Deliverable 3, I tried to make different changes to the model in order to increase accuracy:
1. For Attempt 1, I used the same model functions but went back and consolidated more of the different Application Type/Classification categories into the Other bucket.  Accuracy went down, which told me there was valuable information in the delineation of data in those columns.
2. In Attempt 2, I used the baseline data but added more nodes to each layer and got significantly better results (69%).  
3. In Attempt 3, I attempted to increase the node count even further but accuracy went down (was still better than baseline).
4. In Attempt 4, I webt back to the settings from my best result so far and tried adding a third hidden layer with about half of the nodes as the second layer (100/50/20 nodes per layer respectively) but accuracy was lower than Attempt 2.
5. Attempt 5 I tried a different activation function for the nodes and used the same settings as Attempt 2.  Accuracy was not as good.
6. For Attempts 6 and 7 I tried a cople different settings (more or less layers, different node settings) and got worse results than the baseline.

For all of the prior attempts, I only had one attempt that did significantly better than baseline.  Knowing that neural networks can be thrown off by outlier data, I revisited the topic of data cleanup and attempted to clean the data even more (consolidate categories, drop variables that offered little data):
- Of the Organization types, Co-operative and Corporation were a very small percentage of the overall values so I consolidated them into an OTHER bucket.
- Similarly, in the USE CASE category Community Service, Health Care, and Other were very small percentages of the overall category and I consolidated them into a single OTHER bucket as well.
- Looking at INCOME AMT, I consolidated a lot of the ultra-high amounts into an OTHER bucket.
- I dropped both the ASK_AMT and STATUS columns.  A little more than half of the Ask Amount was 5000 and then the rest of the values were individual amounts that ranged from 5,001 to millions.  And only 5 of the data points in STATUS were 0, the rest were 1.  Effectively it didn't offer much to the data.

I then reran the model using baseline settings but on the cleaner data:
1. Attempt 8 was baseline on clean data and accuracy went up to 71%
2. On Attempt 9 I decreased the number of nodes on the clean data set and got 62% accuracy.

I stopped at this point, given the time constraint.  I was not able to hit the 75% accuracy but assume that I would be able to if I either continue to tweak the model parameters on this new clean data set or go back and modify the data preprocessing further and rerun.

## Summary

In summary, while I was not able to achieve the 75% target accuracy, I was able to get much better performance than the Deliverable 2 baseline results by further preprocessing the data and modifying the parameters of the neural network.  

I would recommend attempting to use a random forest model to predict the outcomes on this data set and then compare the accuracy results of the test versus the neural network.  In this case, when I was doing the additional preprocessing between attempts 7 and 8, I did not consider the proportion of those dropped data columns relative to the target variable.  For example, I dropped the STATUS column because there were only 5 of ~40K rows that were STATUS = 0.  However, if there were only 5 unsuccessful campaigns and all 5 were STATUS = 0, something like a decision tree could easily identify that.  A random forest could better handle some of the categorical variables as-is and might discover useful patterns in the data points we ended up consolidating/dropping to make the data easier for the neural network to process.
