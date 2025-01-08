# Kee-Siong
SCTP Data Analyst Associate Capstone

Data Analytics Dashboard and Exploration Data Analysis of HDB resale Market (2000 feb to 2024 Jan):


Description of Data:
4 csv files extracted as follows:
resale-flat-prices-based-on-approval-date-2000-feb-2012
resale-flat-prices-based-on-registration-date-from-mar-2012-to-dec-2014
resale-flat-prices-based-on-registration-date-from-jan-2015-to-dec-2016
ResaleflatpricesbasedonregistrationdatefromJan2017onwards


Perform data cleaning, normalization, and transformation to ensure the dataset(s) are ready for analysis:	

Normalization: 4 files extracted need to be joined together as 1 for normalization	
Normalization: Files headers names are renamed with "_" taken out and replace with space	
	For example: flat_type, street_name, storey_range, floor_area_sqm, flat_model, lease_commence_date, remaining_lease, resale_price	
Normalization: "floor_area_ Sqm", "remaining_lease", "lease_commence_date" and "resale_price" change to data type whole number format	
Cleaning: 2 files have missing column header on Remaining_lease (resale flat prices from Jan 2000 to Feb 2012 to Mar 2012 to Dec 2014)	
Cleaning: Remaining_lease data is in XX years XX months format. Not in numerical whole number	
	Use Text to limit to split out the text. For XX months, change XX/10 to get decimal. Then XX years + XX/10 = end result for a integer with a decimal	
Cleaning: for files without Remaining_lease add a column, replace blank values with a zero as integer	
Cleaning: 4 files are found with same headers and values are combined into one file named as "hdb.csv"

The intention is to use it for PowerBI and Python analysis
