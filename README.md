# Karamoja-Datasets

Untitled5.ipynb_Notebook unstarred
star
File
Edit
View
Insert
Runtime
Tools
Help
comment
Comment
people
Share
settings

format_list_bulleted
search
vpn_key
folder
code
Files
tab
close
upload_file
refresh
visibility_off
folder_open
..
arrow_drop_down
folder
sample_data
draft
Uganda_Karamoja_District_Crop_Yield_Population.csv
draft
Uganda_Karamoja_Subcounty_Crop_Yield_Population.csv
draft
cleaned_dataset.csv
upload_file
Drop files to upload them to session storage.
Code
Text
Gemini
expand_less
Business problem
Karamoja is the most food-insecure region of Uganda. One of the main reasons is the low productivity level of the crops due to intense droughts as well as pest and disease outbreaks.

Project overview
The project aims to analyze agricultural datasets related to the Karamoja region of Uganda. The project aims at understanding the impact of drought, pest infestations and disease outbreaks on crop productivity. The analysis will help identify patterns, vulnerabilities, and potential interventions to improve food security in the region.

Objectives
Develop data-driven insights and recommendations to enhance crop productivity in Karamoja
Identify the crops doing well in Karamoja despite the adverse conditions
Identify the crops that have the least productivity in order to come up with ways to improve their productivity
keyboard_arrow_down
Description of dataset
OBJECTID :unique object ID
DISTRICT:district under study
SUBCOUNTY NAME:name of subcounty under study
POP X:total population for subcounty X
Area x:area of X under study
S Yield Ha x:average yield for sorghum for subcounty X(Kg/Ha)
M Yield Ha x: average yield for maize for subcounty X(Kg/Ha)
Crop Area Ha x:total crop area for subcounty X(Ha)
S Area Ha x:total sorghum crop area for subcounty X(Ha)
M Area Ha x:total maize crop area for subcounty X(Ha)
S Prod Tot x:total productivity for the sorghum for subcounty X(Kg)
POP y:total population for subcounty Y
M Prod Tot x:total productivity for the maize for subcounty X(Kg)
Area y:Area of Y under study
S Yield Ha y:average yield for sorghum for subcounty Y
M Yield Ha y:average yield for maize for subcounty Y
Crop Area Ha y:total crop area for subcounty Y(Ha)
S Area Ha y:total sorghum crop area for subcounty Y(Ha)
M Area Ha y:total maize crop area for subcounty Y(Ha)
S Prod Tot y:total productivity for the sorghum for subcounty Y(Kg)
M Prod Tot y:total productivity for the maize for subcounty Y(Kg)
#impoting necessary librariesimport pandas as pdimport numpy as npimport matplotlib.pyplot as pltimport seaborn as sns

keyboard_arrow_down
Datasets Used
Uganda Karamoja District Crop Yield Population
Uganda Karamoja Subcounty Crop Yield Population
Loading the datasets

#Loading dataset 1df1= pd.read_csv('/content/Uganda_Karamoja_District_Crop_Yield_Population.csv')#display first five rowsdf1.head()


#Renaming name column
df1.rename(columns={'NAME':'DISTRICT'},inplace=True)
df1.head()


#Loading dataset 2
df2= pd.read_csv('/content/Uganda_Karamoja_Subcounty_Crop_Yield_Population.csv')
#display first five rows
df2.head()

#Renaming column district column
df2.rename(columns={'DISTRICT_NAME':'DISTRICT'},inplace=True)
df2.head()

Renaming of the name and district name columns in the first and second dataset to read district is to provide a common column for merging.

keyboard_arrow_down
Merging the datasets
This is to make the work appear cleaner

  #merging the two datasets
  merged_df= pd.merge(df1,df2,on='DISTRICT',how="inner")
  merged_df.head()



#viewing column names
merged_df.columns
Index(['OBJECTID_x', 'DISTRICT', 'POP_x', 'Area_x', 'S_Yield_Ha_x',
       'M_Yield_Ha_x', 'Crop_Area_Ha_x', 'S_Area_Ha_x', 'M_Area_Ha_x',
       'S_Prod_Tot_x', 'M_Prod_Tot_x', 'OBJECTID_y', 'SUBCOUNTY_NAME', 'POP_y',
       'Area_y', 'Karamoja', 'S_Yield_Ha_y', 'M_Yield_Ha_y', 'Crop_Area_Ha_y',
       'S_Area_Ha_y', 'M_Area_Ha_y', 'S_Prod_Tot_y', 'M_Prod_Tot_y'],
      dtype='object')
print(merged_df.shape)
print(merged_df.info())

(52, 23)
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 52 entries, 0 to 51
Data columns (total 23 columns):
 #   Column          Non-Null Count  Dtype  
---  ------          --------------  -----  
 0   OBJECTID_x      52 non-null     int64  
 1   DISTRICT        52 non-null     object 
 2   POP_x           52 non-null     int64  
 3   Area_x          52 non-null     int64  
 4   S_Yield_Ha_x    52 non-null     int64  
 5   M_Yield_Ha_x    52 non-null     int64  
 6   Crop_Area_Ha_x  52 non-null     float64
 7   S_Area_Ha_x     52 non-null     float64
 8   M_Area_Ha_x     52 non-null     float64
 9   S_Prod_Tot_x    52 non-null     int64  
 10  M_Prod_Tot_x    52 non-null     int64  
 11  OBJECTID_y      52 non-null     int64  
 12  SUBCOUNTY_NAME  52 non-null     object 
 13  POP_y           52 non-null     int64  
 14  Area_y          52 non-null     int64  
 15  Karamoja        52 non-null     object 
 16  S_Yield_Ha_y    52 non-null     float64
 17  M_Yield_Ha_y    52 non-null     float64
 18  Crop_Area_Ha_y  52 non-null     float64
 19  S_Area_Ha_y     52 non-null     float64
 20  M_Area_Ha_y     52 non-null     float64
 21  S_Prod_Tot_y    52 non-null     float64
 22  M_Prod_Tot_y    52 non-null     float64
dtypes: float64(10), int64(10), object(3)
memory usage: 9.5+ KB
None
keyboard_arrow_down
Data Cleaning
Cleaning of data ensures the good quality and reliability of our analysis. There are various methods of cleaning data. These include: Handling missing values, handling duplicates, standardizing data, removing unnecessary columns, renaming columns etc.

#checking for null values
merged_df.isnull().sum()

#checking for duplicates
merged_df.duplicated().sum()
0
 #removing underscores on column names
 merged_df.columns= merged_df.columns.str.replace('_','')
 merged_df.head()

#removing unnecessary columns
merged_df.drop(['OBJECTIDx','OBJECTIDy','Karamoja'],axis=1,inplace=True)
merged_df.head()


#Ensuring uniformity of data by imposing standard decimal places
merged_df= merged_df.round(2)
merged_df.head()

#exporting our cleaned dataset
merged_df.to_csv('cleaned_dataset.csv',index=False)
keyboard_arrow_down
Data Exploration
To get a quick overview of our new dataset after merging and cleaning.

#x represents districts
#y represents sublocations
#show first seven rows of the dataset
merged_df.head(7)

#show last 3 rows of the dataset
merged_df.tail(3)

print(merged_df.info())
print(merged_df.shape)
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 52 entries, 0 to 51
Data columns (total 20 columns):
 #   Column         Non-Null Count  Dtype  
---  ------         --------------  -----  
 0   DISTRICT       52 non-null     object 
 1   POPx           52 non-null     int64  
 2   Areax          52 non-null     int64  
 3   SYieldHax      52 non-null     int64  
 4   MYieldHax      52 non-null     int64  
 5   CropAreaHax    52 non-null     float64
 6   SAreaHax       52 non-null     float64
 7   MAreaHax       52 non-null     float64
 8   SProdTotx      52 non-null     int64  
 9   MProdTotx      52 non-null     int64  
 10  SUBCOUNTYNAME  52 non-null     object 
 11  POPy           52 non-null     int64  
 12  Areay          52 non-null     int64  
 13  SYieldHay      52 non-null     float64
 14  MYieldHay      52 non-null     float64
 15  CropAreaHay    52 non-null     float64
 16  SAreaHay       52 non-null     float64
 17  MAreaHay       52 non-null     float64
 18  SProdToty      52 non-null     float64
 19  MProdToty      52 non-null     float64
dtypes: float64(10), int64(8), object(2)
memory usage: 8.2+ KB
None
(52, 20)
#getting summary statistics to 2 decimal places
merged_df.describe().round(2)


 #checking column labels of cleaned dataset
 merged_df.columns
Index(['DISTRICT', 'POPx', 'Areax', 'SYieldHax', 'MYieldHax', 'CropAreaHax',
       'SAreaHax', 'MAreaHax', 'SProdTotx', 'MProdTotx', 'SUBCOUNTYNAME',
       'POPy', 'Areay', 'SYieldHay', 'MYieldHay', 'CropAreaHay', 'SAreaHay',
       'MAreaHay', 'SProdToty', 'MProdToty'],
      dtype='object')
keyboard_arrow_down
Data analysis
#total maize production in the districts
merged_df['MProdTotx'].sum()
247828278
#total sorghum production in the districts
merged_df['SProdTotx'].sum()
267425528
#total maize production in subcounties
merged_df['MProdToty'].sum()
28603794.869999997
#total sorghum production in subcounties
merged_df['SProdToty'].sum()
34098704.79
#District with highest maize production
merged_df[merged_df['MProdTotx']==merged_df['MProdTotx'].max()]

#District with the lowest maize production
merged_df[merged_df['MProdTotx']==merged_df['MProdTotx'].min()]

#District with the highest sorgum production
merged_df[merged_df['SProdTotx']==merged_df['SProdTotx'].max()]

#District with the lowest sorghum production
merged_df[merged_df['SProdTotx']==merged_df['SProdTotx'].min()]

#Subcounty with the highest maize production
merged_df[merged_df['MProdToty']==merged_df['MProdToty'].max()]

#Subcounty with the lowest maize production
merged_df[merged_df['MProdToty']==merged_df['MProdToty'].min()]

#Subcounty with the highest sorghum production
merged_df[merged_df['SProdToty']==merged_df['SProdToty'].max()]

#Subcounty with the lowest sorghum production
merged_df[merged_df['SProdToty']==merged_df['SProdToty'].min()]

#List different districts in the dataset
merged_df['DISTRICT'].unique()
array(['ABIM', 'AMUDAT', 'KAABONG', 'KOTIDO', 'MOROTO', 'NAKAPIRIPIRIT',
       'NAPAK'], dtype=object)
#total population in each district
merged_df.groupby('DISTRICT')['POPx'].sum()

#total maize and sorghum production in districts
merged_df.groupby('DISTRICT')[['MProdTotx','SProdTotx']].sum()

#district with lowest maize production to population ratio
merged_df[merged_df['MProdTotx']/merged_df['POPx']==merged_df['MProdTotx']/merged_df['POPx'].min()]



#district with highest maize production to population ratio
merged_df[merged_df['MProdTotx']/merged_df['POPx']==merged_df['MProdTotx']/merged_df['POPx'].max()]

Conclusion
District withe highest Maize production is Nakapiririt.
District with the lowest maize production is Moroto
District with the highest sorghum production is Kotido
District with the lowest sorghum production is Moroto
Recommendations
Develop an alert system that automatically notifies farmers and NGOs of emerging threats such as droughts, pests, or diseases based on predictive models.
Promote the cultivation of drought-resistant varieties of sorghum and maize.
Focus on educating farmers about best practices in drought management, soil health improvement, and pest control.
Develop heatmaps of crop productivity, identifying high-risk zones that require urgent attention, allowing NGOs to allocate resources more effectively.
Colab paid products - Cancel contracts here
merged_df[merged_df['MProdTotx']/merged_df['POPx']==merged_df['MProdTotx']/merged_df['POPx'].max()]
