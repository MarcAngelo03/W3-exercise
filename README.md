# W3-exercise
Take the Week 2 project and formalize it into a collaborative repo
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

print("1 - Calculator")
print("2 - Load & Analyze Dataset")
option = int(input("Choose an option: "))

# -------------------------------------------------------
# CALCULATOR SECTION
# -------------------------------------------------------
if option == 1:
    print("Choose an operation:")
    print("1 - Addition")
    print("2 - Subtraction")
    print("3 - Multiplication")
    print("4 - Division")
    option  = int(input("Choose an operation: "))

    if option  in [1, 2, 3, 4]:
        num1 = float(input("Enter 1st Number: "))
        num2 = float(input("Enter 2nd Number: "))

        if option  == 1:
            result = num1 + num2
        elif option  == 2:
            result = num1 - num2
        elif option  == 3:
            result = num1 * num2
        elif option  == 4:
            result = num1 / num2

        print("Result:", result)
    else:
        print("Invalid operation")

# -------------------------------------------------------
# DATA HANDLING SECTION
# -------------------------------------------------------
elif option == 2:
    print("Dataset Mode")

    # Load dataset
    try:
        fpath = "C:\\Users\\USER\\Desktop\\Book1.csv"
        df = pd.read_csv(fpath)
        print(df.head())
    except Exception as e:
        print("Error loading file:", e)
        exit()

    # Cleaning Example
    print("\nChecking for missing values...")
    print(df.isnull().sum())

    print("\nDropping rows with missing values...")
    df = df.dropna()

    # Transformation Example
    print("\nAdding a new column (numeric summary)...")
    df["row_sum"] = df.select_dtypes(include=np.number).sum(axis=1)

    print(df.head())

    # Visualization Menu
    print("\nChoose a visualization:")
    print("1 - Histogram (Numeric Column)")
    print("2 - Correlation Heatmap")
    print("3 - Scatter Plot")

    vis = int(input("Select: "))

    if vis == 1:
        column = input("Enter numeric column name: ")
        df[column].hist()
        plt.title(f"Histogram of {column}")
        plt.show()

    elif vis == 2:
        plt.figure(figsize=(10, 6))
        numeric_df = df.select_dtypes(include=[np.number])
        sns.heatmap(numeric_df.corr(), annot=True)
        plt.title("Correlation Heatmap")
        plt.show()

    elif vis == 3:
        x = input("X column: ")
        y = input("Y column: ")
        sns.scatterplot(data=df, x=x, y=y)
        plt.title(f"{x} vs {y}")
        plt.show()

    else:
        print("Invalid visualization option")

else:
    print("Invalid menu option!")
