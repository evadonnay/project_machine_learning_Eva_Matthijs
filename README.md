# Project_machine_learning_Eva_Matthijs
machine learning project for microarray gene expression

## Organisation of the repository 
In our github repository you can find the different scripts for every part of the project. We decided to split up into different parts to maintain a better structure and to have a better overview of all the code we have written for every part of the project. The report will contain a discussion of the results and observation we obtained from the code. In this README file you can find some brief explinations of some of the steps we have taken. Something really important we have to clear out is that a lot of the code is written with deleted colmuns (columns where variance was zero). Some time later we had noticed some dimensional problems when we wanted to do the same approach on the test set, because some genes that came to expression in the training data, didn't come to expression in the test set. So what we did to solve this is standardizing both training and test set and putted the NaN (not a number value) to zero. This has no effect on the earlier determined lambda by the tuned model and the variance explained by the PC's where we deleted the zero value columns of the training set. This approach allowed the trained machine to work in the same dimensions for training and test set.

## Reproducibility 
In the map reproducibility u can find the envirnoment we worked with for all the coding. We have chosen to work with the MLCourse environment and we haven't downloaded any extra packages that were not included in the MLCourse environment. Also, we worked with standardization zo we have to use the same standardization values for training as for testing data. The formule we used for this is available in the folder data cleaning. 

## Data cleaning
We started the process of data cleaning by looking at the raw data and checking for any missing values. There were no missing values in the dataset, so no samples had to be removed from the data. 

The next important step we committed to was to remove genes that had a variance of 0. These genes didn’t come to expression in a single cell of the 5000 cells, so they won’t have any explanatory value in model training and the classification process. Deleting the unexpressed genes allowed us to reduce the dimension from 32285 predictors to 26226 predictors. 

Finally, we standardized the data with the built-in standardizing machine in Julia. Standardizing the data means that the original data is now transformed into a “new” dataset where for every predictor the mean is zero and the standard deviation is 1. This harmonization of the data now allows us to make more accurate machines for principal component analysis and regularization, because both of these approaches depend on data scaling.

## Data preparation
Now after the data cleaning it’s still clear we’re working with a dataset where the number of samples is way smaller than the number of predictors (n<<p). The big problem with this kind of dataset is overtraining of the training data. In other words, a linear model will perfectly fit the training data, leading to a poorer classification accuracy of the test data. Now as seen in the lectures there are several dimension reduction tactics to create a dataset where the number of samples is bigger than the number of predictors (n>p). In this project we applied 2 different tactics: feature selection and dimensional reduction with PCA.  

### Feature selection
In this section we tried to extract the predictors with the highest predictive value, form a new dataset with these and run a machine on this newly created dataset. The parameters with the highest predictive value were found as the predictors wherefor the absolute value of the coefficients in a model with L1 regularization were the highest. 

### Dimensional reduction using principal components 
Beginning of the code is to produce the graphes given below. The interpretation of these graphs is discussed in the report.

![Cumulative variance explained](https://user-images.githubusercontent.com/114157780/208315814-92bb1e0c-f80e-40aa-866d-1e4b9c3ef4a3.png)
![proportion of variance](https://user-images.githubusercontent.com/114157780/208315823-b3bb8272-7ebd-422b-a397-fd8668b6f5ec.png)

Second part of the code is used to produce the graphs given below. These results are also discussed in the report.

![training_accuracy](https://user-images.githubusercontent.com/114157780/208315896-ebb048f7-e9fc-49b1-8d4d-2d15887639e8.png)
![validation_accuracy](https://user-images.githubusercontent.com/114157780/208315910-c638ba87-4f70-4fc3-beab-6a049baeaa42.png)

## non linear model
We have chosen to work with a neural network classifier for the prediction of the test set. We made this decision based on some trial and error with different methods like a tree classifier, random forest classifier and neural networks. We found the best classification accuracy for neural networks. We also noticed a better accuracy for one hidden layer, making the hyperparameter tuning process a bit easier. We worked with PC's for the neural network with output dimension 140. The reason we have chosen 140 dimensions is discussed in the report and can be derived from the graphs given above. 

## Clustering
Finally, some cluster technologies were applied on the dataset. 
The first step in the analysis was trying to visualize the data and clusters. To do this the data had to be reduced from over 32000 predictors to only two variables that could be plotted against each other. The first and second principal component were chosen as these two variables. Plots were made with label colors obtained by k-means clustering and hierarchical clustering on the PCA data with 90 components.
Secondly, we tried to determine the number of clusters that can be distinguished in higher dimensions. For this analysis the PCA data with 140 components and the cleanen standardized data was used.


