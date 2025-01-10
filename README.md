# Kee-Siong
SCTP Data Analyst Associate Capstone

Data Analytics Dashboard and Exploration Data Analysis of HDB resale Market (2000 Feb to 2024 Jan)
![image](https://github.com/user-attachments/assets/99356a64-d893-49c6-b58c-de09370d4a62)

Data Summary:
Data comprise of HDB resale transaction prices from (2000 Jan to 2024 Jan). It include town names, flat types, floor area sqm, flat model,
lease commence date, resales price and remaining lease.
Dataset is large enough and comprehensive for deep dived into predicting trends and insights into the HDB flat resale market.
Data size has a total of 628591

Assumption:
As portions of remaining Lease (years) are incomplete, this value will not be included in the analysis due to impact on statistical analyses 
and skew the results of hypothesis tests. Instead, we will look at lease commence date data header.

Description of Data:
4 csv files extracted as follows:
resale-flat-prices-based-on-approval-date-2000-feb-2012
resale-flat-prices-based-on-registration-date-from-mar-2012-to-dec-2014
resale-flat-prices-based-on-registration-date-from-jan-2015-to-dec-2016
ResaleflatpricesbasedonregistrationdatefromJan2017onwards


Perform data cleaning, normalization, and transformation to ensure the dataset(s) are ready for analysis:	

1. Normalization: 4 files extracted need to be joined together as 1 for normalization	

2. Normalization: Files headers names are renamed with "_" taken out and replace with space	
For example: flat_type, street_name, storey_range, floor_area_sqm, flat_model, lease_commence_date, remaining_lease, resale_price	

3. Normalization: "floor_area_ Sqm", "remaining_lease", "lease_commence_date" and "resale_price" change to data type whole number format	

4. Normalization: Data format is set to be in YYYY-MM format. i.e Change to Datetime64 on Python later.

5. Cleaning: 2 files have missing column header on Remaining_lease (resale flat prices from Jan 2000 to Feb 2012 to Mar 2012 to Dec 2014)	

6. Cleaning: Remaining_lease data is in XX years XX months format. Not in numerical whole number	
Use Text to limit to split out the text. For XX months, change XX/10 to get decimal. Then XX years + XX/10 = end result for a integer with a decimal	

7. Cleaning: for files without Remaining_lease add a column, replace blank values with a zero as integer	

8. Cleaning: 4 files are found with same headers and values are combined into one file named as "hdb.csv"

9. Cleaning: converting month object data type to datetime64 format.

The intention is to use Python analysis to gain useful insights into the HDB resale market.


1. Articulate the size and shape of the dataset AND
2. Comment on data quality with respect to null values or missing data.

Articulate the size and shape of the dataset :

a. Size: Total: 628591 rows | memory usage: 52.8+ MB
b. Shape: 11 columns: 7 objects, 2 Float64, 2 int64 | 628591 rows 

Comment on data quality with respect to null values or missing data :

a. Output shows no null or empty values after cleaning;
b. Remove need for further data imputation and promote better analysis.

![image](https://github.com/user-attachments/assets/c4e8eccf-c40c-4086-972f-788fd7f2dec8)



# Overall information about the dataset

df.head( )

![image](https://github.com/user-attachments/assets/8cb8544c-1cec-4e5c-bd77-1c58d45d3add)

hdb.info( ) : Before "month"  data type as "object" is suitable for analysis

![image](https://github.com/user-attachments/assets/08fe7e95-a9b9-4966-a889-b0c63bc04306)

print(df.info()) : After Clean "month" from data type: "object" to "datetime 64 format"

![image](https://github.com/user-attachments/assets/9dcf1e8a-b390-4418-92c6-d2dc78fdd589)



3. Describe the data types of all features (After Cleaning Completed).

Data Types of Features:

float64 (2 columns):

floor area sqm: The floor area of the residential flat in square meters, indicating the size of the unit.
remaining Lease: The remaining lease period of the residential flat in years.

int64 (2 columns):

lease commence date: The year in which the lease for the residential flat started.
resale price: The price at which the residential flat was resold.

object (6 columns):

town: The town or area where the residential flat is situated.
flat type: The type of the residential flat, such as 1-room, 2-room, 3-room, etc.
block: The block number or identifier of the residential unit.
street name: Name of the street where the property is located.
storey range: The range of storeys where the residential flat is located in the building.
flat model: The model or type of the residential flat, which indicates the layout and design.

Datetime64 (1 column):

month: The month of the transaction or record.

4. Select a target column for analysis.

The resale price is the targetted column for analysis. It is the most main value used for analysing
and predicting modelling on HDB resale market. 

Resale price has business relevance to help homebuyers, real estate investors, government agencies, researchers 
to research and make informed prediction and decisions in summary.

Resale price when correlating with features in the dataframe contribute to analysis considerations:

Relationship between price versus town, flat type, lease commencement date, month in the dataframe (i.e. refers transaction period)
would offer choices for suitable model selection (e.g., R-squared, Mean Squared Error, Root Mean Squared Error), 
more accurate trend prediction and identify areas of market demand and supply.
Insights can be gained in housing market and informed decisions can be made available by various stakeholders.


5. Provide descriptive statistics and information for the entire dataset.


information for the entire dataset:


<class 'pandas.core.frame.DataFrame'>
RangeIndex: 628591 entries, 0 to 628590
Data columns (total 11 columns):
 #   Column               Non-Null Count   Dtype  
---  ------               --------------   -----  
 0   month                628591 non-null  object 
 1   town                 628591 non-null  object 
 2   flat type            628591 non-null  object 
 3   block                628591 non-null  object 
 4   street name          628591 non-null  object 
 5   storey range         628591 non-null  object 
 6   floor area sqm       628591 non-null  float64
 7   flat model           628591 non-null  object 
 8   lease commence date  628591 non-null  int64  
 9    resale price        628591 non-null  int64  
 10  remaining Lease      628591 non-null  float64
dtypes: float64(2), int64(2), object(7)
memory usage: 52.8+ MB


Descriptive statistics for the entire dataset:


![image](https://github.com/user-attachments/assets/3fbef9b8-39b2-41b4-81f9-6d704549c2da)


![image](https://github.com/user-attachments/assets/8b2a01b0-b462-480e-bc30-501ed79b6d5c)



7. Identify and comment on outliers within the dataset.


1. resale price:

High Prices: The maximum value of 1,500,000 is significantly higher than the 75th percentile (450,000). 
This suggests the presence of very high-priced properties, which could be considered outliers as higher than the typical market value.

Low Prices: While the minimum value (28,000) doesn't seem extremely low, it's worth investigating properties with very low prices to see 
if they are genuine or potentially erroneous data.


2. floor area sqm:

Large Flat: The maximum value of 297 sqm suggests the presence of very large apartments. While not inherently outliers, 
it's worth examining if these extremely large apartments are consistent with typical market sizes for the given location.


Small Flat: The minimum value of 28 sqm might indicate very small apartments, which could be outliers if 
they are significantly smaller than typical units in the dataset.


3. Remaining Lease:


Will not discussed remaining lease as significant missing data are to be missing. 
Lease commence date will be considered in this report for more accuracy.


4. lease commence date:


Very Early Dates: Properties with extremely early lease commencement dates (e.g., significantly before the average), 
especially if they seem inconsistent with typical construction timelines.


![image](https://github.com/user-attachments/assets/5e5b667e-b8d1-4860-88ab-bb0ef1db089e)


7. Create plots for each categorical column, showing categorical feature distributions.


![image](https://github.com/user-attachments/assets/ccb3430f-5683-4f78-8055-a6957031dcc8)


![image](https://github.com/user-attachments/assets/ec7266aa-1ef3-4e56-b30e-7c442ae3d03a)


![image](https://github.com/user-attachments/assets/4ebf5db1-11ab-4253-83e0-b88d623aaa50)


8. Generate appropriate charts for numerical features, both individually and in relation to the target column.


![image](https://github.com/user-attachments/assets/ce8f4264-c92a-42cb-a8e6-5ee56dbbb84d)


9. Calculate and display correlations between numerical features and the target feature.


![image](https://github.com/user-attachments/assets/c72c3eea-861e-4a94-9902-3c11a9722ab3)


![image](https://github.com/user-attachments/assets/87f31343-2be4-41cb-a1aa-c7fc5e03b8df)


10. Identify any other significant relationships or patterns within the data.


Correlation Matrix Summary:

Correlation: floor area sqm       Versus resale price: 0.53
Correlation: lease commence date  Versus resale price: 0.47
Correlation: remaining Lease      Versus resale price: 0.54

Floor area sqm and resale price: A strong positive correlation (0.53) is observed. 
data indicate as the floor area sqm increases, the resale price increase as well.

lease commence date and resale price: A moderate positive correlation (0.47) is observed. 
This indicates that properties with more recent lease commencement dates (newer properties) have moderate higher resale prices.

Remaining Lease and resale price: A moderate positive correlation (0.54) is observed. 
This suggests that properties with longer remaining lease durations tend to have higher resale prices.
But we will disregard this part due to some data values are empty.


11. Summarize findings from these EDA steps, highlighting key insights and implications for the project.


XXXXX TBC
XXXXX TBC
XXXXX TBC
XXXXX TBC


3. Visual Exploration:

Based on the project's objectives, create at least five visualizations using Python or Power BI. 
Explain your choice of visualization type and tool for each.

Pairplot:
a. Able to do correlation checks between targeted variable "resale price" versus variables in the dataset.
b. Able to spot outliers and weak correlationship between variables

Lineplots:
a. Able to see trends over time, easy spot, thus prediction of future prices


![image](https://github.com/user-attachments/assets/1622e997-bcdc-428a-9c39-9562fc483da2)


![image](https://github.com/user-attachments/assets/6adf904a-5aa6-49e4-b323-1b55b41e806b)


![image](https://github.com/user-attachments/assets/0e28db7f-1829-46c1-8461-ef85a2ff0b85)


![image](https://github.com/user-attachments/assets/a4b18a1f-775b-4393-90b2-be9452d313a8)


![image](https://github.com/user-attachments/assets/6efebefc-32cc-48bd-b443-6a31c2554067)


4. Model Development:

Build a model suited to the project's needs and evaluate its performance using at least three metrics appropriate to regression or classification 
(e.g., accuracy, precision, recall, F1). If certain metrics are solely ideal, it is expected that this will be mentioned by the candidate, 
but still 3 metrics total must be presented, even if the remaining 2 are sub-optimal or not ideally suited for the task. 
If the learners can draw an invidious distinction between the ideal metric and the others, they are encouraged to do so.


Three Machine learning data models covered as follows:


a. Linear Regression Model


b. Random Forest Regressor Model


c. Decision Tree Regressor Model


Machine learning models: Regression model are suitable for predicting housing prices, regression models are generally the most suitable type of machine learning model.


a. Regression models are designed to predict continuous values i.e. housing prices. 


b. Housing prices are not discrete categories but rather a continuous range of values.   


Machine learning models: Classification models (i.e. Logistic Regression or Decision Trees Model) can be used to predict categories
(e.g. high price vs. low price). In this report, it is NOT ideal for directly predicting the actual resale price, which is a continuous value.


In summary:


The choice of the specific regression model will depend on factors like the complexity of the data, 
the presence of multicollinearity, and the desired level of interpretability.
We find the Linear Regression Model most suitable for HDB price prediction.


Linear Regression Model:

![image](https://github.com/user-attachments/assets/84f194dd-d2e1-4f59-9f8a-b374ebedfe1f)

Key Observations:


Scatter Plot: The scatter plot shows a strong positive correlation between the Actual and Predicted Resale Prices. 
Model is capturing the trend in the data. The points cluster around a diagonal line direction which makes predictions reasonably close to the actual values.
The model appears to be performing reasonably well in predicting resale prices. The strong positive correlation in the scatter plot and 
the relatively high R-squared value suggest that the model captures the underlying trends in the data.
The MSE and RMSE values provide quantitative measures of the model's prediction error. 
These values can be used to assess the model's accuracy and compare its performance with other models.
The MAE provides another measure of prediction error, which may be more interpretable than MSE or RMSE as it represents the average absolute difference in resale price.


Evaluation Metrics:


Mean Squared Error (MSE): 5194369915.213859. This metric measures the average squared difference between the actual and predicted values. 
A lower MSE generally indicates better performance.

Root Mean Squared Error (RMSE): 72071.9773227699. This is the square root of MSE, providing an error value in the same units as the target variable (resale price).

R-squared (R²): 0.8068809275566823. This metric represents the proportion of variance in the target variable explained by the model. 

An R-squared of 0.806 indicates that the model explains approximately 80.6% of the variance in resale prices, which is a relatively good fit.

Mean Absolute Error (MAE): 54498.6556327262. This measures the average absolute difference between actual and predicted values.



2. Random Forest Regressor Model:



![image](https://github.com/user-attachments/assets/c191b5cb-0413-406b-b1e2-40a8f0d478e3)


Key Observations:


Chart visually represents the relative importance of different features in predicting HDB resale prices using a Random Forest Regressor model. 
Features are ranked based on their contribution to the model's accuracy.

flat type 3 ROOM appears to be the most important feature, indicating number of rooms (specifically 3-room flats) has the highest impact on resale prices.
Other significant features:

flat type 4 ROOM, flat type 5 ROOM, flat type 2 ROOM, and flat type EXECUTIVE, indicate number of rooms in general is a significant factor.
Several town features (e.g., town_BUKIT TIMAH, town_BUKIT MERAH, town_QUEENSTOWN) also have relatively high importance, indicating that location plays a crucial role in determining resale prices.


Feature Groups:


flat type features as a group are highly influential, emphasizing the importance of flat size in predicting resale prices.
town features also form a significant group, highlighting the impact of location on resale values.
flat model features have varying levels of importance, with some models having a greater impact than others.


Model accuracy and featured importance to model building:


Model Accuracy: The model's performance metrics (Mean Squared Error, Root Mean Squared Error, R-squared, Mean Absolute Error) 
can be used to assess its accuracy in predicting resale prices. 
A higher R-squared value generally indicates a better fit of the model to the data.

Feature Importance for Model Building: The chart provides valuable insights for feature selection and model building. 
By focusing on the most important features, model builders can potentially improve accuracy and efficiency.


Metrics Analysis:


Mean Squared Error (MSE): This metric measures the average squared difference between the predicted and actual resale prices. 
A lower MSE indicates better model performance. In this case, the MSE is quite high, suggesting that the model might not be making very accurate predictions.

Root Mean Squared Error (RMSE): The RMSE is the square root of the MSE. It provides a measure of the average error in the same units as the target variable (resale price). A lower RMSE is generally preferred.

R-squared (R2): This metric indicates the proportion of variance in the target variable (resale price) that is explained by the model. 
An R2 value of 0.089 means that only about 8.9% of the price variation is explained by the model, suggesting that it has limited predictive power.

Mean Absolute Error (MAE): This metric measures the average absolute difference between the predicted and actual prices. A lower MAE indicates better model accuracy in terms of predicting the magnitude of the error.


3. Decision Tree Regressor Model:



![image](https://github.com/user-attachments/assets/72e0c646-c95f-4cdc-83d1-972282abddb8)

Model Evaluation:


Key Observations:

The chart visually represents the relative importance of different features in predicting HDB resale prices. 
Features with longer bars have a greater influence on the model's predictions.


Top Features:


Flat Type: 3 ROOM, 4 ROOM, and 5 ROOM flat types have the highest feature importance, suggesting that the number of rooms is a strong predictor of resale price.
Town: Locations like BUKIT MERAH, QUEENSTOWN, and BISHAN also have significant influence, indicating that location plays a crucial role in determining resale values.


Other Influential Features:

Flat Model: Specific flat models like Improved-Maisonette, Premium Maisonette, and 3Gen appear to have a moderate impact on resale prices.
Year and Month: These temporal features likely capture market trends and seasonal variations in prices.


Metrics Analysis:


Mean Squared Error (MSE):

This metric measures the average squared difference between the predicted and actual resale prices. A lower MSE indicates better model performance. 
In this case, the MSE is quite high, suggesting that the model might not be making very accurate predictions.

Root Mean Squared Error (RMSE):

The RMSE is the square root of the MSE. It provides a measure of the average error in the same units as the target variable (resale price). A lower RMSE is generally preferred.


R-squared (R2): 

This metric indicates the proportion of variance in the target variable (resale price) that is explained by the model.
An R2 value of 0.089 means that only about 8.9% of the price variation is explained by the model, suggesting that it has limited predictive power.


Mean Absolute Error (MAE):

This metric measures the average absolute difference between the predicted and actual prices.
A lower MAE indicates better model accuracy in terms of predicting the magnitude of the error.


Overall, the chart and metrics suggest that while the Decision Tree model identifies some important features, 
it does not perform very well in predicting HDB resale prices.
The model's accuracy is limited, and it explains only a small portion of the price variation.


5. Report Presentation:


Prepare a report in either Power BI (with at least three pages and a summary dashboard) or Jupyter Notebook (with at least five graphics). 
Present the data insights in a storytelling format that is tailored to the target audience. 
IT IS NOT A REQUIREMENT TO USE PRESENTATION OR SLIDESHARING SOFTWARE FOR THIS SECTION, but you may if you prefer.

Note: If the minimum criteria above are not met, the project will be deemed incomplete, and you will not pass the assessment.


Overview and Data Summary


Project Overview:
- This analysis focuses on the HDB resale market from February 2000 to January 2024.
- The dataset contains 628,591 rows and 11 columns, including town names, flat types, floor area, flat model, lease commence date, resale price, and remaining lease.


Data Summary:


- Data comprises HDB resale transactions, including town names, flat types, floor area, flat model, lease commence date, resale price, and remaining lease.
- Data is pre-processed through normalization and cleaning to ensure readiness for analysis.
- Missing data in remaining lease is handled by focusing on lease commence date instead.


Data Characteristics and Quality


Dataset Characteristics:


- Size: 628,591 rows, 11 columns.
- Memory usage: 52.8+ MB.
- Data Types: 2 float64, 2 int64, 7 objects.
- No null or empty values after cleaning.


Descriptive Statistics:
- The dataset is comprehensive, with no missing values post-cleaning.
- The shape and memory usage make it suitable for detailed analysis.


Outliers:
- High prices (max: $1,500,000) and very low prices (min: $28,000) may indicate outliers.
- Large flats (max: 297 sqm) and very small flats (min: 28 sqm) should be investigated for consistency.


Insights and Model Development


Key Correlations:
- Floor area sqm and resale price show a strong positive correlation (0.53).
- Lease commence date and resale price have a moderate positive correlation (0.47).


Model Development:

- Three models were evaluated: Linear Regression, Random Forest Regressor, and Decision Tree Regressor.
- Linear Regression Model:
  - R-squared: 0.806, indicating 80.6% variance explained.
  - Metrics: MSE: 5,194,369,915, RMSE: 72,071.98, MAE: 54,498.66.
- Random Forest Regressor Model:
  - Key features: flat type and town.
  - Limited predictive power with an R-squared of 0.089.
- Decision Tree Regressor Model:
  - Identified important features but had limited accuracy with an R-squared of 0.089.


Conclusion:


- Linear Regression Model is most suitable for predicting HDB resale prices.
- Key insights include the significance of flat size and lease commencement date on resale prices.
- Town location play importance with HDB resale prices
- Further analysis can focus on improving model accuracy and exploring additional features.



