# **AIML 2024-2025 Project**

### **Team Members**
- **Vince Coppens**
- **Mateusz Waglowski**
- **Hamza Yazan Jamal**

---

## **Introduction**

This project explores a dataset titled `alien_galaxy.csv` to analyze patterns, preprocess data, and apply clustering techniques for insight extraction. The primary goal is to define the different types of alien species and their characteristics using various clustering methods. Before clustering, the dataset undergoes thorough exploration, imputation, and cleaning to ensure accurate analysis. By leveraging advanced data imputation, dimensionality reduction, and visualization tools, this project demonstrates the application of machine learning techniques to solve complex analytical tasks and derive actionable insights.

---

## **Methods**

### **Proposed Ideas**
- **Preprocessing**:
  - Missing data handled using `SimpleImputer` and `KNNImputer`.
  - Data standardized using `StandardScaler` and encoded using `OneHotEncoder`.
- **Dimensionality Reduction**:
  - PCA (Principal Component Analysis) applied to reduce features for clustering.
- **Clustering**:
  - Hierarchical clustering to group data based on patterns.
  - Evaluation metrics such as Silhouette Score and Calinski-Harabasz Index used to assess clustering quality.
- **Visualization**:
  - Missing data patterns visualized using `missingno`.
  - Data distribution explored with `seaborn` and `matplotlib`.

### **Flowchart**
![Flowchart](flowchart.png)