# Project_machine_learning_Eva_Matthijs
machine learning project for microarray gene expression

## Organisation of the repository 
In our github repository you can find the different scripts for every part of the project. We decided to split up into different parts to maintain a better structure and to have a better overview of all the code we have written for every part of the project. The report will contain a discussion of the results and observation we obtained from the code. Under this README file u will be able to find more comments and approaches for every part of the coding process. We also would like to point out that in the written two pages report u would be able to find some graphs and results we used for certain decisions we made in the coding process. We will refer to them in the coding files if necessary. 

## Reproducibility 

## Data cleaning
We started the process of data cleaning by looking at the raw data and checking for any missing values. There were no missing values in the dataset, so no samples had to be removed from the data. 

The next important step we committed to was to remove genes that had a variance of 0. These genes didn’t come to expression in a single cell of the 5000 cells, so they won’t have any explanatory value in model training and the classification process. Deleting the unexpressed genes allowed us to reduce the dimension from 32285 predictors to 26226 predictors. 

Finally, we standardized the data with the built-in standardizing machine in Julia. Standardizing the data means that the original data is now transformed into a “new” dataset where for every predictor the mean is zero and the standard deviation is 1. This harmonization of the data now allows us to make more accurate machines for principal component analysis and regularization, because both of these approaches depend on data scaling.  

## Feature selection
In this section we tried to extract the predictors with the highest predictive value, form a new dataset with these and run a machine on this newly created dataset. The parameters with the highest predictive value were found as the predictors wherefor the absolute value of the coefficients in a model with L1 regularization were the highest. 

## Clustering
Finally, some cluster technologies were applied on the dataset. 
The first step in the analysis was trying to visualize the data and clusters. To do this the data had to be reduced from over 32000 predictors to only two variables that could be plotted against each other. The first and second principal component were chosen as these two variables. Plots were made with label colors obtained by k-means clustering and hierarchical clustering on the PCA data with 90 components.
Secondly, we tried to determine the number of clusters that can be distinguished in higher dimensions. For this analysis the PCA data with 140 components and the cleanen standardized data was used.


