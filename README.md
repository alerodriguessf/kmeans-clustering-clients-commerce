

# **Portfolio -  Clustering Model (KMeans) for Customer Segmentation**

This repository provides a comprehensive implementation of a customer segmentation analysis using the KMeans clustering algorithm. The project's objective is to explore a transactional dataset, perform advanced preprocessing, and derive meaningful customer clusters based on RFM (Recency, Frequency, Monetary) metrics. This detailed segmentation enables businesses to design targeted marketing campaigns, improve customer retention, and optimize resource allocation.

-----

## **Table of Contents**

1.  Project Overview
2.  Setup and Installation
3.  Dataset Description
4.  Methodology and Project Steps
      - Step 1: Exploratory Data Analysis (EDA)
      - Step 2: Data Preprocessing and Feature Engineering
      - Step 3: RFM-Based Clustering Analysis
      - Step 4: Cluster Profiling and Visualization
      - Step 5: Strategic Business Recommendations
5.  Technologies Used
6.  How to Use
7.  Future Improvements
8.  Contributors

-----

## **Project Overview**

Customer segmentation is a critical component of data-driven marketing. This project applies the KMeans clustering technique to segment customers based on their purchasing behavior, quantified by RFM metrics. The project follows a structured pipeline from data exploration to the delivery of actionable business strategies.

  - **Exploratory Data Analysis (EDA)**: Initial investigation of the data's structure, distributions, and quality using statistical summaries and visualization.
  - **Data Preprocessing**: Rigorous cleaning of the dataset, including handling missing values, removing outliers, and transforming data types for consistency.
  - **Feature Engineering**: Calculation of Recency, Frequency, and Monetary (RFM) metrics from raw transactional data to serve as the basis for clustering.
  - **Clustering Analysis**: Systematic determination of the optimal number of clusters using multiple validation metrics, followed by the application of the KMeans algorithm.
  - **Business Recommendations**: Formulation of targeted strategies based on the distinct data-backed profiles of each identified customer segment.

-----

## **Setup and Installation**

To run the project locally, please ensure the following prerequisites are met.

### **Prerequisites**:

  - Python 3.8 or higher
  - Jupyter Notebook or Google Colab (Recommended for interactive analysis)
  - Required libraries can be installed via pip:

<!-- end list -->

```bash
pip install pandas numpy seaborn plotly matplotlib sidetable yellowbrick ydata-profiling scikit-learn
```

### **Files**:

  - **`data.csv`**: The raw transactional dataset used for the analysis.
  - **`Portfolio_Clustering_Model_Kmeans_20250122.ipynb`**: The Jupyter Notebook containing the complete Python implementation, from data loading to final recommendations.

-----

## **Dataset Description**

The dataset contains transactional data from an e-commerce platform. The key columns utilized are:

  - **`CustomerID`**: A unique identifier for each customer.
  - **`InvoiceDate`**: The date and time of each transaction.
  - **`Quantity`**: The number of units of a product purchased in a transaction.
  - **`UnitPrice`**: The price of a single unit of a product.
  - **`Country`**: The country where the purchase was made.

These raw features are processed to engineer the RFM metrics, which form the feature space for clustering:

  - **Recency**: Days since the customer's last purchase, calculated relative to a reference date (`2012-01-01`).
  - **Frequency**: The total number of unique invoices for each customer.
  - **Monetary**: The average monetary value of transactions for each customer.

-----

## **Methodology and Project Steps**

### **Step 1: Exploratory Data Analysis (EDA)**

  - **Goals:** Understand data characteristics and identify potential data quality issues.
  - **Key Tasks:**
      - Generated a comprehensive data profile using `ydata-profiling` to get a high-level overview of variable types, missing values, and descriptive statistics.
      - Utilized `sidetable` to analyze the frequency distribution of categorical variables, notably `Country`, which showed a heavy concentration of transactions in the United Kingdom.
      - Visualized feature distributions with histograms and boxplots to identify skewness and potential outliers in `Quantity` and `UnitPrice`.

### **Step 2: Data Preprocessing and Feature Engineering**

  - **Goals:** Clean the data and construct the RFM feature set for modeling.
  - **Key Tasks:**
      - **Handling Missing Data**: Removed records with missing `CustomerID` as they cannot be used for segmentation.
      - **Correcting Data Types**: Converted `InvoiceDate` to datetime objects and `CustomerID` to integer type for accurate calculations.
      - **Cleaning Inconsistent Values**: Filtered out transactions where `Quantity` or `UnitPrice` were zero or negative, as these represent invalid entries or returns.
      - **Outlier Mitigation**: Capped extreme values in the calculated RFM metrics at their 95th percentile. This clipping technique mitigates the disproportionate influence of a small number of outliers on the cluster centroids.
      - **Normalization**: Applied a `PowerTransformer` to the clipped RFM metrics to handle skewness and stabilize variance, followed by a `StandardScaler` (`scale`) to normalize the features to have a mean of 0 and a standard deviation of 1. This ensures that each feature contributes equally to the clustering algorithm.

### **Step 3: RFM-Based Clustering Analysis**

  - **Goals:** Segment customers into distinct groups using the KMeans algorithm.
  - **Key Tasks:**
      - **Optimal Cluster Determination**: To ensure a robust choice for the number of clusters (*k*), multiple validation methods were employed:
          - **Elbow Method**: Utilized `yellowbrick`'s `KElbowVisualizer` to identify the "elbow point" where the rate of decrease in inertia (within-cluster sum of squares) slows, suggesting an optimal *k*.
          - **Cluster Quality Metrics**: Calculated the **Silhouette Score**, **Davies-Bouldin Score**, and **Calinski-Harabasz Score** for a range of *k* values.
          - The analysis consistently pointed to **k=4** as the optimal number of clusters, offering the best balance between intra-cluster cohesion and inter-cluster separation.
      - **Model Training**: Trained the KMeans model using `n_clusters=4` on the preprocessed (scaled and transformed) RFM data.

### **Step 4: Cluster Profiling and Visualization**

  - **Goals:** Analyze and interpret the characteristics of each customer segment.
  - **Key Tasks:**
      - Calculated the mean RFM values for each of the four clusters to create distinct customer profiles.
      - Computed Z-scores for each cluster's mean RFM values to visualize their divergence from the global average, presented in a heatmap.
      - Generated boxplots to show the distribution of Recency, Frequency, and Monetary values within each cluster.
      - Created a 3D scatter plot using `plotly` to visualize the separation of the four clusters in the RFM feature space.

### **Step 5: Strategic Business Recommendations**

  - **Goals:** Translate data-driven cluster profiles into actionable business strategies.
  - **Cluster Profiles & Strategies:**
      - **Cluster 1: Inactive, Low-Value Customers**:
          - *Profile*: High recency (\~260 days), very low frequency (\~1.5 purchases), and low monetary value (\~$18).
          - *Strategy*: Target with reactivation campaigns, offering personalized discounts or "we miss you" promotions to re-engage them.
      - **Cluster 2: Moderately Active, Low-Value Customers**:
          - *Profile*: Moderate recency (\~67 days), low frequency (\~2.7 purchases), and low monetary value (\~$17).
          - *Strategy*: Nurture and grow. Encourage increased spending through product bundling, cross-sells, and entry-level loyalty programs.
      - **Cluster 3: Active, High-Value Customers**:
          - *Profile*: Moderate recency (\~121 days), high frequency (\~3.9 purchases), and the highest monetary value (\~$81).
          - *Strategy*: These are valuable customers. Focus on retention with VIP programs, exclusive offers, and early access to new products to build loyalty.
      - **Cluster 4: Recent and Very Frequent Customers**:
          - *Profile*: Very low recency (\~41 days), the highest frequency (\~10.2 purchases), but a moderate monetary value (\~$20).
          - *Strategy*: These are highly engaged customers. The goal is to increase their average transaction value. Suggest higher-value complementary products and implement volume-based promotions.

-----

## **Technologies Used**

  - **Data Manipulation & Analysis**: `pandas`, `numpy`
  - **Data Profiling**: `ydata-profiling`, `sidetable`
  - **Machine Learning & Preprocessing**: `scikit-learn` (for `KMeans`, `PowerTransformer`, `StandardScaler`)
  - **Visualization**: `matplotlib`, `seaborn`, `plotly` (for interactive 3D plots)
  - **Clustering Evaluation**: `yellowbrick` (for `KElbowVisualizer`)

-----

## **How to Use**

1.  Clone the repository:
    ```bash
    git clone https://github.com/yourusername/portfolio-clustering-kmeans.git
    ```
2.  Navigate to the project directory and place the dataset (`data.csv`) in the root.
3.  Run the analysis using the Jupyter Notebook (`Portfolio_Clustering_Model_Kmeans_20250122.ipynb`) in an environment like Jupyter Lab or Google Colab for an interactive experience.

-----

## **Future Improvements**

  - Experiment with alternative clustering algorithms like **DBSCAN** or **Hierarchical Clustering** to compare segmentation results.
  - Implement **hyperparameter tuning** for the KMeans algorithm to further optimize cluster formation.
  - **Enrich the dataset** by integrating customer demographic or behavioral data for a more holistic segmentation.
  - **Automate business recommendations** by training a decision-tree model on the cluster labels to identify key drivers for each segment.
  - **Deploy the model** as a web application or API to allow for real-time customer segmentation.

-----

## **Contributors**

This project was developed by **Alexandre R.S.F**. Contributions, suggestions, and feedback are highly encouraged. Please feel free to submit a pull request or open an issue. For more details, refer to the project script or contact [alerodriguessf@gmail.com].
