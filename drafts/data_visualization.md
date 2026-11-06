# Data Visualization

"In this course, we mainly learned how to use Python for end-to-end data analysis. Basically, it covers two parts: first, using **Pandas** to clean, filter, and aggregate raw datasets; and second, using **Matplotlib** to build subplots and visualize the data patterns." 

#### Part A: Data Processing with Pandas (数据处理)

> "For data processing, we worked with two main structures: 1D **Series** and 2D **DataFrames**.
In our labs, our workflow usually has three steps:
> 
> 1. **Data Selection**: We use `.loc` for label-based indexing and `.iloc` for integer-position indexing. We also filter rows with boolean conditions, like checking if a column value is greater than a threshold.
> 2. **Data Cleaning**: Raw data is always messy. We first check missing values with `df.isna().sum()`. Then we fix them using `dropna()` or `fillna()`, remove duplicates with `drop_duplicates()`, and convert string formats to numbers using `pd.to_numeric`.
> 3. **Aggregation**: We use `groupby()` to group data by category and calculate statistics like `mean()`, `sum()`, or `count()`."

#### Part B: Data Visualizing with Matplotlib (数据可视化)

> "For visualization, Matplotlib uses an object-oriented architecture:
The **Figure** is the whole window or canvas, and the **Axes** are the individual subplots where we draw data.
Depending on the data type, we choose different charts:
> 
> - `ax.plot()` for time-series trends,
> - `ax.bar()` for category comparison,
> - `ax.scatter()` to see correlations between two variables,
> - and `ax.hist()` to check the data distribution."

### Experiment

"Let me take our course project as an example. We were given a large CSV file with raw commercial data.   
**Step 1: Ingestion & Inspection**
I loaded the file with `pd.read_csv()`. When I ran `df.info()` and `df.isna().sum()`, I noticed many missing prices and duplicated rows.   
**Step 2: Cleaning**
• I dropped duplicate records with `df.drop_duplicates()`.   
• For missing values, I filled numerical blanks using `df.fillna()`.   
• Some numeric columns were wrongly imported as strings, so I used `pd.to_numeric(..., errors='coerce')` to safely parse them into floats.   
**Step 3: Aggregation & Visualization**
• I grouped the records by product category using `df.groupby('category')` and calculated their average sales with `.mean()`.   
• Finally, I created a subplot layout with `plt.subplots()`. On the first axis, I drew an `ax.bar()` chart to compare sales across categories. On the second axis, I drew an `ax.hist()` chart to inspect the distribution of transaction amounts. I also added titles, labels, and grids to make it clean and readable."   3