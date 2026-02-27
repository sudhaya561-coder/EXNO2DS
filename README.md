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
        <<INCLUDE YOUR CODING AND OUTPUT SCREENSHOTS>>
      import pandas as pd
      import numpy  as np
      import seaborn as sns
      import matplotlib.pyplot as plt
      import pandas as pd   
      
      data = pd.read_csv("titanic_dataset.csv")
      print("\nDataset Loaded Successfully\n")
      print(data.head())
      print("\nDataset Info:\n")
      data.info()
      print("\nDataset Description:\n")
      print(data.describe())

      for column in data.columns:
    if data[column].dtype == 'object':
        data[column] = data[column].fillna(data[column].mode()[0])   # Mode for categorical
    else:
        data[column] = data[column].fillna(data[column].median())   # Median for numerical
      print("\nMissing values handled successfully.\n")

      plt.figure(figsize=(6,4))
      sns.boxplot(x=data["Age"],color="gold")
      plt.title("Boxplot - Age")
      plt.show()

      plt.figure(figsize=(6,4))
      sns.boxplot(x=data["Fare"],color="magenta")
      plt.title("Boxplot - Fare")
      plt.show()

       def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]
      data = remove_outliers_iqr(data, "Age")
      data = remove_outliers_iqr(data, "Fare")
      print("Outliers removed using IQR method.\n")
      
      plt.figure(figsize=(6,4))
      sns.countplot(x="Survived", data=data)
      plt.title("Countplot - Survival Distribution")
      plt.show()

      plt.figure(figsize=(6,4))
      sns.countplot(x="Sex", data=data)
      plt.title("Countplot - Gender Distribution")
      plt.show()

      plt.figure(figsize=(6,4))
      sns.countplot(x="Pclass", data=data)
      plt.title("Countplot - Passenger Class Distribution")
      plt.show()

      sns.displot(data["Age"], kde=True, height=4, aspect=1.5,color="cyan")
      plt.title("Displot - Age Distribution")
      plt.show()

      sns.displot(data["Fare"], kde=True, height=4, aspect=1.5,color="red")
      plt.title("Displot - Fare Distribution")
      plt.show()

      print("\nCross Tabulation: Sex vs Survived\n")
      print(pd.crosstab(data["Sex"], data["Survived"]))
      print("\nCross Tabulation: Pclass vs Survived\n")
      print(pd.crosstab(data["Pclass"], data["Survived"]))

      plt.figure(figsize=(8,6))
      correlation_matrix = data.select_dtypes(include=np.number).corr()
      sns.heatmap(
          correlation_matrix,
          annot=True,                # show values
          fmt=".2f",                 # 2 decimal places
          cmap="RdYlGn",            # multi-color palette
            linewidths=1,              # edge thickness
          linecolor="black",         # edge color
          square=True,               # square cells
          cbar=True                  # color bar
      )
      plt.title("Correlation Heatmap - Titanic Dataset")
      plt.show()
      
[exp2.pdf](https://github.com/user-attachments/files/25596199/exp2.pdf)

<img width="635" height="514" alt="Screenshot 2026-02-27 114108" src="https://github.com/user-attachments/assets/17627a04-5208-4708-aab9-e61a15b68589" />
<img width="637" height="510" alt="Screenshot 2026-02-27 114115" src="https://github.com/user-attachments/assets/b9493ded-fe64-4f62-a011-fc5adba65fb7" />
<img width="694" height="493" alt="Screenshot 2026-02-27 114122" src="https://github.com/user-attachments/assets/daac1092-bf88-4d39-9257-36a60ba7133d" />
<img width="740" height="518" alt="Screenshot 2026-02-27 114131" src="https://github.com/user-attachments/assets/3c55c0e5-e41a-4974-b6b7-d03aa52c0240" />
<img width="869" height="706" alt="Screenshot 2026-02-27 114141" src="https://github.com/user-attachments/assets/684b16ee-0a27-4a5e-8e8f-1d48702386ba" />

### Result:
sucessfully performed Exploratory Data Analysis on the given data set.


