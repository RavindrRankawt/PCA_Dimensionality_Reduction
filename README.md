# PCA_Dimensionality_Reduction

This repository contains a micro project entitled "PCA on American's economy".

# Conda Virtual Environment
* conda create --name <environment_name> python=3
* conda activate <environment_name>
* conda install -c anaconda cmake pkg-config
* conda install matplotlib
* conda install numpy
* conda install pandas
* conda install scikit-learn

# Introduction
Principal Component Analysis(PCA), a dimensionality reduction approach, is the focus of this kernel. I've introduced PCA, explained variance ratio, and Logistic Regression combined with PCA, selecting the appropriate number of dimensions, and visualized the explained variance ratio against the number of dimensions. For this kernel, I've used the adult data set. This dataset is too tiny to be used for PCA. My goal is to use this dataset to illustrate PCA implementation.

# Dataset
Ronny Kohavi and Barry Becker (Data Mining and Visualization, Silicon Graphics) took this information out of the 1994 Census Bureau's database. Using the criteria ((AAGE>16) && (AGI>100) && (AFNLWGT>1) && (HRSWK>0) a collection of reasonably clean records was extracted. To anticipate if an individual earns more than $50,000 annually is the prediction task. Dataset has the dimension of 32561*15 (32561 instances and 15 attributes).

# Exploratory Data Analysis
The data collection consists of 32561 instances and 15 attributes.
The dataset's summary reveals that there are no missing values. However, the preview reveals that the collection includes values with the '?' coding. Therefore, represent '?' as NaN values.

The summary after encoding reveals that the variables for workclass, occupation, and native.country have blank values. These variables are all of the categorical variety. Therefore, we can see that there are no missing values in the dataset by impute the missing values with the value that occurs the most frequently- the mode.

# Logistic Regression using PCA
Scikit-Learn's PCA class uses the following code to implement the PCA technique.

* Explaned Variance Ratio - The explained variance ratio for each primary component is a very helpful statistic. The explained_variance_ratio_ variable makes it accessible. It displays the percentage of the dataset's variance that falls on each primary component's axis.

## PCA implementation
![Screenshot 2023-04-13 024436](https://user-images.githubusercontent.com/130180779/231616806-22c1fa04-56d4-4d41-872a-297f34347f41.jpg)

The first 13 factors, as can be seen, account for about 97.25% of the variance.
The last variable only explains 2.75% of the variance. Consequently, we can infer that it contains little information.
So, disregaring that, retrain the model, and determine correctness.

### Logistic Regression with first 13 features
![13](https://user-images.githubusercontent.com/130180779/231617259-3c7026e2-414e-4ba4-aa93-1eb2153e7671.jpg)

After the last feature was removed, accuracy fell from 0.8218 to 0.8213, as can be seen.
Now, if combine the last two attributes, we can see that they account for about 7% of variance.
Discard them, retrain the model, and determine accuracy.

### Logistic Regression with first 12 features
![12](https://user-images.githubusercontent.com/130180779/231617555-e1821587-2864-4f0a-abc7-39b6cb93926b.jpg)

Now, if the model is trained with 12 features, it can be seen that the accuracy has grown to 0.8227.
Finally, merge the final three characteristics. They explain roughly 11.83% of the variance.
Going through the procedure again, remove these features, train the model once more, and determine accuracy.

### Logistic Regression with first 11 features
![11](https://user-images.githubusercontent.com/130180779/231617805-73bc3368-2392-4cd2-be11-45245ffc79aa.jpg)

If removing the last three characteristics, we can observe that accuracy has considerably fallen to 0.8187.
Maximizing accuracy is our goal. With the first 12 features, we achieve the highest accuracy (0.8227).

### Right number of dimensions
If there are few dimensions, the above procedure performs effectively.
But if we have a lot of dimensions, it becomes really difficult.
Calculating the number of dimensions that can explain a sizably substantial fraction of the variance is therefore a better course of action.
The code below calculates PCA without lowering dimensionality, then determines the bare minimum number of dimensions needed to maintain 90% of the variance in the training set.

![dim](https://user-images.githubusercontent.com/130180779/231618147-57edd761-014e-4e19-9226-6471e6c12407.jpg)

### Variance ratio via a plot with the number of dimensions
![download](https://user-images.githubusercontent.com/130180779/231619014-9212cee9-3fd1-47b1-8e74-87ddf127fc72.png)

We should search for an elbow in the plot where the explained variance stops increasing quickly. Which is 12, as we can see.

# Conclusion
The most common method for dimensionality reduction, principal component analysis, is covered in this kernel. On the dataset, I have shown how to implement PCA using logistic regression. The maximum accuracy I could find using the first 12 features was 0.8227. It is discovered that 12 dimensions are necessary to preserve 90% of the variation, as predicted. The explained variance ratio is then plotted with the number of dimensions. The graph demonstrates that the top 12 components account for almost 90% of the volatility.
