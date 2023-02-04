# Neural Network Charity Analysis

## Overview of the Analysis
The goal of this week's analysis was to use machine learning and neural networks to accurately predict what charity requests our foundation should invest in and those to avoid.  Using the features of the data set, we attempted to preprocess the data and build a neural network as a baseline, then optimize the results by modifying parameters of the model.  The target was 75% accuracy.

## Results

### Preprocessing
- Our target variable is the "IS_SUCCESSFUL" column of data.  We want to know if we invest the money into whatever request is being made by that individual or organization, were they successful in what they were hoping to accomplish with the funds.
- The features of the model are: application type, affiliation, classification, use case, organization type, active status, income classification, whether or not the application requested a special consideraiton, and the amount being requested.
- The EIM and Name variables are neither targets nor features and can be dropped.  In this case, those variables are likely unique to each row of data and will provide no information to the model that we build.

### Compiling, Training, and Evaluating the Model

The below table summarizes the results of the 9 different variations I attempted in order to reach 75% accuracy:

![Summary Table](/Resources/summary_table.png)
