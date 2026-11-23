# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

data = pd.read_csv(r"C:\Users\acer\Downloads\titanic_dataset.csv")

print(data.head())
print(data.info())
print(data.isnull().sum())

data['Age'] = data['Age'].fillna(data['Age'].median())
data['Embarked'] = data['Embarked'].fillna(data['Embarked'].mode()[0])
data['Cabin'] = data['Cabin'].fillna('Unknown')

print("Missing values handled.")

sns.boxplot(x=data['Fare'])
plt.title("Boxplot - Fare")
plt.xlabel("Fare")
plt.show()

def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(data, 'Fare')
print("Outliers removed using IQR method.")

sns.countplot(x='Sex', data=data)
plt.title("Countplot - Gender Distribution")
plt.show()

sns.displot(data['Age'], kde=True)
plt.title("Displot - Age Distribution")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()

crosstab_result = pd.crosstab(data['Sex'], data['Survived'])
print("\nCross Tabulation Result:")
print(crosstab_result)

correlation_matrix = data.select_dtypes(include=np.number).drop(
    columns=['PassengerId'], errors='ignore'
).corr()

sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()
```

# Box plot
<img width="648" height="577" alt="Screenshot 2026-11-23 151238" src="https://github.com/user-attachments/assets/1a00b4b7-ce66-4a18-8233-df71a51a8cc5" />
```


```

# Countplot
<img width="707" height="567" alt="Screenshot 2026-11-23 151344" src="https://github.com/user-attachments/assets/f462462e-d97b-4a9d-adc3-1e63b795238c" />
```


```

# Displot
<img width="605" height="632" alt="Screenshot 2026-11-23 151435" src="https://github.com/user-attachments/assets/23d52ace-9084-4642-af58-2d1a6d6e827b" />


```
```
# Correlation Heatmap
<img width="652" height="527" alt="Screenshot 2026-11-23 151501" src="https://github.com/user-attachments/assets/8e6633e5-278e-4bf7-b3eb-2c80413e0967" />
```
# RESULT
This project analyzes the Titanic dataset using Python, Pandas, NumPy, Seaborn, and Matplotlib.
It performs data cleaning, handles missing values, identifies outliers, and visualizes survival patterns.
