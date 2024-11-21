# **AIML 2024-2025 Project**

### **Team Members**
- **Vince Coppens**
- **Mateusz Waglowski**
- **Hamza Yazan Jamal**

---

## **[Section 1] Introduction**

This project explores a dataset titled `alien_galaxy.csv` to analyze patterns, preprocess data, and apply clustering techniques for insight extraction. Using advanced data imputation and dimensionality reduction methods, the project demonstrates the application of machine learning and visualization tools for solving complex analytical tasks. The overarching goal is to preprocess, cluster, and visualize the dataset for better understanding and actionable insights.

---

## **[Section 2] Methods**

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

### **Environment**
The project requires the following setup:
1. Install necessary libraries:
   ```bash
   pip install pandas missingno seaborn matplotlib scikit-learn