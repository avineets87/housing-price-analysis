# Housing Pricing Analysis for New York City

## Project Objective and Goals
**Objective:**  
The objective of this project is to conduct a comprehensive analysis of housing prices in New York City, identifying key factors that drive property valuations. Our goal is to develop predictive models capable of forecasting housing prices and generating actionable insights into the dynamics of the New York City housing market.

**Goals:**  
1. **Identify Key Factors:** Determine the primary factors affecting housing prices (beds, bath, property sqft, borough, property category,	type).
2. **Price Prediction:** Build regression models to predict housing prices based on features.
3. **Classify Housing Types:** Develop a classification model to categorize properties based on pricing categories.

---

## Meet the Team Members

- **Avineet Sharma**   
- **Marwa Bensalem** 
- **Natasha Anghelescu** 
- **Ryan Goldstein** 

---

## Data Gathering Approach

### **Kaggle Housing Dataset**
- **Source:** The primary dataset was obtained from Kaggle, which contains information on NYC housing prices, including features like property size, number of rooms, neighborhood, and price. https://www.kaggle.com/code/alancano/new-york-housing-market 
- **Key Features:** Property size, number of bedrooms, number of bathrooms, locality, sub locality and geo location parameters

### **Reverse Geolocation API**
- **Purpose:** We used a reverse geolocation API to enrich the dataset with borough and neighborhood information based on geographic coordinates (latitude/longitude). 
- Example: https://api.geoapify.com/v1/geocode/reverse?lat=40.618103&lon=-74.0369047&format=json&apiKey=b8568cb9afc64fad861a69edbddb2658 
- **Rationale:** This allowed us to group properties by specific geographic areas and perform better spatial analysis on price trends.

---

## Data Exploration

### **Descriptive Statistics**
To get a better understanding of the dataset, we started by calculating basic descriptive statistics for key variables such as price, square footage, number of bedrooms, and the type of property. The summary statistics provide insight into the distribution of data, including measures of central tendency (mean, median) and variability (standard deviation, min, max).

**Descriptive Statistics:**
![Data Summary](./visualizations/data.describe.png)
*Above: A summary of the key statistics for the housing data, including price, square footage, and the number of bedrooms.*

---

### **Geographical Distribution of Properties**
We visualized the geographical distribution of properties across New York City. The plot shows how properties are distributed across different boroughs and neighborhoods. It also helps identify areas with higher concentrations of real estate activity.

**Geo Distribution of Properties:**
![Geographical Distribution](./visualizations/geo_distribution.png)
*Above: A visualization showing the geographical distribution of properties across NYC.*

---

### **Price vs. Property Size**
We examined the relationship between the price of properties and their size (measured in square footage). The plot helps us understand if larger properties tend to be more expensive, or if other factors play a significant role in pricing.

**Price vs. Property Size:**
![Price vs Property Size](./visualizations/price_vs_propertysize.png)
*Above: A scatter plot showing the relationship between property size and price.*

---

### **Price vs. Property Sizes (Without Outliers)**
Outliers were removed to get a clearer view across the dataset. 

**Price vs. Property Sizes (Without Outliers):**
![Price vs. Property Sizes (Without Outliers)](./visualizations/price_vs_propertysize_without_outliers.png)
*Above: A scatter plot showing the relationship between property size and price, excluding outliers.*

---

### **Property Type Counts**
This visualization shows the distribution of property types in the dataset, including the outliers. It helps in identifying trends, such as the most common types of properties (e.g., apartments, houses).

**Property Type Counts (With Outliers):**
![Property Type Counts](./visualizations/property_type_counts.png)
*Above: A bar chart displaying the counts of different property types, including outliers.*

---

### **Property Price vs. Neighborhoods**
To analyze how property prices vary across different neighborhoods in New York City, we plotted the price of properties against the neighborhoods they belong to. This visualization reveals how neighborhood location is a significant factor in property pricing.

**Property Price vs. Neighborhoods:**
![Property Price vs Neighborhood](./visualizations/property_vs_neighbourhoods.png)
*Above: A plot showing how property prices vary across different neighborhoods in NYC.*

---

### **SPLOM (Scatter Plot Matrix) of Real Estate Data**
We performed a scatter plot matrix (SPLOM) to visually assess the relationships between multiple variables in the dataset (e.g., price, square footage, number of bedrooms, etc.). This helps us identify potential correlations and patterns among different features.

**SPLOM of Real Estate Data:**
![SPLOM of Real Estate Data](./visualizations/splom_real_estate_data.png)
*Above: A scatter plot matrix showing pairwise relationships between key features in the real estate dataset.*

---

### Summary of Findings
- **Geographical Insights:** The geographic distribution of properties highlights that most real estate activity is concentrated in Manhattan and parts of Brooklyn, with fewer listings in less urbanized areas of the city.
- **Price and Size:** Larger properties tend to have higher prices, but the relationship is not perfectly linear, indicating other factors contribute to pricing.
- **Property Types:** The distribution of property types shows that apartments are the most common type of property in NYC, followed by houses and condos.
- **Neighborhood Impact:** Property prices are heavily influenced by the neighborhood, with prime areas such as Manhattan and parts of Brooklyn commanding higher prices.
- **Feature Relationships:** The SPLOM visualization revealed that property size and price have a moderate positive correlation, while other features, like the number of bedrooms, have varying levels of influence on price.


---

## Data Cleaning Process

The objective of this section is to clean and analyze a real estate dataset. This involves removing inconsistencies, handling missing data, standardizing columns, and eliminating outliers, thereby preparing the dataset for further analysis and predictive modeling.

### 1. **Merging and Removing Duplicates**
- Merged the datasets based on `LATITUDE` and `LONGITUDE` columns.
- Removed duplicates based on `LATITUDE` and `LONGITUDE`.

### 1. Merging and Removing Duplicates
- **Action**: Merged datasets based on `LATITUDE` and `LONGITUDE` columns.
- **Outcome**: Removed duplicate entries based on the same `LATITUDE` and `LONGITUDE`.

### 2. Standardization
- **Action**: Standardized text columns by:
  - Stripping leading and trailing spaces.
  - Converting text to lowercase for columns such as `SUBLOCALITY` and `STATE`.
- **Outcome**: Renamed redundant columns for improved clarity.

### 3. Handling Missing Data
- **Action**: 
  - Dropped rows with missing values in critical columns (`TYPE`, `PROPERTY_CATEGORY`).
  - Filled missing values in other columns (`BEDS`, `BATH`) using appropriate methods (e.g., median for numerical data).
- **Outcome**: Ensured that essential data is complete for analysis.

### 4. Outlier Removal
- **Action**: Removed outliers using the Interquartile Range (IQR) method for the following columns:
  - `PRICE`
  - `BEDS`
  - `BATH`
  - `PROPERTYSQFT`
  - `PRICE_PER_SQFT`
- **Outcome**: Enhanced the quality of the dataset by eliminating extreme values.

### 5. Category Mapping
- **Action**: Mapped `PROPERTY_CATEGORY` to simplified categories (e.g., Residential, Commercial, Other).
- **Outcome**: Streamlined categories for easier analysis.

### 6. Final Dataset
- **Action**: Exported the cleaned dataset to a CSV file for further analysis.
- **Outcome**: Prepared the dataset for subsequent modeling and insights.

---

## Data Interpretation

| **Metric**        | **Before Cleaning**                                | **After Cleaning**                              |
|-------------------|---------------------------------------------------|-------------------------------------------------|
| **PRICE**         | **Min**: $3,225<br>**Max**: Over $2 billion<br>**Mean**: $730,000<br>**Comment**: Extreme outliers present, with some properties priced unrealistically. | **Min**: $50,000<br>**Max**: $2.8 million<br>**Mean**: $805,000<br>**Comment**: Extreme outliers removed, resulting in more realistic price ranges. |
| **BEDS**          | **Min**: 1<br>**Max**: 50<br>**Mean**: 3.4<br>**Comment**: Some properties had a high number of bedrooms, likely due to data entry errors. | **Min**: 1<br>**Max**: 7<br>**Mean**: 3.2<br>**Comment**: Number of bedrooms now within a typical range. |
| **BATH**          | **Min**: 0<br>**Max**: 50<br>**Mean**: 2.2<br>**Comment**: Some properties had 0 or more than 10 bathrooms, which are uncommon. | **Min**: 1<br>**Max**: 4<br>**Mean**: 2.1<br>**Comment**: Number of bathrooms now more realistic. |
| **PROPERTYSQFT**  | **Min**: 230 sqft<br>**Max**: 65,535 sqft<br>**Mean**: 1,400 sqft<br>**Comment**: Square footage had large discrepancies, indicating outliers. | **Min**: 230 sqft<br>**Max**: 3,733 sqft<br>**Mean**: 1,765 sqft<br>**Comment**: Square footage now more consistent and realistic. |
| **PRICE_PER_SQFT**| **Min**: $225<br>**Max**: $2,000,000<br>**Mean**: $500<br>**Comment**: Price per square foot showed unrealistic extremes. | **Min**: $1.48<br>**Max**: $1,201<br>**Mean**: $488<br>**Comment**: Price per square foot now within a reasonable range. |

---

## Visual Comparison

### Before Cleaning and After Cleaning:
![Data Cleaning Summary](/visualizations/CLean.png)

---

The data cleaning process successfully removed extreme outliers, standardized column values, and addressed missing data. The cleaned dataset is now ready for deeper analysis or predictive modeling.

---

## Regression Model and Results

### **Approach:**
- **Model:** We built a **Linear Regression** models to predict housing prices based on numeric features such as square footage, number of bedrooms,bathrooms and neighborhood.
  
  **GridSearchCV** was used for optimizing machine learning models, and to allow to systematically explore the hyperparameter space and find the best settings for our data.

List of used hyperparameters:

    Linear Regression: 
    fit_intercept: [True, False],
 
    Decision Tree: 
    max_depth: [None, 5, 10, 20],
    min_samples_split: [2, 5, 10],
    min_samples_leaf: [1, 2, 4]
  
    Random Forest: 
    n_estimators: [50, 100, 200],
    max_depth: [None, 10, 20],
    min_samples_split: [2, 5],
    min_samples_leaf: [1, 2],
    bootstrap: [True, False]
  
    Gradient Boosting: 
    n_estimators: [50, 100, 200],
    learning_rate: [0.01, 0.1, 0.2],
    max_depth: [3, 5, 7]
    
    Support Vector Regressor: 
    C: [0.1, 1, 10],
    epsilon: [0.01, 0.1, 0.2],
    kernel: [linear, rbf]

    - **Best Parameters and Evaluation Metrics:**

  We used **Mean Squared Error (MSE)**, and **R-squared** to evaluate model performance.

- Linear Regression         - MSE: 103975174803.5488, R2: 0.510741
- Decision Tree Best Parameters: 10, min_samples_leaf: 4, min_samples_split: 10
  
  Decision Tree: MSE: 97702388957.6151, R2: 0.540257
  
- Random Forest Best Parameters: bootstrap: True, max_depth: 10, min_samples_leaf: 2, min_samples_split: 5, n_estimators: 50

  Random Forest MSE: 87429100923.3593, R2: 0.588599

- Gradient Boosting Best Parameters: learning_rate: 0.1, max_depth: 3, n_estimators: 200

  Gradient Boosting         - MSE: 94112950013.0487, R2: 0.557148

- Vector Regressor Best Parameters: C: 10, epsilon: 0.01, kernel: linear
  
  Support Vector Regressor  - MSE: 212468456339.3231,R2: 0.000221

  ### **Plot MSE results**
  
![image](https://github.com/user-attachments/assets/be8a284e-8323-4812-8056-6805072638c3)

### **Plot R2 results**

![image](https://github.com/user-attachments/assets/fee9d1a2-e8c6-4450-a4d1-97290f75b802)

### **Results:**
- **R-squared:** Indicating that depending on the model, 50-59%  of the variance in housing prices was explained by the model.
- **Model Insights:** The model suggests that proximity to Manhattan and certain high-demand neighborhoods (e.g., Brooklyn) significantly increase property prices.
- Based on the evaluation, the best model is: **Random Forest with highest R2 score, 0.588599**
- **Key Predictors:** Location (borough), property size (square footage), and the number of bathrooms were the most influential factors.
  Our dataset lacks information on the overall number of rooms in the property, encompassing not only bedrooms but also other spaces such as living rooms, dining rooms, and additional rooms. This missing data could impact the model’s accuracy in predicting house prices, as the total number of rooms is a significant feature in real estate valuation.

- **Feature importance:**
  Feature importance to determine the relevance of each feature in predicting the target variable

  Results before feature aggregation:
  
  ![image](https://github.com/user-attachments/assets/07560218-b4ae-4b5d-923f-2084aff8b5da)

Results after feature aggregation:

![image](https://github.com/user-attachments/assets/748a8e82-3abf-4c0e-9fac-3df3ced3684b)

Results after feature aggregation plotted:

![image](https://github.com/user-attachments/assets/e8168092-fd55-4a3d-bc5a-c4f1b8f16070)

---
## **Classification Model and Results**

### **Data Features and Preprocessing**

#### **Feature Engineering**
1. **Derived Features:**
   - `TOTAL_ROOMS`: Sum of bedrooms and bathrooms.

2. **Binning Square Footage:**
   - Created a `SQFT_CATEGORY` feature (target variable):
     - **Small:** Less than 1,000 sqft.
     - **Medium:** Between 1,000 and 2,000 sqft.
     - **Large:** Greater than 2,000 sqft.

   - The `SQFT_CATEGORY` column was encoded using **LabelEncoder** to transform the categorical values ("Small," "Medium," "Large") into numeric representations (0, 1, 2).
      - Reason for Label Encoding: Since SQFT_CATEGORY is the target variable, label encoding ensures that the classification model can process it effectively, as most machine learning algorithms require numerical inputs.

3. **ZIP Code Handling:**
   - Converted `POSTCODE` to `ZIPCODE` as a string for classification.

---

#### **One-Hot Encoding**
Categorical features were encoded using **OneHotEncoder** to transform them into numerical representations.
#### **Data Splitting**
The dataset was split into **training** (80%) and **test** (20%) sets to evaluate the model effectively.

### **Model Training**

#### **Classification Algorithm**
The **Random Forest Classifier** was selected for its robustness and capability to handle mixed data types.

#### **Hyperparameter Tuning:**
- Used **RandomizedSearchCV** to optimize hyperparameters, including:
  - `n_estimators`
  - `max_depth`
  - `min_samples_split`
  - `min_samples_leaf`
  - `class_weight`

---

### **Evaluation Metrics**

#### **Training Performance:**
- **Accuracy:** 0.8872
- **Confusion Matrix:**
  ```
   [[1068   53   26]
    [  71  564   17]
    [  54   24  295]]
  ```
- **Classification Report:**
  ```
                 precision    recall  f1-score   support

             0       0.90      0.93      0.91      1147
             1       0.88      0.87      0.87       652
             2       0.87      0.79      0.83       373

      accuracy                           0.89      2172
     macro avg       0.88      0.86      0.87      2172
  weighted avg       0.89      0.89      0.89      2172
  ```

---

#### **Test Performance (Before SMOTE):**
- **Accuracy:** 0.6360
- **Confusion Matrix:**
  ```
   [[203  43  20]
    [ 68  84   8]
    [ 46  13  59]]
  ```
- **Classification Report:**
  ```
                 precision    recall  f1-score   support

             0       0.64      0.76      0.70       266
             1       0.60      0.53      0.56       160
             2       0.68      0.50      0.58       118

      accuracy                           0.64       544
     macro avg       0.64      0.60      0.61       544
  weighted avg       0.64      0.64      0.63       544
  ```

---

#### **Test Performance (After SMOTE):**
- **Accuracy:** 0.6415
- **Confusion Matrix:**
  ```
   [[193  47  26]
    [ 58  91  11]
    [ 42  11  65]]
  ```
- **Classification Report:**
  ```
                 precision    recall  f1-score   support

             0       0.66      0.73      0.69       266
             1       0.61      0.57      0.59       160
             2       0.64      0.55      0.59       118

      accuracy                           0.64       544
     macro avg       0.64      0.62      0.62       544
  weighted avg       0.64      0.64      0.64       544
  ```

---

#### **Test Performance (After Tuning):**
- **Accuracy:** 0.6654
- **Confusion Matrix:**
  ```
   [[212  38  16]
    [ 65  88   7]
    [ 45  11  62]]
  ```
- **Classification Report:**
  ```
                 precision    recall  f1-score   support

             0       0.66      0.80      0.72       266
             1       0.64      0.55      0.59       160
             2       0.73      0.53      0.61       118

      accuracy                           0.67       544
     macro avg       0.68      0.62      0.64       544
  weighted avg       0.67      0.67      0.66       544
  ```


---

### **Summary**
1. **SMOTE** effectively balanced the dataset, reducing bias toward majority classes and improving the model's ability to classify all categories accurately.
2. **Hyperparameter tuning** fine-tuned the model's performance, resulting in higher accuracy and better generalization.
3. **XGBoost** delivered the best results, with accuracy, precision, recall, and F1-scores surpassing Random Forest.

 
![Confusion Matrix](/visualizations/Classification_Heatmap_matrix.png)

Both **Random Forest** and **XGBoost** demonstrated strong performance, with **XGBoost** achieving the highest accuracy of 66.54%. XGBoost’s superior handling of imbalanced classes and ability to capture complex patterns make it the preferred choice for this classification task. By utilizing SQFT_CATEGORY as the target, the model provides valuable insights into property size zones and their market significance as a whole.

![Performance Summary](/visualizations/Classifcation_Summary_results.png)


---

## Next Steps

1. **Improve Model Performance:**
   - **Additional Data:** This will enhance the model's ability to capture complex relationships and provide more accurate predictions, as a broader dataset can improve its generalizability and robustness.
   - **More Features:** One example of such a feature could be proximity to city center. This can also be accomplished through further data collection.
