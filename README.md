
# South Africa Matric Pass Analysis | Limpopo, Mpumalanga & North West (2022-2024)

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge)
![Data Analysis](https://img.shields.io/badge/Data%20Analysis-2E8B57?style=for-the-badge)

## 📌 Project Overview
This project analyzes the Matric performance for 3 provinces: **Limpopo, Mpumalanga, and North West** from 2022 to 2024. 
The goal was to understand pass rates, learner volumes, and Bachelor pass contribution to university entry.

I built an interactive Power BI dashboard to answer 8 business questions.

## 🎯 Key Questions Answered

**Q1: Overall Pass Rate per Province**
- Limpopo leads with a higher average pass rate than Mpumalanga and North West.

**Q2: Learners Who Passed (Total Volume)**
- Limpopo passed the highest total number of learners.

**Q3: Total Learners Who Wrote**
- Limpopo wrote the most, followed by Mpumalanga and North West.

**Q4: Trend Over Time (2022-2024)**
- Analyzed yearly trend - pass rates improved from 2022 to 2024 across all provinces.

**Q5: Top Performing Districts by Pass Rate**
- Districts like Mopani West (77.99%) and Capricorn North (74.46%) are top performers.

**Q6: Average Learners Passed per District (Matrix Visual)**
- **Mpumalanga: 1,278.28** average per district - Highest
- Limpopo: 1,235.49
- North West: 1,223.76
- Lowest district: Dr Ruth Segomotsi Mompati (894.09)

**Q7: Ranking All Districts by Pass Rate (RANKX)**
- **Top 5 are ALL from Limpopo:**
    1. Mopani West - 77.99%
    2. Capricorn North - 74.46%
    3. Mopani East - 74.22%
    4. Vhembe East - 73.67%
    5. Sekhukhune South - 72.61%
- Bottom: Bojanala (66.49%) and Ehlanzeni (68.40%)
- Gap between #1 and #15 = 11.5%

**Q8: Bachelor Pass Contribution (Donut Chart)**
- Limpopo contributes **64.19%** of all Bachelor passes
- Mpumalanga + North West = 35.81% combined
- This means Limpopo produces the most university-eligible learners.

## 📊 Dashboard Preview
![Dashboard Screenshot](./dashboard_screenshot.png)
> *Add your Power BI screenshot here. Name it `dashboard_screenshot.png`*

## 🛠️ Tools & Skills Used
- **Power BI Desktop** - Data modeling & visualization
- **DAX** - Measures created:
    - `Pass Rate % = DIVIDE([Passed], [Wrote])`
    - `Average Passed = AVERAGE([Passed])`
    - `Rank = RANKX(ALL(District), [Pass Rate %])`
    - `Bachelor Contribution % = DIVIDE([Bachelor Passes], [Total Bachelor Passes])`
- **Data Cleaning** - Power Query
- **Visuals:** Matrix, Bar Chart, Donut Chart, Line Chart, Table with Conditional Formatting

## 📁 Dataset
- Source: Matric Results Dataset (2022-2024)
- Provinces: Limpopo, Mpumalanga, North West
- Columns: Province, District, Year, Wrote, Passed, Bachelor Pass, Pass Rate

## 💡 Key Insights
1.  **Mpumalanga is most consistent** in average learners passed per district (1,278).
2.  **Limpopo dominates quality** - 8 of top 10 districts by pass rate are in Limpopo.
3.  **Limpopo drives higher education** - 64.19% of all Bachelor passes come from Limpopo alone.
4.  Biggest opportunity is in North West - Bojanala district needs support at 66.49%.

## 🚀 How to Run This Project
1. Clone this repo
2. Open the `.pbix` file in Power BI Desktop
3. Refresh the data if needed
4. Interact with the slicers for Province and Year

## 👤 Author
**Sipho Mcani**


