# What Drives the Price of a Used Car?

## Project Overview

This project explores a dataset of 426,000 used car records from Kaggle to understand the key factors that influence a vehicle's price. The ultimate goal is to provide clear,
data-driven recommendations to a used car dealership to help them optimize their inventory, increase turnover, and improve pricing strategies.

## Framework Used

The analysis strictly follows the CRISP-DM (Cross-Industry Standard Process for Data Mining) framework, structured into six major phases:

1 Business Understanding

2 Data Understanding

3 Data Preparation

4 Modeling

5 Evaluation

6 Deployment


### 1. Business Understanding

Objective: To translate the business goal of maximizing dealership profit into a data problem by identifying the key mathematical drivers of used car prices.

Deliverable: Actionable, non-technical recommendations for a used car dealership on what consumers value most in the current market.

### 2. Data Understanding & Exploratory Data Analysis (EDA

The initial dataset contained 426,000 rows and 18 columns.

  ****Missing Data Analysis:****  A visual and statistical analysis was performed to identify missing values.

   - Critical: The size column was missing ~72% of its data and was flagged for complete removal to prevent model bias.
      
   - Moderate/Minor: Other columns like cylinders, condition, and VIN had varying levels of missing data requiring strategic imputation rather than deletion.

  ****Exploratory Insights:****
  
  The price distribution is heavily right-skewed, with typical vehicle prices clustering between $8k and $26k.
    
  - Scatter plots revealed a distinct negative correlation between price and mileage.
  - Utility and luxury brands (Ram, Mercedes-Benz, BMW, Lexus) command noticeably higher average prices than mass-market manufacturers like Honda or Hyundai.




### 3. Data Preparation & Feature Engineering
To ensure the machine learning models received clean, mathematical inputs without data leakage, the following pipeline was executed:

  ****Cleaning & Imputation::**** Dropped id and size. Converted the messy VIN column into a usable binary has_VIN feature. Filled missing odometer values with the dataset median, and imputed missing categorical variables (like fuel, condition) with placeholders or mode values.
    
  ****Outlier Removal::**** Applied an Interquartile Range (IQR) filter to mathematically strip out extreme price anomalies. Applied a logarithmic transformation (log_price) to normalize the target variable.

  ****Feature Engineering:**** 
  - Created a continuous variable, car_age, derived from the vehicle's year to better represent wear-and-tear.
  - Applied One-Hot Encoding to convert categorical text (like drive type) into binary format.
  - Used Standard Scaling to normalize numerical features so columns with naturally large numbers (like odometer) wouldn't unfairly dominate the model.




### 4. Modeling
Three distinct regression models were trained to predict the car's log price. Grid Search Cross-Validation (GridSearchCV) was used to tune hyperparameters for the regularized models.
  - Standard Linear Regression
  - Ridge Regression (L2 Regularization)
  - Lasso Regression (L1 Regularization)

    
 ****Results:****
  
  - Performance: All three models successfully captured the market trends, achieving an $R^2$ score of approximately 0.643 (explaining ~64.3% of the variance in used car prices).
  
  - Overfitting Check: The models generalized perfectly to unseen data. The Train $R^2$ (~0.640) and Test $R^2$ (~0.643) were nearly identical.

  - Final Selection: Standard Linear Regression was chosen as the winning model. Because the dataset did not suffer from heavy multicollinearity, the regularized Ridge and Lasso models provided no accuracy boost while taking significantly longer to compute.
(Note: Exploring Polynomial Features to capture non-linear depreciation curves was attempted but limited by memory constraints).


### 5. Evaluation & Business Recommendations
By extracting the mathematical coefficients from the trained Linear Regression model, we can clearly identify the exact features that drive vehicle prices up or down.

****The Biggest Depreciators (What drives prices down)****
  - Age & Mileage: A car's age and its odometer reading are the strongest negative predictors. As these numbers increase, consumers heavily penalize the vehicle's value.

  - Condition & Title: Cars listed as "salvage", "fair", or lacking a clean title take massive valuation hits.
  - 
****The Premium Drivers (What consumers pay extra for)****
  - Vehicle Type: Body style matters immensely. Pickup trucks and SUVs hold their value far better than standard sedans or hatchbacks.

  - Engine & Drivetrain: Consumers demonstrate a willingness to pay a high premium for more power (higher cylinder counts), Diesel/Electric fuel types, and 4-Wheel Drive (4WD) systems.

***Actionable Strategy for Dealerships:***

  - Optimize Inventory Acquisition: Focus purchasing efforts on vehicles under 10 years old with below-average mileage. Prioritize stocking SUVs and Pickup trucks with 4WD and powerful engines, as these retain the highest profit margins.

  - Strategic Pricing: Aggressively price premium vehicles (Diesels, 4WD SUVs) as consumers will pay extra for them. Conversely, do not overprice older, high-mileage sedans, as the market demands steep discounts.

  - Condition is King: Consumers are highly risk-averse. Ensure all inventory has "Clean" titles. Investing in minor refurbishments to upgrade a car's cosmetic or mechanical condition from "Good" to "Excellent" will yield a high return on investment.

  - Regional Adaptation: Tailor your lot's inventory to local geography—stock more AWD/4WD vehicles if your dealership is in a region with harsh weather or rough terrain.
