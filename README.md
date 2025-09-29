<p align="center">
  <img src="https://i.imgur.com/Nm7UOaW.png" alt="Blinkit Sales Analysis" width="80%" />
</p>

<h1 align="center">📊 Blinkit Sales Data Analysis in Python</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?logo=python" alt="Python Version" />
  <img src="https://img.shields.io/badge/Platform-Google%20Colab-yellow?logo=google-colab" alt="Platform" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen" alt="Project Status" />
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License" />
</p>

---

# 📊 Blinkit Sales Data Analysis in Python

This project presents a comprehensive sales analysis of **Blinkit**, an Indian quick commerce platform, using **Python** and powerful data analysis libraries such as **Pandas**, **NumPy**, **Matplotlib**, and **Seaborn**.

It explores trends in sales based on item characteristics, outlet details, and customer ratings, helping uncover insights that could support data-driven decision-making.

---

## 📁 Dataset Information

- File Used: `blinkit_data.csv`
- Number of Records: `8523`
- Number of Columns: `12`

### 🔑 Columns Overview:
- `Item Fat Content`
- `Item Identifier`
- `Item Type`
- `Outlet Establishment Year`
- `Outlet Identifier`
- `Outlet Location Type`
- `Outlet Size`
- `Outlet Type`
- `Item Visibility`
- `Item Weight`
- `Sales`
- `Rating`

---

## 🧹 Data Cleaning

### 🔄 Standardizing "Item Fat Content"

Some inconsistent values found in the `Item Fat Content` column were:
```python
['Regular', 'Low Fat', 'low fat', 'LF', 'reg']
```

We replaced them for consistency:

```python
df['Item Fat Content'] = df['Item Fat Content'].replace({
    "low fat": "Low Fat",
    "LF": "Low Fat",
    "reg": "Regular"
})
```

✅ After replacement:  
```python
['Regular', 'Low Fat']
```

---

## 📌 Business KPIs

We calculated several key performance indicators:

```python
Total_Sales = df['Sales'].sum()
Avg_Sales = df['Sales'].mean()
No_item_sold = df['Sales'].count()
Avg_ratings = df['Rating'].mean()
```

### 📈 Results:
- **Total Sales**: `$1,201,681.5`
- **Average Sales per Item**: `$141.0`
- **Total Items Sold**: `8,523`
- **Average Customer Rating**: `4.0`

---

## 📊 Visual Analysis

### 🥧 1. Sales by Fat Content (Pie Chart)

```python
Sales_by_fat = df.groupby('Item Fat Content')['Sales'].sum()
plt.pie(Sales_by_fat, labels=Sales_by_fat.index, autopct='%1.1f%%', explode=(0.1, 0), shadow=True)
plt.title("Sales by Fat Content")
plt.axis("equal")
plt.show()
```

---

### 📦 2. Total Sales by Item Type (Bar Chart)

```python
Sales_by_item = df.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)
plt.figure(figsize=(10, 5))
ax = sns.barplot(x=Sales_by_item.index, y=Sales_by_item.values)
plt.xticks(rotation=90)
plt.title("Total Sales by Item Type")
plt.xlabel("Item Type")
plt.ylabel("Total Sales")
for bar in ax.patches:
    plt.text(bar.get_x() + bar.get_width() / 2, bar.get_height(), f'{bar.get_height():.1f}', ha='center', va='bottom', fontsize=7)
plt.tight_layout()
plt.show()
```

---

### 🏪 3. Fat Content by Outlet Location (Grouped Bar Chart)

```python
Grouped = df.groupby(["Outlet Location Type", "Item Fat Content"])["Sales"].sum().unstack()
Grouped = Grouped[["Regular", "Low Fat"]]
ax = Grouped.plot(kind="bar", figsize=(10, 5))
plt.title("Fat Content by Outlet for Total Sales")
plt.xlabel("Outlet Location Type")
plt.ylabel("Total Sales")
for bar in ax.patches:
    plt.text(bar.get_x() + bar.get_width()/2, bar.get_height(), f'{bar.get_height():.1f}', ha='center', va='bottom', fontsize=7)
plt.tight_layout()
plt.show()
```

---

### 🏗️ 4. Sales by Outlet Establishment Year (Line Chart)

```python
sales_by_year = df.groupby("Outlet Establishment Year")["Sales"].sum().sort_index()
plt.figure(figsize=(10, 5))
plt.plot(sales_by_year.index, sales_by_year.values, marker="o", linestyle="-", color="b")
plt.title("Total Sales by Outlet Establishment Year")
plt.xlabel("Outlet Establishment Year")
plt.ylabel("Total Sales")
for x, y in zip(sales_by_year.index, sales_by_year.values):
    plt.text(x, y, f"${y:,.0f}", ha="center", va="bottom", fontsize=8)
plt.tight_layout()
plt.show()
```

---

### 🧱 5. Sales by Outlet Size (Pie Chart)

```python
sales_by_size = df.groupby("Outlet Size")["Sales"].sum().sort_values(ascending=False)
plt.figure(figsize=(4, 4))
plt.pie(sales_by_size, labels=sales_by_size.index, autopct='%1.1f%%', shadow=True, startangle=90)
plt.title("Sales by Outlet Size")
plt.axis("equal")
plt.tight_layout()
plt.show()
```

---

### 🌍 6. Sales by Outlet Location Type (Horizontal Bar Chart)

```python
Sales_by_location = df.groupby("Outlet Location Type")["Sales"].sum().sort_values(ascending=False).reset_index()
plt.figure(figsize=(8, 3))
ax = sns.barplot(x="Sales", y="Outlet Location Type", data=Sales_by_location)
plt.title("Sales by Outlet Location")
plt.xlabel("Total Sales")
plt.ylabel("Outlet Location Type")
plt.tight_layout()
plt.show()
```

---

## ✅ Conclusion

This analysis provided several important insights:

- **Low Fat items** contributed significantly to overall sales.
- **Certain item types** drive much higher sales than others.
- **Outlet size and location** play a key role in performance.
- Outlets established in earlier years still contribute significantly to total sales.

---

## 🔧 How to Run This Project

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/blinkit-sales-analysis.git
cd blinkit-sales-analysis
```

### 2. Install Required Libraries
```bash
pip install pandas numpy matplotlib seaborn
```

### 3. Run the Notebook
You can open the notebook using Jupyter Notebook or Google Colab.

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🙏 Acknowledgements

- Thanks to [Google Colab](https://colab.research.google.com/) for a free and easy-to-use notebook environment.
- This analysis was conducted using publicly available or hypothetical Blinkit sales data.
