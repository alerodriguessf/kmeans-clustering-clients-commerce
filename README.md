# Portfolio Clustering Model (KMeans)

This repository comprehensively implements a customer segmentation analysis using the KMeans clustering algorithm. The project objective is to explore a transactional dataset, process it, and derive meaningful customer clusters based on RFM (Recency, Frequency, Monetary) metrics. This segmentation enables businesses to design targeted marketing campaigns, improve customer retention, and optimize resources.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Setup and Installation](#setup-and-installation)
3. [Dataset Description](#dataset-description)
4. [Project Steps](#project-steps)
   - Step 1: Exploratory Data Analysis (EDA)
   - Step 2: Data Preprocessing
   - Step 3: Clustering Analysis
   - Step 4: Cluster Analysis and Visualization
   - Step 5: Business Recommendations
5. [Technologies Used](#technologies-used)
6. [How to Use](#how-to-use)
7. [Future Improvements](#future-improvements)
8. [Contributors](#contributors)

---

## Project Overview

Customer segmentation plays a pivotal role in data-driven marketing strategies. This project applies the KMeans clustering technique to segment customers based on their purchasing behavior. The dataset is processed and analyzed in the following stages:

- **Exploratory Data Analysis (EDA)**: Insights into the data structure, distribution, and quality.
- **Data Preprocessing**: Removal of inconsistencies, outliers, and normalization of features.
- **Clustering Analysis**: Identification of the optimal number of clusters and application of the KMeans algorithm.
- **Business Recommendations**: Insights and strategies derived from the clustering output.

---

## Setup and Installation

To run the project, ensure the following prerequisites:

### Prerequisites:
- Python 3.8 or higher
- Jupyter Notebook or Google Colab (optional)
- Required libraries (install using the commands below):

```bash
pip install pandas numpy seaborn plotly matplotlib sidetable yellowbrick ydata-profiling
```

### Files:
- **`data.csv`**: The dataset file used for analysis.
- **`portfolio_clustering_model_kmeans_20250122.py`**: Python script containing the full implementation.

---

## Dataset Description

The dataset includes transactional data with the following key columns:

- **CustomerID**: Unique identifier for each customer.
- **InvoiceDate**: Date of purchase.
- **Quantity**: Number of units purchased.
- **UnitPrice**: Price per unit.
- **Country**: Country of purchase.

The data is cleaned and transformed to compute the RFM metrics:
- **Recency**: Days since the last purchase.
- **Frequency**: Number of unique transactions.
- **Monetary**: Average transaction value.

---

## Project Steps

### **Step 1: Exploratory Data Analysis (EDA)**

- **Goals:**
  - Understand data structure and distributions.
  - Identify missing values, outliers, and inconsistencies.

- **Key Tasks:**
  - Generate summary statistics and data profiling reports.
  - Visualize feature distributions using histograms, boxplots, and heatmaps.
  - Analyze unique value counts and correlations between numerical variables.

### **Step 2: Data Preprocessing**

- **Goals:**
  - Prepare data for clustering analysis by cleaning and transforming features.

- **Key Tasks:**
  - Remove rows with missing or inconsistent values.
  - Convert column types to appropriate formats (e.g., date, integer).
  - Handle outliers by capping extreme values and removing negative values.
  - Normalize the RFM metrics using `PowerTransformer` and scaling.

### **Step 3: Clustering Analysis**

- **Goals:**
  - Segment customers into clusters based on RFM metrics.

- **Key Tasks:**
  - Use the Elbow Method and Silhouette Score to determine the optimal number of clusters.
  - Train the KMeans model with the selected number of clusters.
  - Assign cluster labels to each customer and visualize the clusters in 3D.

### **Step 4: Cluster Analysis and Visualization**

- **Goals:**
  - Analyze the characteristics of each cluster to derive actionable insights.

- **Key Tasks:**
  - Compute mean RFM values for each cluster.
  - Normalize cluster profiles using Z-scores.
  - Visualize cluster patterns using heatmaps, boxplots, and bar charts.

### **Step 5: Business Recommendations**

- **Goals:**
  - Provide actionable insights based on cluster profiles.

- **Key Tasks:**
  - Recommend strategies for customer retention, reactivation, and loyalty.
  - Suggest marketing actions tailored to each cluster's characteristics.

---

## Technologies Used

- **Python Libraries**:
  - Data Manipulation: `pandas`, `numpy`
  - Visualization: `seaborn`, `matplotlib`, `plotly`
  - Profiling and Summarization: `sidetable`, `ydata-profiling`
  - Clustering and Preprocessing: `scikit-learn`, `yellowbrick`

---

## How to Use

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/portfolio-clustering-kmeans.git
   ```

2. Place the dataset (`data.csv`) in the root directory.

3. Run the script:
   ```bash
   python portfolio_clustering_model_kmeans_20250122.py
   ```

4. Alternatively, use Jupyter Notebook or Google Colab for an interactive execution.

---

## Future Improvements

- Extend clustering analysis with additional algorithms like DBSCAN and Hierarchical Clustering.
- Implement hyperparameter tuning for improved KMeans performance.
- Integrate customer demographic and behavioral data for enhanced segmentation.
- Automate the generation of business recommendations using decision-tree models.
- Deploy the clustering model as a web application with a user-friendly interface.

---

## Contributors

This project was developed by **Alexandre R.S.F**. Contributions, suggestions, and feedback are welcome. Please feel free to submit a pull request or raise an issue.

---

For more details, refer to the project script or contact [alerodriguessf@gmail.com].

