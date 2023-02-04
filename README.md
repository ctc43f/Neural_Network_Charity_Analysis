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
- 
