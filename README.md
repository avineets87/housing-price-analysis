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

### **Property Type Counts (Without Outliers)**
Outliers in property type counts were removed to get a clearer view of the distribution of property types across the dataset. This helps identify the most common types of properties and eliminates any extreme values that may distort the analysis.

**Property Type Counts (Without Outliers):**
![Property Type Counts Without Outliers](./visualizations/property_type_counts_without_outliers.png)
*Above: A bar chart displaying the counts of different property types, excluding outliers.*

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

## Data Cleanup

### **Missing Data**
- Imputation was used to handle missing values in non-essential columns (e.g., missing amenities information).
- Properties with significant missing data were removed.

### **Outliers**
- We identified and handled outliers using z-scores and IQR methods, adjusting or removing extreme outliers where necessary to ensure model accuracy.

### **Feature Engineering**
- Created new features such as price per square foot and neighborhood categories.
- One-hot encoding was applied to categorical features like neighborhood and property type.

---

## Regression Model and Results

### **Approach:**
- **Model:** We built a **Linear Regression** model to predict housing prices based on numeric features such as square footage, number of bedrooms, and neighborhood.
- **Evaluation Metrics:** We used **Mean Absolute Error (MAE)**, **Root Mean Squared Error (RMSE)**, and **R-squared** to evaluate model performance.

### **Results:**
- **R-squared:** 0.85 – indicating that 85% of the variance in housing prices was explained by the model.
- **Key Predictors:** Location (borough), property size (square footage), and the number of bedrooms were the most influential factors.
- **Model Insights:** The model suggests that proximity to Manhattan and certain high-demand neighborhoods (e.g., Brooklyn) significantly increase property prices.

---

## Classification Model and Results

### **Approach:**
- **Model:** We built a **Random Forest Classifier** to categorize properties into pricing brackets (e.g., Low, Medium, High) based on key features.
- **Evaluation Metrics:** We used **Accuracy**, **Precision**, **Recall**, and **F1 Score** for model evaluation.

### **Results:**
- **Accuracy:** 0.78 – meaning 78% of the time, the model correctly predicted the price category.
- **Precision and Recall:** High precision for the "High Price" category, indicating good detection of luxury properties.
- **Model Insights:** The classification model revealed that properties with specific amenities (e.g., parking, gyms) and those in certain high-demand neighborhoods were most likely to fall into the "High Price" category.

---

## Next Steps

1. **Improve Model Performance:**
   - **Additional Data:** This will enhance the model's ability to capture complex relationships and provide more accurate predictions, as a broader dataset can improve its generalizability and robustness.
   - **More Features:** One example of such a feature could be proximity to city center. This can also be accomplished through further data collection.
