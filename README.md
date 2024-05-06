# Exno:1 Data Cleaning Process

# AIM:
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation:
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm:
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
Name : Lingasri P
Register No : 212221040089
```
### Data Cleaning:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![309301073-3ca587d6-9eab-4809-be07-6fecb7d38144](https://github.com/Kowsalyasathya/exno1/assets/118671457/bb7ce684-3c79-4163-8b0f-115ae9cb7e92)

```
data = pd.get_dummies(data)
data.isnull().sum()
```
![309301121-5376ecdf-49bd-44cf-bfb0-c814590c8144](https://github.com/Kowsalyasathya/exno1/assets/118671457/91b09028-7061-401a-9328-af63c39c7f6a)

![image](https://github.com/Kowsalyasathya/exno1/assets/118671457/faac1587-d627-4e52-97b0-0bfb4a693e71)
```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![309301192-b1022155-ea0a-4187-b06f-a78375303d43](https://github.com/Kowsalyasathya/exno1/assets/118671457/7e44373e-5688-41ad-bb0e-98fcb43790f7)
```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
![309301238-c63d7324-1c97-49cb-a6a7-ecee861c386b](https://github.com/Kowsalyasathya/exno1/assets/118671457/2bdafb33-ad4e-4fad-bb2a-872078c8c2bd)
### IQR:
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![309301294-a12a23d1-ce37-46cc-9c29-f2df411b4170](https://github.com/Kowsalyasathya/exno1/assets/118671457/715fba3c-9f64-43ac-8484-2360a47309a8)
```
ir.describe()
```
![309301334-0f478b80-2e6f-4115-acac-10468ed9b39c](https://github.com/Kowsalyasathya/exno1/assets/118671457/93138dbc-9ef8-4259-8741-35823209d891)
```
sns.boxplot(x='sepal_width',data=ir)
```
![309301362-4eb55cb6-bf9f-47bf-8f97-c5a11edd0876](https://github.com/Kowsalyasathya/exno1/assets/118671457/39d5f85b-387a-422b-a332-a98d8d712066)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![309301391-9e5ac1f7-f414-4799-bd30-be914233d1a3](https://github.com/Kowsalyasathya/exno1/assets/118671457/43f8ddab-6d8e-4cae-9368-80ab9c68ad54)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![309301412-9765bd3c-5836-487b-8e81-564a8802aca9](https://github.com/Kowsalyasathya/exno1/assets/118671457/87415875-af60-4701-bbd5-a9fd5de8bd16)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![309301434-45fcdef3-e491-449b-afdc-c44153092c50](https://github.com/Kowsalyasathya/exno1/assets/118671457/452b65ed-3001-49e6-8361-7367fad75712)
```
sns.boxplot(x='sepal_width',data=delid)
```
![309301455-69078496-2736-4ecd-9e19-e03d1738622b](https://github.com/Kowsalyasathya/exno1/assets/118671457/7415fe8d-aff1-4552-ae44-2c93b29a1cf4)
### Z SCORE:
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```

![309301483-85a422ca-4fac-4db4-a32d-4a1508d736b8](https://github.com/Kowsalyasathya/exno1/assets/118671457/63b287a2-5528-4fae-a166-8d7fc7be13ba)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```
iqr = q3-q1
iqr
```

![309301503-264e6e9e-2f8b-47df-a3e8-33db992a783d](https://github.com/Kowsalyasathya/exno1/assets/118671457/850b3546-0082-4905-a4da-2c6266e829b0)

```
low = q1 - 1.5*iqr
low
```

![309301554-a80f4578-fc2b-4ca0-a524-6a05b12b8539](https://github.com/Kowsalyasathya/exno1/assets/118671457/bcc395a5-44a9-4a9a-a9cd-9ac65d008d49)

```
high = q3 + 1.5*iqr
high
```

![309301584-1a56212e-cc6f-40e8-80e0-2d918b356919](https://github.com/Kowsalyasathya/exno1/assets/118671457/b5eb3cbc-84b9-48d7-b07f-637afc3c616f)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1

```
![309301615-7610c576-d3f6-4955-99b6-c0ec48183986](https://github.com/Kowsalyasathya/exno1/assets/118671457/b9b1a265-7f90-4a0d-a2ec-3f5be2609f87)

```
z = np.abs(stats.zscore(df['height']))
z
```

![309301639-29ca2a73-2b45-4de4-a538-0795024c5d55](https://github.com/Kowsalyasathya/exno1/assets/118671457/9bf8eff7-dec5-4736-b4ef-03f10fc6064f)

## Result:
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
