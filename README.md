# project_machine_learning_Eva_Matthijs
machine learning project for microarray gene expression

## organisation of the repository 
In our github repository you can find the different scripts for every part of the project. We decided to split up into different parts to maintain a better structure and to have a better overview of all the code we have written for every part of the project. The report will contain a discussion of the results and observation we obtained from the code. Under this README file u will be able to find more comments and approaches for every part of the coding process. 

## reproducibility 

## Feature selection
In this section we tried to extract the predictors with the highest predictive value, form a new dataset with these and run a machine on this newly created dataset. The parameters with the highest predictive value were found as the predictors wherefor the absolute value of the coefficients in a model with L1 regularization were the highest. 

## Clustering
Finally, some cluster technologies were applied on the dataset. 
The first step in the analysis was trying to visualize the data and clusters. To do this the data had to be reduced from over 32000 predictors to only two variables that could be plotted against each other. The first and second principal component were chosen as these two variables. Plots were made with label colors obtained by k-means clustering and hierarchical clustering on the PCA data with 90 components.
Secondly, we tried to determine the number of clusters that can be distinguished in higher dimensions. For this analysis the PCA data with 140 components and the cleanen standardized data was used.


