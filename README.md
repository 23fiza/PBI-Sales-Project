# 📊 Power BI Sales Overview Dashboard by Region (Dynamic KPIs)

This project is a **Sales Overview Dashboard** created in Power BI that tracks and analyzes **Sales**, **Profit**, and **Quantity** across four regions (Central, East, South, and West). The report is fully dynamic with year-based filters, metric toggles, and YoY comparisons.

---

## 🔍 Project Objective

To design an interactive dashboard to monitor regional performance across key business KPIs:
- 💰 Sales
- 📈 Profit
- 📦 Quantity

---

## 📌 Business Requirements

- Display Sales, Profit, and Quantity for **each region** (Central, East, South, West).
- Dynamic metric selection using a slicer.
- Year-based filtering with comparison against **Previous Year (PY)**.
- Monthly **bar sparkline** with trendline to track monthly performance.
- Comparative analysis by **state**, including **bubble maps** and **bar charts**.
- Tabular view with YoY performance metrics.

---

## 🧩 Steps Followed

1. Requirement Gathering
2. Data Walkthrough
3. Data Connection
4. Data Cleaning / Quality Check
5. Data Modeling
6. Data Processing
7. DAX Calculations
8. Dashboard Layouting
9. Chart Development
10. Report Development
11. Insights Generation

---

## 📁 Dataset Columns

- Order ID, Order Date, Ship Date, Customer ID, Segment, Region
- State/Province, City, Product Category & Sub-Category
- Sales, Quantity, Discount, Profit

---

## 📌 DAX Measures

### ✅ Total KPIs
```DAX
Total Sales = SUM('Sales Data'[Sales])
Total Profit = SUM('Sales Data'[Profit])
Total Quantity = SUM('Sales Data'[Quantity])
📅 Current Year Measures

CY Sales =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
RETURN CALCULATE([Total Sales], CalendarTable[Year] = SelectedYear)

CY Profit =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
RETURN CALCULATE([Total Profit], CalendarTable[Year] = SelectedYear)

CY Quantity =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
RETURN CALCULATE([Total Quantity], CalendarTable[Year] = SelectedYear)
🕒 Previous Year Measures

PY Sales =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
RETURN CALCULATE([Total Sales], CalendarTable[Year] = SelectedYear - 1)

PY Profit =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
RETURN CALCULATE([Total Profit], CalendarTable[Year] = SelectedYear - 1)

PY Quantity =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
RETURN CALCULATE([Total Quantity], CalendarTable[Year] = SelectedYear - 1)
📉 PY Sales Display (Formatted Text)

PY KPI Sales =
VAR SelectedYear = SELECTEDVALUE(CalendarTable[Year])
VAR PreviousYearSales = CALCULATE([Total Sales], CalendarTable[Year] = SelectedYear - 1)
VAR FormatPYSales = FORMAT(PreviousYearSales / 1000, "0.00")
RETURN
    IF(ISBLANK(PreviousYearSales), "PY Sales: No Data", 
    "PY Sales: " & FormatPYSales & "K")
📊 Year-over-Year (YoY) KPIs

YoY Sales =
VAR CurrentY = [CY Sales]
VAR PreviousY = [PY Sales]
VAR YoY = DIVIDE(CurrentY - PreviousY, PreviousY)
RETURN IF(YoY > 0, UNICHAR(9650) & " " & FORMAT(YoY, "0%"), UNICHAR(9660) & " " & FORMAT(YoY, "0%"))

YoY Profit =
VAR CurrentY = [CY Profit]
VAR PreviousY = [PY Profit]
VAR YoY = DIVIDE(CurrentY - PreviousY, PreviousY)
RETURN IF(YoY > 0, UNICHAR(9650) & " " & FORMAT(YoY, "0%"), UNICHAR(9660) & " " & FORMAT(YoY, "0%"))

YoY Quantity =
VAR CurrentY = [CY Quantity]
VAR PreviousY = [PY Quantity]
VAR YoY = DIVIDE(CurrentY - PreviousY, PreviousY)
RETURN IF(YoY > 0, UNICHAR(9650) & " " & FORMAT(YoY, "0%"), UNICHAR(9660) & " " & FORMAT(YoY, "0%"))
📌 Dynamic Titles

Dynamic Title = MAX('Select Metric'[Select Metric])
Visual Title = MAX('Select Metric'[Select Metric]) & " By Region"
📈 Visuals Used
KPI Cards for CY & PY metrics

Bar Sparklines for monthly trends

Toggle Buttons for Metric Selection (Sales, Profit, Quantity)

Bubble Map for Sales by State

Bar Chart for State-wise Breakdown

Table for CY vs PY & YoY % Comparison

📊 Insights Summary
California is the top-performing state across all years.

North Carolina consistently ranks lowest in sales.

Regional YoY trends highlight consistent growth in West and East regions.

Sharp QoQ gains in November and December across multiple regions.

📎 How to Use
Open the .pbix file in Power BI Desktop.

Use the Year slicer to switch analysis between years.

Use the metric toggle to switch between Sales, Profit, and Quantity.

Hover on bar sparklines or use tooltips for monthly breakdowns.
