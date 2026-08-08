# Exploratory Data Analysis (EDA) of Customer Churn

## Project Overview
This project aims to perform an Exploratory Data Analysis (EDA) on customer and pricing data to understand factors contributing to customer churn in an energy utility company. The analysis covers data loading, cleaning, descriptive statistics, and visualization of key features and their relationships with churn.

## Dataset Description
Two main datasets are used:
1.  **`client_data.csv`**: Contains historical customer information and a churn indicator.
2.  **`price_data.csv`**: Contains historical pricing information for different electricity and gas components.

## EDA Steps Performed

### 1. Data Loading and Initial Inspection
-   Loaded `client_data.csv` into `client_df` and `price_data.csv` into `price_df`.
-   Displayed the first 5 rows of each DataFrame to get an initial glance at the data structure.

### 2. Data Type and Missing Value Analysis
-   Used `.info()` to inspect data types and identify non-null counts for both DataFrames.
-   **Observations:**
    -   Several date columns (`date_activ`, `date_end`, `date_modif_prod`, `date_renewal` in `client_df`; `price_date` in `price_df`) were initially `object` type.
    -   The `channel_sales` column in `client_df` contained 'MISSING' string values, which needed conversion for proper handling.

### 3. Data Cleaning (Type Conversion & Missing Value Handling)
-   Converted all identified date columns to `datetime` objects.
-   Replaced 'MISSING' strings in `client_df['channel_sales']` with `pd.NA` to standardize missing value representation.
-   Confirmed no missing values in `price_df`.

### 4. Descriptive Statistics
-   Generated descriptive statistics for numerical columns (`.describe()`) and categorical columns (`.describe(include='object')`) for both DataFrames.
-   **Key Insights from `client_df`:**
    -   Numerical features like consumption (`cons_12m`, `cons_gas_12m`, etc.) and `net_margin` showed highly skewed distributions and a wide range of values, indicating potential outliers.
    -   The churn rate was approximately **9.72%**, highlighting an imbalanced target variable.
    -   `id`s were unique.
    -   Categorical features included `channel_sales`, `has_gas`, and `origin_up`.
-   **Key Insights from `price_df`:**
    -   Pricing components showed reasonable ranges.
    -   A discrepancy was noted: `price_df` had more unique `id`s (16096) than `client_df` (14606), suggesting potential data incompleteness for merging.

### 5. Distribution Visualization (Numerical Columns)
-   Generated histograms and box plots for numerical columns in both `client_df` and `price_df`.
-   **Observations:**
    -   `client_df` numerical features confirmed extreme right-skewness and the presence of numerous outliers, consistent with the descriptive statistics.
    -   `price_df` numerical features exhibited multi-modal distributions, suggesting distinct pricing tiers, and some outliers.

### 6. Churn Variable Analysis
-   Visualized the churn distribution using a stacked bar plot and calculated the exact churn rate.
-   Confirmed the churn rate at approximately **9.72%**, indicating an imbalanced dataset, which is crucial for subsequent modeling steps.

### 7. Correlation Analysis (Numerical Features vs. Churn)
-   Calculated the correlation matrix between numerical features in `client_df` and the `churn` variable.
-   Visualized the correlations using a heatmap.
-   **Observation:** Most numerical features showed a very weak linear correlation with `churn` (coefficients close to zero), suggesting they are not strong individual linear predictors of churn.

### 8. Categorical Feature Analysis (Distribution and Churn Relationship)
-   Generated count plots to visualize the distribution of `channel_sales`, `has_gas`, and `origin_up` in `client_df`.
-   Used stacked bar plots to analyze the churning status within each category of these features.
-   **Observations:**
    -   `channel_sales`: Churn rates vary across different sales channels. Some channels show higher churn percentages (e.g., 'lxidpiddsbxsbosboudacockeimpuepw') than others.
    -   `has_gas`: Customers with gas contracts (`t`) tend to have a slightly higher churn rate than those without (`f`).
    -   `origin_up`: Churn rates also vary by the origin of the customer, with 'lxidpiddsbxsbosboudacockeimpuepw' showing a higher churn percentage.

## Next Steps
-   Further investigate the `id` discrepancy between `client_df` and `price_df` to ensure proper data merging.
-   Explore potential feature engineering opportunities based on the insights gained (e.g., transformations for skewed data, creating new features from dates or interactions).
-   Prepare data for machine learning model training.
