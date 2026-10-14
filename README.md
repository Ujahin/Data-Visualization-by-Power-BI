# Data-Visualization-by-Power-BI
Created dashboards using the sales data and the HR data.


## For Sales Analytics Dashboard
## Key DAX Formulas

### 1. Total Buying Value
Calculates the total cost of purchased products based on quantity sold.

```DAX
Total Buying Value =
'Sales Data'[Sold Quantity] *
'Sales Data'[Unit Buying Price]
```

### 2. Total Selling Value
Calculates sales revenue after applying the discount.

```DAX
Total Selling Value =
'Sales Data'[Sold Quantity] *
'Sales Data'[Unit Selling Price] *
(1 - 'Sales Data'[Discount])
```

**Note:** This formula assumes `Discount` is stored as a decimal (e.g., 10% = 0.10). If the discount is stored as a whole percentage (e.g., 10), use `1 - 'Sales Data'[Discount] / 100` instead.

### 3. Profit
Calculates profit by subtracting the total buying value from the total selling value.

```DAX
Profit =
SUM('Sales Data'[Total Selling Value]) -
SUM('Sales Data'[Total Buying Value])
```

**Mathematical formula:**

Profit = Total Selling Value − Total Buying Value

### 4. Profit Percentage
Calculates profit relative to the total buying value.

```DAX
Profit Percentage =
DIVIDE(
    [Profit],
    SUM('Sales Data'[Total Buying Value]),
    0
)
```

**Mathematical formula:**

Profit Percentage (%) = (Profit / Total Buying Value) × 100

Format this measure as a percentage in Power BI.

### 5. Total Sales
```DAX
Total Sales =
SUM('Sales Data'[Total Selling Value])
```

### 6. Total Quantity Sold
```DAX
Total Quantity =
SUM('Sales Data'[Sold Quantity])
```

## Dashboard Analysis

The dashboard uses these calculations to analyze:

- **Sales and Profit by Month:** Compares monthly sales revenue and profit.
- **Daily Sales:** Tracks sales trends across days.
- **Sales by Product:** Identifies products generating the highest sales.
- **Sales by Category:** Compares revenue across product categories.
- **Sales by Type:** Analyzes sales distribution by sales type.
- **Sales by Payment Mode:** Examines revenue across payment methods.
- **KPI Cards:** Summarizes total sales, quantity, profit, and profit percentage.
- **Interactive Slicers:** Filters the dashboard by year, month, sales type, and payment mode.

**Note:** Replace `'Sales Data'` and the column names with the actual names used in your Power BI model. The buying value and selling value formulas should be created as calculated columns, while Profit and Profit Percentage should be measures. The transcript does not provide the exact field names or full DAX code shown on screen, so these formulas represent the calculations described in the tutorial.



## For HR Analytics Dashboard
## Key DAX Formulas

### 1. Total Employees
```DAX
Total Employees =
DISTINCTCOUNT('HR Data'[Employee ID])
```

### 2. Active Employees
```DAX
Active Employees =
CALCULATE(
    [Total Employees],
    'HR Data'[Attrition] = "No"
)
```

### 3. Attrition Count
```DAX
Attrition Count =
CALCULATE(
    [Total Employees],
    'HR Data'[Attrition] = "Yes"
)
```

### 4. Attrition Rate
```DAX
Attrition Rate =
DIVIDE(
    [Attrition Count],
    [Total Employees],
    0
)
```

*Format this measure as a percentage with one decimal place.*

**Mathematical formula:**

Attrition Rate (%) = (Attrition Count / Total Employees) × 100

### 5. Average Age
```DAX
Average Age =
AVERAGE('HR Data'[Age])
```

### 6. Average Experience
```DAX
Average Experience =
AVERAGE('HR Data'[YearsAtCompany])
```

## Data Visualization and Analysis

The dashboard uses these calculations to analyze:
- Employee attrition by department, salary slab, gender, job role, and job satisfaction.
- Workforce distribution by age group and department.
- Attrition trends across employee experience levels.
- Key performance indicators (KPIs), including total employees, active employees, attrition count, attrition rate, average age, and average experience.

**Note:** Replace `'HR Data'` with the actual table name in your Power BI model. These measures assume that each employee ID uniquely identifies an employee; `DISTINCTCOUNT` prevents duplicate IDs from inflating employee counts.
