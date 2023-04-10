# Ex02-Outlier

You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,

(1) Remove outliers using IQR 

(2) After removing outliers in step 1, you get a new dataframe.

(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result

(4) for the data set height_weight.csv find the following

    (i) Using IQR detect weight outliers and print them

    (ii) Using IQR, detect height outliers and print them
    
AIM:

TO detect and remove the outliers in the given data set and save the final data.

Algorithm:

Step 1

Import the required packages(pandas,numpy,scipy)

Step 2

Read the given csv file

Step 3

Convert the file into a dataframe and get information of the data.

Step 4
Remove the non numerical data columns using drop() method.

Step 5

Detect the outliers in the data set using z scores method.

Step 6

Remove the outliers by z scores and list manupilation or by using Interquartile Range(IQR)

Step 7

Check if the outliersare removed from data set using graphical methods.

Step 8

Save the final data set into the file.
    
    
``` 
DEVELOPED BY: BALA MURUGAN P
REFERENCE NO: 212222230017
import pandas as pd
import seaborn as sns
import numpy as np
from scipy import stats
df=pd.read_csv('bhp.csv')
print(df['price_per_sqft'])
sns.boxplot(x="price_per_sqft",data=df)
df.shape
```

```
q1=df['price_per_sqft'].quantile(0.25)
q3=df['price_per_sqft'].quantile(0.75)
iqr=q3-q1
print("FIRST QUANTILE=",q1,"\nSECOND QUANTILE=",q3)
low=q1-1.5*iqr
high=q3+1.5*iqr
df_filtered=df[((df['price_per_sqft']>=low)&(df['price_per_sqft']<=high))]
sns.boxplot(x="price_per_sqft",data=df_filtered)
```

```
from scipy import stats
import numpy as np
z=np.abs(stats.zscore(df['price_per_sqft']))
df_filtered=df_filtered[(z<3)]
sns.boxplot(x='price_per_sqft',data=df_filtered)
```

```
q1=df.quantile(0.25)
q3=df.quantile(0.75)
iqr=q3-q1
low=q1-1.5*iqr
high=q3+1.5*iqr
df_fil=df[((df<=high)&(df>=low))]
outliers=np.setdiff1d(df['weight'],df_fil['weight'])
print("THE OUTLIERS IN THE DATA SET WEIGHT:",outliers)
```

```
q1=df.quantile(0.25)
q3=df.quantile(0.75)
iqr=q3-q1
low=q1-1.5*iqr
high=q3+1.5*iqr
df_fil=df[((df<=high)&(df>=low))]
outliers=np.setdiff1d(df['height'],df_fil['height'])
print("THE OUTLIERS IN THE DATA SET height:",outliers)
```

![aa](https://user-images.githubusercontent.com/118680410/227790376-0249836a-1815-4be8-8083-49fd6cdb9f68.png)

![bb](https://user-images.githubusercontent.com/118680410/227790395-08526e51-0aba-4670-9c34-3f31ef2fdbf2.png)

![cc](https://user-images.githubusercontent.com/118680410/227790403-52258caf-87e8-469e-9750-b9a135b985d1.png)

![dd](https://user-images.githubusercontent.com/118680410/227790420-daa0d07b-8b38-4b56-aeb1-961d426f6b36.png)

![ee](https://user-images.githubusercontent.com/118680410/227790441-cd68c41b-1aea-4829-a651-db5924d496cc.png)

