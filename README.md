# **AIML 2024-2025 Project**
---
---

### **Team Members**
- **Vince Coppens**
- **Mateusz Waglowski**
- **Hamza Yazan Jamal**

---
---

## **Introduction**

This project explores a dataset titled `alien_galaxy.csv` to analyze patterns, preprocess data, and apply clustering techniques for insight extraction. The primary goal is to define the different types of alien species and their characteristics using various clustering methods. Before clustering, the dataset undergoes thorough exploration, imputation, and cleaning to ensure accurate analysis. By leveraging advanced data imputation, dimensionality reduction, and visualization tools, this project demonstrates the application of machine learning techniques to solve complex analytical tasks and derive actionable insights.

---
---

## **Methods & Experimental design**
---

### **Libraries**
Installing and importing all necessary Python libraries.

---

### **Import and Prepare Dataset** - Vince Coppens

The dataset alien_galaxy.csv was imported and the variables were reviewed to understand their representations and identify whether they were numerical or categorical. No duplicate rows were identified during this process.

The missingno library was used to visualize missing values in the dataset. This analysis revealed that only 0.03% of the rows were complete, and each column was missing approximately 10% of its data. Since dropping rows would result in significant data loss, it was decided that the missing values would need to be imputed.

The Discovery_Date variable, originally a string, was converted to a timestamp format and standardized for consistency. Correlation values between variables were calculated and, although they were generally low, these correlations were stored in a dataframe for future use. Additionally, a custom function was created to easily plot the distributions of variables, enabling a more straightforward examination of their characteristics.

---

### **Imputing data** - Vince Coppens
First, the categorical variables in the dataset were transformed. Missing values in these variables were imputed using the most_frequent strategy to ensure consistency. After imputation, one-hot encoding was applied to convert categorical variables into a numerical format suitable for analysis. For categorical variables with an inherent order, level coding was used to preserve their ordinal nature.
#### **Imputing dataset using the distributions**
The distributions of the variables were plotted to better understand their characteristics. Binomial and multinomial distributions were easy to recognize visually, while the other distributions were more challenging to identify. For these, a custom function was used to determine the most likely distributions based on likelihood estimation.

Once the distributions were identified, missing values were imputed using the corresponding distributions to maintain consistency with the data’s natural variability. After imputation, the correlations between variables were reassessed, revealing a significant drop in their values.

#### **Imputing dataset using KNN imputer**
As the initial imputation approach led to a significant loss of information (lower correlations), KNN imputation was explored as an alternative to better preserve relationships between variables. After imputing the missing values, a pairplot was generated to visualize variable interactions and identify any remaining issues.

While correlations are less critical for clustering, highly correlated variables can unnecessarily complicate the model.

Outliers were removed to improve data quality and ensure a more balanced dataset. A range_multiplier of 3 was chosen instead of the standard 1.5, as the latter would have eliminated an excessive number of values. Using this approach, approximately 11% of the dataset was removed. Binary variables with an overwhelming majority of 0 values were excluded from the interquartile range (IQR) filtering, as their IQR was 0. Including these variables would have caused a substantial loss of data, so they were specifically handled to preserve the dataset’s integrity.

Additionally, binary variables with minimal variability (near-constant behavior) were identified and removed to simplify the dataset further.

This time, correlations were better preserved, providing a more consistent and reliable foundation for subsequent analysis.

---
### **Clustering**
............................................
#### **Hierarchical clustering** - Vince Coppens
To explore clustering in the dataset, linkage matrices were generated using different linkage methods (single, complete, average, and ward). The elbow method, particularly for the ward linkage, suggested setting the number of clusters to 4. Based on this, clusters were generated, and dendrograms were plotted to visualize the hierarchical structure.

![](Images/linkagematrix.png)
![](Images/dendrogram.png)

An attempt was made to find a link between the alien_civilization_level variable and the clusters. However, no clear relationship was observed. Plotting the relative counts for this variable might provide better insights in the future.

![](Images/CorrelationAlienHierarchical.png)

Dimensionality reduction was performed using PCA to visualize the clusters. In the 2D visualization, clusters were distinguishable, with Exploration_Missions and Young_Colonies emerging as the most significant variables contributing to the clusters. For further clarity, a 3D visualization was also created, where clusters were even more clearly defined. The key variables in the 3D space were Exploration_Missions, Young_Colonies, and Military_Engagements.

![](Images/2DPCA.png)
![](Images/3DPCA.png)

To evaluate cluster quality, hyperparameter tuning was conducted using the Calinski-Harabasz Index. This metric, also known as the Variance Ratio Criterion, measures the quality of clustering by comparing between-cluster dispersion (how distinct clusters are from one another) to within-cluster dispersion (how compact clusters are). A higher Calinski-Harabasz Index indicates better-defined clusters with clear separation and tight groupings. Hierarchical Clustering models were tested with various linkage methods (ward, complete, average, single), distance metrics (euclidean, manhattan, cosine), and different numbers of clusters to identify the best-performing configuration. The picture below shows the clusters in 3D. The results, including the typical characteristics of the clusters as they currently appear, will be described in detail in the results section.

![](Images/3DPCA_hyper.png)

............................................
### **Gaussian Mixture Model (GMM)** 

To explore clustering in the dataset, GMM models were generated using different covariance types (full, spherical, diagonal, tied). The optimal number of components was determined using the silhouette score, which suggested setting the number of components to 4 for full covariance. Based on this, clusters were generated, and visualizations were plotted to showcase the clustering structure.

![BIC Score vs. Number of Components for GMM](Images/BIC_GMM.png)
![Silhouette Score vs. Number of Components for GMM](Images/optimalclusterGMM.png)

An attempt was made to analyze the relationship between the Alien_Civilization_Level variable and the GMM clusters. A clear pattern was observed, with some civilization levels showing distinct representation across specific clusters, suggesting that the clusters may capture meaningful distinctions related to civilization levels. This indicates that GMM clustering might be successfully identifying patterns within civilization levels.

![Correlation between Alien Civilization Level and GMM Clustering](Images/correlationGMM.png)

Dimensionality reduction was performed using PCA to visualize the clusters. In the 2D visualization, clusters were distinguishable, with Trade_Activity and Exploration_Missions being the most significant variables contributing to the clusters. For further clarity, a 3D visualization was also created, where clusters were even more clearly defined. The key variables in the 3D space were Trade_Activity, Young_Colonies, and Military_Engagements.

![2D PCA GMM Clustering](Images/2dpcaGMM.png)
![3D PCA GMM Clustering](Images/3dpcaGMM.png)

To evaluate cluster quality, hyperparameter tuning was conducted using the Silhouette Score. This metric measures how similar an object is to its own cluster compared to other clusters. A higher Silhouette Score indicates better-defined clusters with clear separation and tight groupings. Gaussian Mixture Models were tested with various covariance types and different numbers of components to identify the best-performing configuration. The picture below shows the clusters in 2d. The results, including the typical characteristics of the clusters as they currently appear, are described in detail in the results section.

![3D PCA GMM Clustering after Hyperparameter Tuning](Images/2dpca_hyperGMM.png)

---

### **Performance Metrics used**

- **Calinski-Harabasz Index**
Measures clustering quality by comparing between-cluster dispersion (how distinct clusters are from one another) to within-cluster dispersion (how compact clusters are). A higher Calinski-Harabasz Index indicates better-defined clusters with clear separation and tight groupings.

- **Silhouette Score**
Assesses how similar an object is to its own cluster compared to other clusters. A higher Silhouette Score indicates better-defined clusters with clear separation and tight groupings.

- **Elbow Method**
Evaluates the variance explained as the number of clusters increases, aiding in selecting the optimal number of clusters by identifying the "elbow" point where additional clusters offer diminishing returns.

- **Bayesian Information Criterion (BIC)**
Used to determine the optimal number of components in Gaussian Mixture Models by balancing model fit and complexity. Lower BIC values indicate better-performing models.

---

---

## **Results**

Please refer to the notebook for a detailed overview of the defining cluster variables and their corresponding values, as we aimed to keep this report concise.

---

#### **Results Hierarchical clustering** - Vince Coppens
3 clusters, euclidian distance, ward linkage
- **Cluster 1** represents the least developed civilizations with minimal resources and activity.
- **Cluster 2** includes civilizations with intermediate development and moderate resource utilization.
- **Cluster 3** features advanced civilizations with high trade and production activity.
- **Cluster 4** represents the peak of development with the largest populations, highest energy consumption, and extensive resource utilization.

#### **Hyperparameter tuning Hierarchical clustering** - Vince Coppens
2 clusters, cosine distance, complete linkage
- **Cluster 1** represents civilizations with moderate development, reflecting limited energy and resource consumption.
- **Cluster 2** includes advanced civilizations with higher populations, resource use, and production capacities.

............................................
#### **Results GMM**
- **Cluster 0** represents civilizations with moderate development levels, focusing on biological research and moderate resource extraction while having minimal engagement in peace treaties.
- **Cluster 1** characterizes highly developed civilizations with significant energy use, technological advancements, and resource extraction activities, indicating a focus on industrial growth.
- **Cluster 2** represents civilizations with moderate development, focusing on expanding young colonies and maintaining strong social structures, particularly in married relationships.
- **Cluster 3** includes advanced civilizations with high technological progress, significant mining activities, and a strong focus on resource utilization, coupled with a balanced approach to agriculture.


#### **Hyperparameter tuning GMM**
- **Cluster 0** represents civilizations at a moderate development level, balancing population, resources, and economic activities.
- **Cluster 1** depicts highly developed civilizations with extensive use of resources, higher population, and sophisticated industrial activities.
- **Cluster 2** represents minimally developed civilizations with small populations, limited resource consumption, and basic economic activities.

---
---

## **Conclusions**

---

### **One paragraph conclusion**

lorum ipsum

---

### **Futere improvements**


This project provides valuable insights into clustering alien civilizations and finding patterns in their characteristics, but some questions remain unanswered. For example, the lack of a clear link between the clusters and the Alien_Civilization_Level variable raises doubts about whether this variable is suitable for defining civilization types. A useful next step could be to study the relative percentage of each Alien_Civilization_Level type in each cluster to see if any hidden patterns emerge. Also, understanding the clusters in terms of civilization development is still a challenge, as the current patterns may not fully capture the complexity of the data. Future work could add more relevant features or use knowledge from experts to make the clusters more meaningful. Trying different clustering methods, improving feature selection, or using supervised learning to check the clusters against known benchmarks could make the results stronger and more useful.

---