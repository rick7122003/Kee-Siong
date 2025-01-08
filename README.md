# Kee-Siong
SCTP Data Analyst Associate Capstone

Data Analytics Dashboard and Exploration Data Analysis of HDB resale Market (2000 Feb to 2024 Jan)
![image](https://github.com/user-attachments/assets/99356a64-d893-49c6-b58c-de09370d4a62)

Data Summary:
Data comprise of HDB resale transaction prices from (2000 Feb to 2024 Jan). It include town names, flat types, floor area sqm, flat model,
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

4. Normalization: Data format is set to be in YYYY-MM format.

5. Cleaning: 2 files have missing column header on Remaining_lease (resale flat prices from Jan 2000 to Feb 2012 to Mar 2012 to Dec 2014)	

6. Cleaning: Remaining_lease data is in XX years XX months format. Not in numerical whole number	
Use Text to limit to split out the text. For XX months, change XX/10 to get decimal. Then XX years + XX/10 = end result for a integer with a decimal	

7. Cleaning: for files without Remaining_lease add a column, replace blank values with a zero as integer	

8. Cleaning: 4 files are found with same headers and values are combined into one file named as "hdb.csv"

The intention is to use it for PowerBI and Python analysis to gain useful insights into the HDB resale market.


1. Articulate the size and shape of the dataset AND
2. Comment on data quality with respect to null values or missing data.

Articulate the size and shape of the dataset :

a. Size: Total: 628591 rows | memory usage: 52.8+ MB
b. Shape: 11 columns: 7 objects, 2 Float64, 2 int64 | 628591 rows 

Comment on data quality with respect to null values or missing data :

a. Output shows no null or empty values after cleaning;
b. Remove need for further data imputation and promote better analysis.


# Overall information about the dataset

df.head( )

![image](https://github.com/user-attachments/assets/8cb8544c-1cec-4e5c-bd77-1c58d45d3add)

hdb.info( )

![image](https://github.com/user-attachments/assets/08fe7e95-a9b9-4966-a889-b0c63bc04306)


3. Describe the data types of all features.
Data Types of Features:

float64 (2 columns):

floor area sqm: The floor area of the residential flat in square meters, indicating the size of the unit.
remaining Lease: The remaining lease period of the residential flat in years.

int64 (2 columns):

lease commence date: The year in which the lease for the residential flat started.
resale price: The price at which the residential flat was resold.

object (7 columns):

month: The month of the transaction or record.
town: The town or area where the residential flat is situated.
flat type: The type of the residential flat, such as 1-room, 2-room, 3-room, etc.
block: The block number or identifier of the residential unit.
street name: Name of the street where the property is located.
storey range: The range of storeys where the residential flat is located in the building.
flat model: The model or type of the residential flat, which indicates the layout and design.


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

_____   floor area sqm  lease commence date   resale price   remaining Lease
count   628591.000000        628591.000000    6.285910e+05    628591.000000
mean        96.767132          1990.411314    3.620510e+05        24.540975
std         25.051891            11.335256    1.643300e+05        35.885856
min         28.000000          1966.000000    2.800000e+04         0.000000
25%         74.000000          1983.000000    2.400000e+05         0.000000
50%         96.000000          1988.000000    3.380000e+05         0.000000
75%        113.000000          1998.000000    4.500000e+05        63.400000
max        297.000000          2022.000000    1.500000e+06        97.900000

Descriptive Statistics for month:
month
2010-07    3679
2010-06    3517
2001-10    3490
2009-10    3432
2001-07    3398
           ... 
2014-02     959
2013-02     886
2020-04     424
2024-01     411
2020-05     363
Name: count, Length: 289, dtype: int64

Descriptive Statistics for town:
town
WOODLANDS          55028
TAMPINES           48480
JURONG WEST        46656
YISHUN             41503
BEDOK              38939
HOUGANG            34173
SENGKANG           31532
ANG MO KIO         31192
CHOA CHU KANG      29136
BUKIT BATOK        27333
BUKIT MERAH        23322
PASIR RIS          22025
BUKIT PANJANG      21743
TOA PAYOH          20287
PUNGGOL            19835
QUEENSTOWN         18721
KALLANG/WHAMPOA    18126
GEYLANG            17467
CLEMENTI           16473
JURONG EAST        15499
SERANGOON          14115
SEMBAWANG          13421
BISHAN             12794
MARINE PARADE       4657
CENTRAL AREA        4583
BUKIT TIMAH         1551
Name: count, dtype: int64

Descriptive Statistics for flat type:
flat type
4 ROOM              248960
3 ROOM              180081
5 ROOM              144616
EXECUTIVE            46835
2 ROOM                7366
1 ROOM                 473
MULTI-GENERATION       260
Name: count, dtype: int64

Descriptive Statistics for block:
block
2       2641
1       2455
4       2030
101     1992
8       1990
        ... 
995C       2
605B       2
226E       2
226F       1
460A       1
Name: count, Length: 2700, dtype: int64

Descriptive Statistics for street name:
street name
YISHUN RING RD            10362
ANG MO KIO AVE 10          8094
BEDOK RESERVOIR RD         7939
ANG MO KIO AVE 3           7097
HOUGANG AVE 8              5745
                          ...  
SELETAR WEST FARMWAY 6        8
GEYLANG EAST AVE 2            7
YISHUN ST 43                  6
MARINE PARADE CTRL            3
ALJUNIED AVE 2                1
Name: count, Length: 573, dtype: int64

Descriptive Statistics for storey range:
storey range
04 TO 06    154522
07 TO 09    138379
01 TO 03    123425
10 TO 12    118344
13 TO 15     47219
16 TO 18     19283
19 TO 21      8583
22 TO 24      5589
25 TO 27      2812
01 TO 05      2700
06 TO 10      2474
28 TO 30      1593
11 TO 15      1259
31 TO 33       592
34 TO 36       551
37 TO 39       495
16 TO 20       265
40 TO 42       237
21 TO 25        92
43 TO 45        64
46 TO 48        48
26 TO 30        39
49 TO 51        17
36 TO 40         7
31 TO 35         2
Name: count, dtype: int64

Descriptive Statistics for flat model:
flat model
Model A                   190205
Improved                  165547
New Generation            108763
Premium Apartment          45634
Simplified                 33893
Apartment                  25227
Standard                   24912
Maisonette                 17165
Model A2                   10014
DBSS                        3191
Adjoined flat               1234
Model A-Maisonette          1078
Terrace                      441
Type S1                      430
Multi Generation             260
Type S2                      212
Premium Apartment Loft       104
2-room                        88
Premium Maisonette            86
Improved-Maisonette           81
3Gen                          26
Name: count, dtype: int64


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



8. Generate appropriate charts for numerical features, both individually and in relation to the target column.



9. Calculate and display correlations between numerical features and the target feature.


10. Identify any other significant relationships or patterns within the data.



11. Summarize findings from these EDA steps, highlighting key insights and implications for the project.


3. Visual Exploration:

Based on the project's objectives, create at least five visualizations using Python or Power BI. 
Explain your choice of visualization type and tool for each.

4. Model Development:

Build a model suited to the project's needs and evaluate its performance using at least three metrics appropriate to regression or classification 
(e.g., accuracy, precision, recall, F1). If certain metrics are solely ideal, it is expected that this will be mentioned by the candidate, 
but still 3 metrics total must be presented, even if the remaining 2 are sub-optimal or not ideally suited for the task. 
If the learners can draw an invidious distinction between the ideal metric and the others, they are encouraged to do so.

5. Report Presentation:

Prepare a report in either Power BI (with at least three pages and a summary dashboard) or Jupyter Notebook (with at least five graphics). 
Present the data insights in a storytelling format that is tailored to the target audience. 
IT IS NOT A REQUIREMENT TO USE PRESENTATION OR SLIDESHARING SOFTWARE FOR THIS SECTION, but you may if you prefer.

Note: If the minimum criteria above are not met, the project will be deemed incomplete, and you will not pass the assessment.





