This is a project I completed for the Udacity Data Analytics Nanodegree. Work is my own.

# Project: Identify Customer Segments for a Mail-Order Company

## Overview

This project applies unsupervised learning techniques to demographic data from Germany to identify population segments that represent the core customer base for a mail-order sales company. By comparing the characteristics of the company's customers to the general population, the goal is to uncover segments that are overrepresented among customers. These insights can then inform targeted marketing campaigns to maximize return on investment.

The analysis utilizes real-world data provided by Bertelsmann Arvato Analytics via Udacity.

## Data

The analysis uses four main datasets:

1.  `Udacity_AZDIAS_Subset.csv`: Demographic data for the general population of Germany (891,211 individuals, 85 features).
2.  `Udacity_CUSTOMERS_Subset.csv`: Demographic data for the mail-order company's customers (191,652 individuals, 85 features).
3.  `Data_Dictionary.md`: Detailed descriptions of the features in the datasets.
4.  `AZDIAS_Feature_Summary.csv`: A summary file outlining feature attributes and missing value codes.

*Note: The CSV files are semicolon (`;`) delimited.*

## Methodology

The project follows these main analytical steps:

1.  **Data Loading & Initial Exploration:** Loading the datasets using pandas.
2.  **Data Preprocessing:**
    * Handling missing values: Converting specified codes to NaN based on the feature summary.
    * Assessing and removing columns with a high percentage (over 80%) of missing data.
    * Assessing missing data per row and dividing data based on a threshold (20% used in the notebook). Comparing distributions between low and high missingness rows. *Analysis proceeds using the low missingness subset.*
3.  **Feature Engineering & Re-Encoding:**
    * Re-encoding categorical features (binary and multi-level). The notebook specifically uses one-hot encoding for `CAMEO` features.
    * Engineering new features from mixed-type variables like `PRAEGENDE_JUGENDJAHRE` (creating `JP_ERA` and `JP_POLITICS`) and `CAMEO_INTL_2015` (creating `CAMEO_WEALTH` and `CAMEO_LIFESTAGE`).
    * Selecting the final set of numeric features for analysis.
4.  **Feature Transformation:**
    * Imputing remaining missing values (the notebook uses mean imputation via `sklearn.preprocessing.Imputer` for sklearn v0.19).
    * Applying feature scaling using `StandardScaler` to standardize the data.
    * Performing dimensionality reduction using Principal Component Analysis (PCA). The notebook retains components explaining ~90% of the variance (determined to be 71 components in the notebook).
5.  **Clustering:**
    * Applying K-Means clustering to the PCA-transformed general population data. The notebook uses the elbow method (plotting average within-cluster distance) to determine the optimal number of clusters (chosen as 5 in the notebook code, though the discussion suggests 6).
    * Applying the same preprocessing, scaling, PCA transformation, and fitted K-Means model to the customer dataset to assign customers to the population clusters.
6.  **Analysis & Comparison:**
    * Comparing the proportion of individuals in each cluster between the general population and the customer datasets.
    * Identifying and interpreting overrepresented (potential target segments) and underrepresented clusters in the customer data.

## Key Findings (Summary)

The analysis successfully identifies distinct demographic segments within the general population. By comparing the customer data against these segments, the project highlights:

* **Popular Segments:** Clusters overrepresented in the customer data, likely indicating the company's core target audience (e.g., the notebook finds clusters associated with higher wealth and potentially older life stages are popular).
* **Unpopular Segments:** Clusters underrepresented among customers, suggesting groups less likely to engage with the company (e.g., potentially younger, less affluent groups).

*(Refer to the Jupyter Notebook `Supervised_and_Unsupervised_Learning.ipynb` for detailed discussion and interpretation of each cluster.)*

## Technologies & Libraries Used

* Python 3
* Jupyter Notebook
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn (specifically Imputer, StandardScaler, PCA, KMeans - *Note: The notebook uses sklearn version 0.19*)

## How to Run

1.  Ensure you have Python 3 and the necessary libraries installed. You might want to use a virtual environment.
    ```bash
    pip install numpy pandas matplotlib seaborn scikit-learn==0.19 jupyter
    ```
    *(Consider creating a `requirements.txt` file for easier setup).*
2.  Download the datasets (`Udacity_AZDIAS_Subset.csv`, `Udacity_CUSTOMERS_Subset.csv`, `AZDIAS_Feature_Summary.csv`, `Data_Dictionary.md`) and place them in the same directory as the notebook.
3.  Launch Jupyter Notebook:
    ```bash
    jupyter notebook
    ```
4.  Open and run the `Supervised_and_Unsupervised_Learning.ipynb` notebook.

## Acknowledgments

* Data provided by Bertelsmann Arvato Analytics.
* Project framework provided as part of the Udacity Data Scientist Nanodegree program.
