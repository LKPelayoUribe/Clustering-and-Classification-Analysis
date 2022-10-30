# STAT 437 Project 1 Data Set Analysis
This research paper studies cancer prediction from gene expression data using clustering methods and classification methods.

### By: Shawn Petersen and Laura K. Pelayo Uribe

# Datasource, approach and cleaning.
The data used to test these methods is the Gene Expression Cancer RNA-Seq Data Set from UC Irvine Machine learning, https://archive.ics.uci.edu/ml/datasets/gene+expression+cancer+RNASeq#

The data analysis for this project uses the following algorithms to build models and analyze the results:

- K-Means Clustering
- Hierarchical Clustering
- Quadratic Discriminant Analysis
- K-Nearest Neighbors

The clustering methods, k-means and hierarchical, will be applied to determine how well the sample classes can be grouped into the models. For these experiments, all five cancer classes will be present. The classification algorithms, quadratic discriminant analysis, and k-nearest neighbors will be used to develop models that can be trained to classify the type of cancer a patient has from their gene expression testing. For the classification algorithms, two cancer classes, BRCA and LUAD , will be used, which will encompass a binary classification problem.

The goal of utilizing multiple feature sizes is to understand how the number of features impacts model test accuracy. When the models are trained, the accuracy of the models will be determined by the use of 2x2 prediction tables, ROC curves, and model accuracies calculations.

The data set contains 801 samples from patients with five cancer types are in the gene samples: BRCA , KIRC , COAD , LUAD , and PRAD . For each patient, they each have 20,531 gene expressions values. Using the information we have learned the past several weeks in STAT 437 class, we applied the four algorithms outlined in the introduction to the cancer data set. The data set was sampled with different number of genes to observe the results and if a small or larger sampled affected the results.

For this project, genes that contained less than 300 values of 0’s were selected for the data set. From the remaining set, 1000 genes were randomly selected for a more manageable data set to analyze with the various techniques. 30 samples were selected at random along with their cancer diagnosis labels. The data was also scaled to minimize the effects that relatively large values have on clustering metrics. One of them is Euclidean distance which calculates how dissimilar are two values in a cluster. Then two subsets of the cancer data were taken, one with 50 genes and the other with 250 genes, to compare if the number of features would improve the clustering results

# K-Means Clustering

# Hierarchical Clustering

# Quadratic Discriminant Analysis

# K-Nearest Neighbors

# Conclusion

Our analysis indicates that using more features does not necessarily give more accurate clustering or classification results. The clustering methods we applied to our data were k-means and hierarchical. K-means is redundant when we get k = 1 from our GAP, for both when our sample size is 50 and 250. Even when k = 5, it is hard to say both graphs make an impact in clustering analysis. K-means clustering was not a useful approach for clustering this data set. Hierarchical clustering does the best job overall for classification, specifically when we use our complete method to model our dendrogram. The classification methods we applied to our data were Quadratic Discriminant Analysis (QDA) and K-Nearest Neighbors (K-NN). With classification, more features did not give a more accurate result. QDA performed best with only 3 genes as features. The density plot for the 3-gene experiment was promising because there was a bimodal distribution and K-NN was more accurately able to classify. On the other hand, when QDA was performed with 100 genes as features, the distribution fails the Gaussian Mixture Model. There is simply too much of an exact overlap between the class observations. The distributions being almost identical, make it impossible for K-NN to accurately classify the genes with the cancer type. We may think more features to describe a data, will render more accurate clustering and classification, but it may be that too many features, create too much “noise” in our data.

**Final model analysis**
- K-Nearest Neighbors: 2.7% Error
- K-Means Clustering: 16.66% Error
- Hierarchical Clustering: 16.66% Error
- Quadratic Discriminant Analysis: 23.16% Error




