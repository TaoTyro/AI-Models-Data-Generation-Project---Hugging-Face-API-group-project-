# AI Model Release Trends Analysis (Hugging Face)

This README is **directly from the project Jupyter Notebook (`ict.ipynb`)** and documents each processing step **with the actual code snippets used** in the original projects' Notebook.

---

## 📌 Project Description

This project analyzes trends in AI model releases using metadata retrieved from the **Hugging Face public API**. The focus is on identifying dominant AI model categories and popularity indicators such as downloads, likes, and trending scores.

---

## 📁 Project Structure

```text
data_generation/
│
├── ict.ipynb              # Main analysis notebook
├── models.json            # Raw API data
├── cleaned_model_data.csv # Cleaned dataset
├── figures/               # Generated visualizations
│   ├── downloads_by_category.png
│   ├── likes_by_category.png
│   ├── trendingScores_by_category.png
│   └── Year_pie.png
└── README.md              # Documentation
```

---

## 📊 Data Source

* **Platform:** Hugging Face
* **API Endpoint:** `https://huggingface.co/api/models`
* **Access:** Public (no authentication required)
* **Format:** JSON

---

## 🛠️ Tools and Environment

* **Language:** Python 3.10+
* **Environment:** Jupyter Notebook

### Install and Import the following Libraries to be used

```python
import requests
import json
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## 🔄 Project Workflow with Code Snippets

Follow each step below respectively to obtain similar results.

---

### Step 1: Fetch Data from Hugging Face API

This block retrieves AI model metadata using an HTTP GET request.

```python
url = "https://huggingface.co/api/models"
response = requests.get(url)
data = response.json()
print(data)
```

The raw response is stored for inspection and reuse.

---

### Step 2: Save Raw Data

The retrieved JSON data is saved locally to preserve the original dataset.

```python
with open("models.json", "w") as f:
    json.dump(data, f)
```

---

### Step 3: Load Data into a Pandas DataFrame

The JSON data is converted into tabular form for analysis.

```python
df = pd.DataFrame(data)
df.head()
```

---

### Step 4: Select Relevant Columns

Only useful fields are retained for analysis.

```python
df = df[["modelId", "pipeline_tag", "createdAt", "downloads", "likes", "trendingScore"]]
```

---

### Step 5: Feature Engineering (Year Extraction & Category Naming)

The model creation timestamp is converted into a release year, and categories are standardized.

```python
df["year"] = pd.to_datetime(df["createdAt"]).dt.year
df = df.rename(columns={"pipeline_tag": "category"})
```

---

### Step 6: Data Cleaning

This block removes incomplete and duplicate records and validates numeric fields.

```python
df = df.dropna(subset=["category", "year"])
df = df.drop_duplicates()

df[["downloads", "likes", "trendingScore"]] = df[["downloads", "likes", "trendingScore"]].clip(lower=0)
```

---

### Step 7: Save Cleaned Dataset

The cleaned dataset is exported for reuse.

```python
df.to_csv("cleaned_model_data.csv", index=False)
```

---

### Step 8: Exploratory Data Analysis

Basic statistics and category counts are computed here.

```python
df.describe()
df["category"].value_counts()
```

Correlation analysis between popularity metrics:

```python
df[["likes", "downloads", "trendingScore"]].corr()
```

---

### Step 9: Data Visualization

#### Bar Chart – Downloads by Category

```python
# Step 1: Count how many times each category appears
category_counts = df["category"].value_counts()

# Step 2: Filter categories with count >= 1
valid_categories = category_counts[category_counts >= 1].index

# Step 3: Filter the DataFrame
filtered_df = df[df["category"].isin(valid_categories)]

# Step 4: Aggregate Likes (sum or mean)
likes_by_category = filtered_df.groupby("category")["downloads"].sum()

# Step 5: Plot bar chart
plt.figure(figsize=(15,5))
likes_by_category.plot(kind="bar", color="skyblue")

plt.xlabel("Category")
plt.ylabel("Total downloads")
plt.title("trendingScores by Category (only categories with ≥ 1 occurrences)")

# Save chart
plt.savefig("downloads_by_category_filtered.png", dpi=300, bbox_inches="tight")

plt.show()
```

#### Bar Chart – Likes by Category

```python
# Step 1: Count how many times each category appears
category_counts = df["category"].value_counts()

# Step 2: Filter categories with count >= 1
valid_categories = category_counts[category_counts >= 1].index

# Step 3: Filter the DataFrame
filtered_df = df[df["category"].isin(valid_categories)]

# Step 4: Aggregate Likes (sum or mean)
likes_by_category = filtered_df.groupby("category")["likes"].sum()

# Step 5: Plot bar chart
plt.figure(figsize=(15,5))
likes_by_category.plot(kind="bar", color="skyblue")

plt.xlabel("Category")
plt.ylabel("Total Likes")
plt.title("Likes by Category (only categories with ≥ 1 occurrences)")

# Save chart
plt.savefig("likes_by_category_filtered.png", dpi=300, bbox_inches="tight")

plt.show()
```

#### Bar Chart – Trending Score by Category

```python
# Step 1: Count how many times each category appears
category_counts = df["category"].value_counts()

# Step 2: Filter categories with count >= 10
valid_categories = category_counts[category_counts >= 1].index

# Step 3: Filter the DataFrame
filtered_df = df[df["category"].isin(valid_categories)]

# Step 4: Aggregate Likes (sum or mean)
likes_by_category = filtered_df.groupby("category")["trendingScore"].sum()

# Step 5: Plot bar chart
plt.figure(figsize=(15,5))
likes_by_category.plot(kind="bar", color="skyblue")

plt.xlabel("Category")
plt.ylabel("Total trendingScores")
plt.title("trendingScores by Category (only categories with ≥ 1 occurrences)")

# Save chart
plt.savefig("trendingScores_by_category_filtered.png", dpi=300, bbox_inches="tight")

plt.show()
```

#### Pie Chart – Category Distribution

```python
# Count occurrences of each category
category_counts = df["category"].head(20).value_counts()

# Plot pie chart
plt.figure(figsize=(6,6))
plt.pie(
    category_counts,
    labels=category_counts.index,   # category names
    autopct="%1.1f%%",              # show percentages
    startangle=90,                  # rotate start
    colors=["skyblue", "lightgreen", "orange", "pink"]  
)

plt.title("Category Distribution")
plt.savefig("category_pie.png", dpi=300, bbox_inches="tight")  # save chart
plt.show()
```
### Pie Chart – Distribution by Year

```python
# Count occurrences of each category
category_counts = df["Year"].value_counts()

# Plot pie chart
plt.figure(figsize=(6,6))
plt.pie(
    category_counts,
    labels=category_counts.index,   # category names
    autopct="%1.1f%%",              # show percentages
    startangle=90,                  # rotate start
    colors=["skyblue", "lightgreen", "orange", "pink"] 
)

plt.title("Distribution by Year")
plt.savefig("Year_pie.png", dpi=300, bbox_inches="tight")  # save chart
plt.show()
```

---

## 📈 Key Findings

* Text-based models dominate model releases and popularity metrics.
* High engagement metrics reflect rapid growth in LLM research.
* Recent years show a sharp increase in AI model releases.

---

## ♻️ Reproducibility & Ethics

* Public, deterministic data source
* No personal or sensitive information used
* Fully reproducible by running the notebook top-to-bottom

---

## 👥 Maintainers

**Research Methods Group 6**
Mzuzu University – ICT Department 
