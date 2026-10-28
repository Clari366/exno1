# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

##  Data Cleaning
#### READ CSV FILE 
   ```
import pandas as pd
df=pd.read_csv('/content/Loan_data.csv')
df
```
<img width="1808" height="773" alt="image" src="https://github.com/user-attachments/assets/127c05e7-6d7e-45c8-ade8-d6902c618578" />

#### DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS


```
df.info()
```

<img width="973" height="598" alt="image" src="https://github.com/user-attachments/assets/e4ed1655-5fc8-4020-b601-63110d9359ac" />

```
df.describe()
```
<img width="991" height="524" alt="image" src="https://github.com/user-attachments/assets/6b033023-c648-4dea-bfdf-7fe8bb0d9074" />


#### CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
```
df.isnull()
```
<img width="1795" height="711" alt="image" src="https://github.com/user-attachments/assets/35c60caa-fc44-4934-b881-db8ebc5bba48" />


#### DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
df.isnull().sum()
```
<img width="525" height="726" alt="image" src="https://github.com/user-attachments/assets/cb6e8d6f-c72e-4c42-bc01-b5d95ce0e374" />



#### DROP NULL VALUES
```
df_dropped=df.dropna()
df_dropped
```
<img width="1773" height="792" alt="image" src="https://github.com/user-attachments/assets/c5c6b2b7-7d80-49c9-9b45-180a428798bc" />


#### FILL NULL VALUES WITH CONSTANT VALUE "O"
     
```
df_fill_0=df.fillna(0)
df_fill_0
```
<img width="1753" height="772" alt="image" src="https://github.com/user-attachments/assets/182d316f-a245-4ced-a573-1a22e7a52ac9" />



#### FILL NULL VALUES WITH ffill or bfill METHOD
```
df_ffill=df.ffill()
df_ffill
```
<img width="1776" height="787" alt="image" src="https://github.com/user-attachments/assets/74cc54c9-faa3-4ae7-bc16-475a9361b54e" />

```
df_bfill=df.bfill()
df_bfill
```
<img width="1787" height="799" alt="image" src="https://github.com/user-attachments/assets/d1439f45-19a5-4ea2-bac0-a1d64ac75441" />



#### CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
```
df_new=df
df_new['LoanAmount']=df['LoanAmount'].fillna((df['LoanAmount']).mean)
df_new['Loan_Amount_Term']=df['Loan_Amount_Term'].fillna((df['Loan_Amount_Term']).mean)
df_new
```
<img width="1792" height="816" alt="image" src="https://github.com/user-attachments/assets/3799894c-5607-4922-b2d2-8db26a1d3954" />



#### DROP NULL VALUES
     

```
df_new.dropna(axis=0)
```
<img width="1806" height="717" alt="image" src="https://github.com/user-attachments/assets/83eabe07-ee44-492c-8f9a-354a15e058c5" />


## Outlier Detection and Removal
```
import pandas as pd
import seaborn as sns
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
<img width="429" height="626" alt="image" src="https://github.com/user-attachments/assets/3f658d3a-9548-4943-b02b-19b61fc00b4c" />



#### USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER

```
sns.boxplot(data=af)
```
<img width="857" height="609" alt="image" src="https://github.com/user-attachments/assets/d597f887-f8d6-44d3-9dee-6835e3cf682e" />



#### PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
import numpy as np
Q1=np.percentile(age,25)
Q2=np.percentile(age,50)
Q3=np.percentile(age,75)
```
```
IRO=Q3-Q1
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
outliers=af[(af<lower_bound) | (af>upper_bound) ]
```
```
print("Quantile 1",Q1)
print("Quantile 2",Q2)
print("Quantile 3",Q3)
print("Inter Quartile Range",IQR)
print("Lower Bound",lower_bound)
print("Upper Bound",upper_bound)
print("Outliers",outliers)
```
<img width="391" height="468" alt="image" src="https://github.com/user-attachments/assets/bf5d8bbd-1b84-4f4e-8e5d-c42ff3da1a2c" />

#### REMOVE OUTLIERS
```
af=af[(af>=lower_bound) & (af<=upper_bound)]
af.dropna()
print("After removing outliers")
af
```
<img width="814" height="834" alt="image" src="https://github.com/user-attachments/assets/610e1848-7e88-48cf-a4f7-0f5c7af8cab6" />

#### USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED


```
sns.boxplot(data=af)
```
<img width="807" height="647" alt="image" src="https://github.com/user-attachments/assets/1598ba6c-68e6-4d2f-aeca-36d972ea4e47" />


#### USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
```
from scipy import stats
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data)
sns.boxplot(data=df)
```

<img width="1150" height="699" alt="image" src="https://github.com/user-attachments/assets/546b9fb6-04f4-4463-a6d9-e1d89cf680cb" />


#### PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
```
z=np.abs(stats.zscore(data))
print("Outlier values:")
outliers=df[z>3]
outliers
```
<img width="524" height="359" alt="image" src="https://github.com/user-attachments/assets/ba4880a0-0004-49f0-b79c-532c18998469" />


#### REMOVE OUTLIERS
```
cleaned_df=df[z<3]
print("After removing outliers")
cleaned_df
```
<img width="887" height="832" alt="image" src="https://github.com/user-attachments/assets/25787c87-7d3a-4be5-9d54-898e11091760" />


#### USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```
sns.boxplot(data=cleaned_df)
```

<img width="1203" height="687" alt="image" src="https://github.com/user-attachments/assets/5f628e1f-8d53-4107-911a-fcbc7fb319cc" />




# Result
Thus the data cleaning process on the given dataset is executed successfully.




# Summary:

[Experiment_1_Data_Cleaning_Summary.pdf](https://github.com/user-attachments/files/34013174/Experiment_1_Data_Cleaning_Summary.pdf)

