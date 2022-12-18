# Project_machine_learning_Eva_Matthijs
machine learning project for microarray gene expression

## Organisation of the repository 
In our github repository you can find the different scripts for every part of the project. We decided to split up into different parts to maintain a better structure and to have a better overview of all the code we have written for every part of the project. The report will contain a discussion of the results and observation we obtained from the code. Under this README file u will be able to find more comments and approaches for every part of the coding process. We also would like to point out that in the written two pages report u would be able to find some graphs and results we used for certain decisions we made in the coding process. We will refer to them in the coding files if necessary. 

## Reproducibility 

## Data cleaning
We started the process of data cleaning by looking at the raw data and checking for any missing values. There were no missing values in the dataset, so no samples had to be removed from the data. 

The next important step we committed to was to remove genes that had a variance of 0. These genes didn’t come to expression in a single cell of the 5000 cells, so they won’t have any explanatory value in model training and the classification process. Deleting the unexpressed genes allowed us to reduce the dimension from 32285 predictors to 26226 predictors. 

Finally, we standardized the data with the built-in standardizing machine in Julia. Standardizing the data means that the original data is now transformed into a “new” dataset where for every predictor the mean is zero and the standard deviation is 1. This harmonization of the data now allows us to make more accurate machines for principal component analysis and regularization, because both of these approaches depend on data scaling.

## Data preparation
Now after the data cleaning it’s still clear we’re working with a dataset where the number of samples is way smaller than the number of predictors (n<<p). The big problem with this kind of dataset is overtraining of the training data. In other words, a linear model will perfectly fit the training data, leading to a poorer classification accuracy of the test data. Now as seen in the lectures there are several dimension reduction tactics to create a dataset where the number of samples is bigger than the number of predictors (n>p). In this project we applied 2 different tactics: feature selection and dimensional reduction with PCA.  

### Feature selection
In this section we tried to extract the predictors with the highest predictive value, form a new dataset with these and run a machine on this newly created dataset. The parameters with the highest predictive value were found as the predictors wherefor the absolute value of the coefficients in a model with L1 regularization were the highest. 

### Dimensional reduction using principal components 
Principal components allow us to reshape the original dataset (after data cleaning) to a set with a smaller number of predictors that collectively explain most of the variability in the original dataset. The next challenge we now had to deal with was finding the proper number of principal components to obtain the best model to work with.  The first step in the search for a good number of principal components was by plotting the number of principal components with cumulative explained variance and the proportion of variance explained by every component (results see figures below).

![Cumulative variance explained](https://user-images.githubusercontent.com/114157780/208315814-92bb1e0c-f80e-40aa-866d-1e4b9c3ef4a3.png)
![proportion of variance](https://user-images.githubusercontent.com/114157780/208315823-b3bb8272-7ebd-422b-a397-fd8668b6f5ec.png)

After iterative fitting some classification machines we made the remarkable observation that 3000 principal components had the same validation accuracy as 140 principal components, meaning that at least 80 precent of the explained variance by 3000 principal components is unexplainable for the classification process. In this kind of dataset, it’s reasonable to find such a big amount of unexplainable variance because every cell is different and so is the amount of expression of the genes in every cell. As a matter of fact, we could notice that a lower number of principal components had a good validation accuracy on the validation set without overtraining on the training set (results figures below).
As seen on the figures there is some sort of saturation of the validation accuracy when we grow the number of principal components. By taking a lower number of principal components we can simplify the machine, have a lower training accuracy and the same validation accuracy. For these reasons we decided to work in a range of 130 to 150 principal components in further data analysis.

![training_accuracy](https://user-images.githubusercontent.com/114157780/208315896-ebb048f7-e9fc-49b1-8d4d-2d15887639e8.png)
![validation_accuracy](https://user-images.githubusercontent.com/114157780/208315910-c638ba87-4f70-4fc3-beab-6a049baeaa42.png)

## Clustering
Finally, some cluster technologies were applied on the dataset. 
The first step in the analysis was trying to visualize the data and clusters. To do this the data had to be reduced from over 32000 predictors to only two variables that could be plotted against each other. The first and second principal component were chosen as these two variables. Plots were made with label colors obtained by k-means clustering and hierarchical clustering on the PCA data with 90 components.
Secondly, we tried to determine the number of clusters that can be distinguished in higher dimensions. For this analysis the PCA data with 140 components and the cleanen standardized data was used.


