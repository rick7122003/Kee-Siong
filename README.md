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

1. Articulate the size and shape of the dataset AND 2. Comment on data quality with respect to null values or missing data.

Articulate the size and shape of the dataset :

a. Size: Total: 628591 rows | memory usage: 52.8+ MB
b. Shape: 11 columns: 7 objects, 2 Float64, 2 int64 | 628591 rows 

Comment on data quality with respect to null values or missing data :

a. Output shows no null or empty values after cleaning;
b. Remove need for further data imputation and promote better analysis.


# Overall information about the dataset
hdb.info()

![image](https://github.com/user-attachments/assets/08fe7e95-a9b9-4966-a889-b0c63bc04306)



# Statistical description of the data
hdb.describe()

![image](https://github.com/user-attachments/assets/ca615d9f-6650-4db3-bec0-b367603a3ca9)


3. Describe the data types of all features.
Data Types of Features:

float64 (2 columns):

floor area sqm: Likely represents the area of the apartment in square meters.
remaining Lease: Likely represents the remaining lease duration in years or some other unit.
int64 (2 columns):

lease commence date: Likely represents the year in which the lease for the property commenced.
resale price: Represents the selling price of the property.
object (7 columns):

month: Likely represents the month of the transaction (e.g., '2023-01').
town: Represents the location of the property (e.g., "Singapore", "London").
flat type: Categorizes the type of apartment (e.g., "1-room", "3-room").
block: Likely identifies the specific building within a housing complex.
street name: Name of the street where the property is located.
storey range: Range of floors for the apartment (e.g., '1-5', '10-15').
flat model: Specific model or design of the apartment.
