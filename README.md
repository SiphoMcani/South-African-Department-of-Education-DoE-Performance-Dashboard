### Visual Container Specifications
1. **KPI Cards Row (Top Navigation):**
   * **Total Enrolment:** `[Total Enrolment]`[cite: 1]
   * **Learners Wrote:** `[Total Learners Who Wrote]`[cite: 1]
   * **Overall Pass Rate:** `[Pass Rate %]`[cite: 1]
   * **Bachelor Qualification Rate:** `[Bachelor Pass Rate %]`[cite: 1]
2. **Main Analytics Panel:**
   * **Pass Rate by Province (Bar Chart):** Category: `DoE_Dataset1[Province]`, Value: `[Pass Rate %]`[cite: 1].
   * **Geospatial Map (Bubble Map):** Location: `DoE_Dataset1[Map Location]`, Size: `[Total Enrolment]`[cite: 1].
3. **Detailed Breakdown Panel:**
   * **Gender Ratio (Donut Visual):** Values: `[Total Male Learners]` vs `[Total Female Learners]`[cite: 1].
   * **District Ranking Matrix (Table Visual):** Columns: `[District Rank]`, `DoE_Dataset1[District]`, `DoE_Dataset1[Province]`, `[Pass Rate %]`, `[Bachelor Pass Rate %]`[cite: 1].

---

## 📊 Key Metrics & DAX Formulas

This repository includes custom DAX measures for analyzing enrollment, pass rates, gender distribution, and bachelor degree qualify rates[cite: 1]:

### 1. Enrollment & High-Level Totals
```dax
Total Enrolment = SUM('DoE_Dataset1'[Number of Enrollment])
Total Learners Who Wrote = SUM('DoE_Dataset1'[Number Wrote])
Total Passes = SUM('DoE_Dataset1'[Number Passed])
Total Failures = SUM('DoE_Dataset1'[Number Failed])
Total Bachelors = SUM('DoE_Dataset1'[Number Passed with Bachelors])
```[cite: 1]

### 2. Pass Rates & Educational Performance
```dax
Pass Rate % = DIVIDE([Total Passes], [Total Learners Who Wrote], BLANK())
Bachelor Pass Rate % = DIVIDE([Total Bachelors], [Total Learners Who Wrote], BLANK())
Exam Participation % = DIVIDE([Total Learners Who Wrote], [Total Enrolment], BLANK())
```[cite: 1]

### 3. Gender Analysis
```dax
Female Percentage = DIVIDE([Total Female Learners], [Total Enrolment])
Male Percentage = DIVIDE([Total Male Learners], [Total Enrolment])
Gender Balance Gap % = ABS([Male Percentage] - [Female Percentage])
```[cite: 1]

### 4. Ranking & Spatial Mapping
```dax
District Rank = 
IF(
    ISINSCOPE('DoE_Dataset1'[District]),
    RANKX(
        ALL('DoE_Dataset1'[Province], 'DoE_Dataset1'[District]),
        [Pass Rate %],
        ,
        DESC,
        DENSE
    )
)

Map Location = 'DoE_Dataset1'[District] & ", " & 'DoE_Dataset1'[Province] & ", South Africa"
```[cite: 1]

---

## 🛠️ Data Transformation (Power Query / M)

The raw dataset undergoes several cleanup steps[cite: 1]:
1. **Filtering & Trimming:** Removes null/empty `District` values and trims whitespace[cite: 1].
2. **Standardization:** Fixes common typographical errors in provincial names (e.g., `Limpoo` / `Lipopo` $\rightarrow$ `Limpopo`, `Mpmalanga` / `Mpumallnga` $\rightarrow$ `Mpumalanga`, `NorthWest` $\rightarrow$ `North West`)[cite: 1].
3. **Type Casting:** Casts enrollment and grade figures into integer types[cite: 1].

```powerquery
let
    Source = Csv.Document(Web.Contents("https://.../DoE_Dataset1.csv"), [Delimiter = ",", Columns = 9, Encoding = 65001, QuoteStyle = QuoteStyle.None]),
    #"Promoted headers" = Table.PromoteHeaders(Source, [PromoteAllScalars = true]),
    #"Filtered rows" = Table.SelectRows(#"Promoted headers", each [District] <> null and [District] <> ""),
    #"Trimmed text" = Table.TransformColumns(#"Filtered rows", {{"District", each Text.Trim(_), type nullable text}}),
    #"Changed column type" = Table.TransformColumnTypes(#"Trimmed text", {
        {"Province", type text}, 
        {"Number of Enrollment", Int64.Type}, 
        {"Number of Male", Int64.Type}, 
        {"Number of Female", type text}, 
        {"Number Wrote", Int64.Type}, 
        {"Number Passed", Int64.Type}, 
        {"Number Failed", Int64.Type}, 
        {" Number Passed with Bachelors ", Int64.Type}
    }, "en-GB"),
    #"Replaced value" = Table.ReplaceValue(#"Changed column type", "Limpoo", "Limpopo", Replacer.ReplaceText, {"Province"}),
    #"Replaced value 1" = Table.ReplaceValue(#"Replaced value", "Lipopo", "Limpopo", Replacer.ReplaceText, {"Province"}),
    #"Replaced value 2" = Table.ReplaceValue(#"Replaced value 1", "Mpmalanga", "Mpumalanga", Replacer.ReplaceText, {"Province"}),
    #"Replaced value 3" = Table.ReplaceValue(#"Replaced value 2", "Mpumallnga", "Mpumalanga", Replacer.ReplaceText, {"Province"}),
    #"Replaced value 4" = Table.ReplaceValue(#"Replaced value 3", "NorthWest", "North West", Replacer.ReplaceText, {"Province"}),
    #"Replaced value 5" = Table.ReplaceValue(#"Replaced value 4", " ", "", Replacer.ReplaceText, {"Number of Female"}),
    #"Changed column type 1" = Table.TransformColumnTypes(#"Replaced value 5", {{"Number of Female", Int64.Type}}),
    #"Renamed columns" = Table.RenameColumns(#"Changed column type 1", {{" Number Passed with Bachelors ", "Number Passed with Bachelors"}})
in
    #"Renamed columns"
```[cite: 1]

---

## 🗂️ Data Model Architecture

* **Table:** `DoE_Dataset1`[cite: 1]
* **Compatibility Level:** 1606 (Power BI / Tabular Storage Engine)[cite: 1]
* **Culture/Locale:** `en-US` / `en-GB`[cite: 1]
* **Key Columns:** `Province`, `District`, `Number of Enrollment`, `Number of Male`, `Number of Female`, `Number Wrote`, `Number Passed`, `Number Failed`, `Number Passed with Bachelors`[cite: 1]

---

## 🚀 Getting Started

1. Clone this repository:
   ```bash
   git clone [https://github.com/your-username/doe-performance-dashboard.git](https://github.com/your-username/doe-performance-dashboard.git)
