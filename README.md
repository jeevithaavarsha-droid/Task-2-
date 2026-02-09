# Step 1: Import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Step 2: Load dataset
data = pd.read_csv("Students Social Media Addiction.csv")

# Step 3: View dataset
data.head()

# Step 4: Dataset information
data.info()

# Step 5: Check missing values
data.isnull().sum()

# Step 6: Fill missing values (numeric columns)
for col in data.select_dtypes(include="number").columns:
    data[col] = data[col].fillna(data[col].mean())

# Step 7: Fill missing values (categorical columns)
for col in data.select_dtypes(include="object").columns:
    data[col] = data[col].fillna(data[col].mode()[0])

# Step 8: Remove duplicate rows
data = data.drop_duplicates()

# ---------------- EDA ----------------

# Step 9: Age Distribution (Histogram)
if "Age" in data.columns:
    plt.hist(data["Age"], bins=10)
    plt.title("Age Distribution")
    plt.xlabel("Age")
    plt.ylabel("Number of Students")
    plt.show()

# Step 10: Gender Distribution (Bar Chart)
if "Gender" in data.columns:
    data["Gender"].value_counts().plot(kind="bar")
    plt.title("Gender Distribution")
    plt.xlabel("Gender")
    plt.ylabel("Count")
    plt.show()

# Step 11: Daily Usage Hours Distribution
if "Daily Usage Hours" in data.columns:
    plt.hist(data["Daily Usage Hours"], bins=10)
    plt.title("Daily Social Media Usage Hours")
    plt.xlabel("Hours per Day")
    plt.ylabel("Number of Students")
    plt.show()

# Step 12: Gender vs Addiction Level
if "Gender" in data.columns and "Addiction Level" in data.columns:
    sns.countplot(x="Gender", hue="Addiction Level", data=data)
    plt.title("Gender vs Addiction Level")
    plt.show()

# Step 13: Correlation Heatmap
plt.figure(figsize=(8,6))
sns.heatmap(data.corr(numeric_only=True), annot=True, cmap="coolwarm")
plt.title("Correlation Matrix")
plt.show()
