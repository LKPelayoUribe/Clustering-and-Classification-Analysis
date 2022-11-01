# Clustering-and-Classification-Analysis
### By: Shawn Petersen and Laura K. Pelayo Uribe
This research paper studies cancer prediction from gene expression data using clustering methods and classification methods.

## Datasource, approach and cleaning.
The data used to test these methods is the gene expression cancer RNA-Seq. (2016). UCI Machine Learning Repository, https://archive-beta.ics.uci.edu/ml/datasets/gene+expression+cancer+rna+seq

The data analysis for this project uses the following algorithms to build models and analyze the results:

- K-Means Clustering
- Hierarchical Clustering
- Quadratic Discriminant Analysis
- K-Nearest Neighbors

The clustering methods, k-means and hierarchical, will be applied to determine how well the sample classes can be grouped into the models. For these experiments, all five cancer classes will be present. The classification algorithms, quadratic discriminant analysis, and k-nearest neighbors will be used to develop models that can be trained to classify the type of cancer a patient has from their gene expression testing. For the classification algorithms, two cancer classes, BRCA and LUAD , will be used, which will encompass a binary classification problem.

The goal of utilizing multiple feature sizes is to understand how the number of features impacts model test accuracy. When the models are trained, the accuracy of the models will be determined by the use of 2x2 prediction tables, ROC curves, and model accuracies calculations.

The data set contains 801 samples from patients with five cancer types are in the gene samples: BRCA , KIRC , COAD , LUAD , and PRAD . For each patient, they each have 20,531 gene expressions values. Using the information we have learned the past several weeks in STAT 437 class, we applied the four algorithms outlined in the introduction to the cancer data set. The data set was sampled with different number of genes to observe the results and if a small or larger sampled affected the results.

For this project, genes that contained less than 300 values of 0’s were selected for the data set. From the remaining set, 1000 genes were randomly selected for a more manageable data set to analyze with the various techniques. 30 samples were selected at random along with their cancer diagnosis labels. The data was also scaled to minimize the effects that relatively large values have on clustering metrics. One of them is Euclidean distance which calculates how dissimilar are two values in a cluster. Then two subsets of the cancer data were taken, one with 50 genes and the other with 250 genes, to compare if the number of features would improve the clustering results

## K-Means Clustering

To determine the best k value, two methods were incorporated. The first method was to compute the k-value using the gap statistic method which is implemented using the clusGap function. This technique uses the output of the clustering algorithm by comparing the change in within-cluster dispersion with the expected null distribution. Using this method to determine the best fit k for both the 50-gene experiment and 250-gene experiment, yielded a k=1. Using a k=1, as seen in **Figure 1** and **Figure 2** below, all gene samples were grouped into the same cluster for both the 50 and 250 gene samples with no clear groupings. The 2 genes selected (gene_7998, gene_322) were from the first 2 columns of the data set.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/K%3D1.PNG">

The elbow method was used to estimate k. With this method, the k-means algorithm was with kvalues from 1 to 10. With each iteration of k, the total within-cluster sum of squares was calculated and plotted. Seen below in **Figure 3** and **Figure 4**.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/elbow.PNG">

Both the 50-gene and 250-gene plots display the majority of the benefits as k is increased are maximized when k=5. The k-means algorithm was then re-run with the new estimates for k=5. The results on both subsets(50 & 250 genes) are seen below in **Figure 5** and **Figure 6**.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/K%3D5.PNG">

The 50-gene and 250-gene experiments with K=5 had the same classification error, 14/30=43.66% of samples present in clusters that did not match the in-cluster class majority, as seen in **Table 1** and **Table 2** below.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/K_class_error.PNG">

## Hierarchical Clustering

Hierarchical Clustering was calculated for the 250-gene subset with single, average, and complete linkages. The cut height calculation to obtain 5 clusters was performed for the average linkage experiment. The cut height to obtain 5 clusters with average linkage was calculated to be 20.96. The complete linkage had the best performance with 16.6%(5/30) of the samples located in a cluster not matching the within-cluster majority.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/single.PNG">
<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/avg.PNG">
<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/complete.PNG">

## Quadratic Discriminant Analysis

The data was cleaned and a subset was created for classification analysis as follows:
Gene expressions that contained less than 300 values of 0 were part of the final data set
1000 genes were randomly sampled
All samples with a class label of LUAD or BRCA were extracted along with their
corresponding class labels, 441 observations
QDA was applied to the two subsets of the data, one contained 3 genes and the other
containing 100 genes.
For the 3-gene experiment, 60% of the samples were selected at random for training the model
with the other 40% used for testing
For the 100-gene experiment, 75% was used for training with 25% used for testing
For each model, two procedures were used, correlation and Gaussian Mixture, as part of the
linear and quadratic discriminant analysis, which, requires that each observation follows a
Gaussian distribution.

1. Correlations between each pair of variables were calculated to find pairs that correlated above 0.9. Any gene pairs which correlated above this value were to be removed from the data set. Some gene pairs had a good correlation but no samples exceeded the >0.9 limits. The correlation plots for both the 3-gene experiment and the 100-gene experiment are seen below in **Figure 10** and **Figure 11**

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/corr_analysis.PNG">

2. The Gaussian Mixture Model assumption, which determines whether each set of class observations is normally distributed. To visualize this, density plots were created for each set of class observations. During my investigation of Gaussian Mixture models they are used for representing Normally Distributed subpopulations within an overall population. The density plots for both classes, for both the 3-gene and 100-gene experiments, are seen below in **Figure 12** and **Figure 13**

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/gaussian_mix.PNG">

Analysis:
1. 3-genes
- The density plot appears to be normally distributed data for both classes
- Have feature mixtures in each cancer class are bi-modal and overlapped

2. 100-genes
- The density plot does not have normally distributed data(left skewed)
- Both cancer classes exhibit highly irregular distributions, and appear to be unimodal with a significant amount of overlap between the classes

3. Final outcome
- The distributions of the class observations for the 100-gene violates the Gaussian Mixture Model assumption while the 3-gene experiment does not.

The model test accuracy showed that the ROC experiment had a 23.16% error rate, with an AUC of 0.786. The model built for the 100-gene subset performed slightly worse with an error rate of 24.32% and an AUC of 0.907.

Below are the QDA 2x2 classification error tables, **Table 3** and **Table 4**.
- 3-genes classification error = 32.38% (41/127)
- 100-genes classification error = 32.14% (27/84)
Between the 3 gene and 100 gene experiments, both have virtually the same classification errors.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/QDA_2X2.PNG">

## K-Nearest Neighbors

In the K-nearest neighbor analysis for classification, the most accurate result is when k = 3. In **Figure 12** the Gaussian distribution when k = 3 overlaps less than in **Figure 13**, when k = 100. Both do not follow an exact Gaussian model but when k = 100, the distributions are identical, making it difficult for the k-nearest neighbor to accurately classify the genes with the cancer type. Finally, our ROC curve when k = 3 reinforces its accuracy compared to the ROC curve when k = 100. When k = 3 we get an elbow shape curve, indicating the connection between sensitivity and specificity, which is more efficient. In **Figure 15**, when k = 100, the ROC curve is ineffective, just reinforcing what was found in the Gaussian distribution when k = 100. Reviewing the classification error results, this classification method performed the best with an error rate of 2.7% (3/108) as seen below in **Table 5**.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Gene-Expression-Cancer-RNA-Seq/main/KKN_pred_table5.PNG">

## Conclusion

Our analysis indicates that using more features does not necessarily give more accurate clustering or classification results. The clustering methods we applied to our data were k-means and hierarchical. K-means is redundant when we get k = 1 from our GAP, for both when our sample size is 50 and 250. Even when k = 5, it is hard to say both graphs make an impact in clustering analysis. K-means clustering was not a useful approach for clustering this data set. Hierarchical clustering does the best job overall for classification, specifically when we use our complete method to model our dendrogram. 

The classification methods we applied to our data were Quadratic Discriminant Analysis (QDA) and K-Nearest Neighbors (K-NN). With classification, more features did not give a more accurate result. QDA performed best with only 3 genes as features. The density plot for the 3-gene experiment was promising because there was a bimodal distribution and K-NN was more accurately able to classify. On the other hand, when QDA was performed with 100 genes as features, the distribution fails the Gaussian Mixture Model. There is simply too much of an exact overlap between the class observations. The distributions being almost identical, make it impossible for K-NN to accurately classify the genes with the cancer type. 

We may think more features to describe a data, will render more accurate clustering and classification, but it may be that too many features, create too much “noise” in our data.

**Final model analysis**
- K-Nearest Neighbors: 2.7% Error
- K-Means Clustering: 16.66% Error
- Hierarchical Clustering: 16.66% Error
- Quadratic Discriminant Analysis: 23.16% Error
