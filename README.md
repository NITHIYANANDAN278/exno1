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
           
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/db18d883-b43d-4c93-a831-8272be520df9)
```
df.shape
```
![image](https://github.com/user-attachments/assets/649f6b11-1266-465a-8ae3-13e3cd055b8c)

```
df.describe()
```
![image](https://github.com/user-attachments/assets/1a6f832d-19d7-41ad-9dc8-3d4af512cc18)
```
df.info()
```
![image](https://github.com/user-attachments/assets/bcc39755-d3e0-4fea-8a53-e29cdc6f585c)
```
df.head(3)
df.tail(3)
```
![image](https://github.com/user-attachments/assets/e30a32c7-8328-405e-94b4-950a44e091e0)
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/5cf1c40d-1c1b-42d8-97ca-3f4761fc0b6b)
```
df.dropna(how='any').shape
```
![image](https://github.com/user-attachments/assets/be78766d-49d8-4612-b8c6-f43b25997c3b)
```
df.shape
```
![image](https://github.com/user-attachments/assets/c93b7cad-87cf-40d4-899c-7f05d2af67d8)
```
mn=df.TOTAL.mean()
mn
```
![image](https://github.com/user-attachments/assets/637a75fd-7d90-4713-b154-1f23b9373224)
```
df.TOTAL.fillna(mn,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/1f192dc9-17b9-438b-bd0a-4fac63308e08)
```
df['M1'].fillna(method='FFill',inplace=True)
df.M1
```
![image](https://github.com/user-attachments/assets/99fa5f13-d3f2-4af5-8e39-337ab53d0fd7)
```
df.M1.dropna(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/a835c289-87dc-4777-bef2-f8d85959d0e7)
```
df.fillna(method='ffill',inplace=True)
df
```
![image](https://github.com/user-attachments/assets/c81220ef-7d4d-41d6-abbc-b2f7bfe32b93)
```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/3c2a2ca9-bffa-4842-9fc2-7e246ca42af0)
```
df.drop_duplicates(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/990b5e7a-e7bb-46ae-bee8-5806a1968d53)
```
df['DOB']
```
![image](https://github.com/user-attachments/assets/eccfb6bb-f24c-4a75-978e-63afaf17c890)
```
df['DOB']=pd.to_datetime(df['DOB'],format='%y.%m,%d',errors='coerce')
df
```
![image](https://github.com/user-attachments/assets/50656676-60d4-441c-8557-846fd267af9c)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/e536b2da-f3d3-4db7-8d6e-ac0539ef05a5)
```
import pandas as pd
import seaborn as sns
import numpy as np
```
```
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/df460537-7ffd-4fdb-9e82-54de2776ee24)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/27285355-0916-4d1f-adc8-17930b96735a)
```
sns.scatterplot(data=af)
```
![image](https://github.com/user-attachments/assets/582e0036-07b8-4940-8e04-278718d3654b)
```
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/8d77236f-c433-4fc5-874a-4940516e2c57)
```
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
![image](https://github.com/user-attachments/assets/80405a03-1d01-4fdb-8bc7-ed6e8b5bf1e0)
```
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
```
```
lower_bound
```
![image](https://github.com/user-attachments/assets/f7accad2-e2d9-4f25-95b1-bbac1416f20b)
```
upper_bound
```
![image](https://github.com/user-attachments/assets/262b93ff-c0e1-4567-9081-5936c698e17b)
```
outlier=[x for x in age if x < lower_bound or x > upper_bound]
```
```
print("Q1 : ",Q1)
print("Q3 : ",Q3)
print("IQR : ",IQR)
print("lower bound : ",lower_bound)
print("upper bound : ",upper_bound)
print("outliers : ",outlier)
```
![image](https://github.com/user-attachments/assets/94c800ba-92c3-4481-8fbb-a2021324712b)
```
af=af[((af>=lower_bound)&(af<=upper_bound))]
```
```
af.dropna()
```
![image](https://github.com/user-attachments/assets/bbd50f9b-c0a0-4135-98b7-e6c9e7aa80c4)
```

data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
![image](https://github.com/user-attachments/assets/99b61f32-950b-4eae-9b3d-f069bc99b835)
```
threshold=3
outliers=[]
for i in data:
  z=(i-mean)/std
  if z > threshold:
    outliers.append(i)
    print('outlier in dataset is',outliers)
```
![image](https://github.com/user-attachments/assets/0c1fced3-6226-4fe9-87d9-c6b4ff78d679)
```
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
```
```
import pandas as pd
import numpy as np
import seaborn as sns
```
```
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
```
```
df=pd.DataFrame(data)
df
```
![image](https://github.com/user-attachments/assets/57e018e9-6400-45d5-8183-3cc6264a3ebb)
```
from scipy import stats
```
```
z = np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
![image](https://github.com/user-attachments/assets/60e8aac8-c900-40e8-beb6-aae44c744a38)




# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score
method.
