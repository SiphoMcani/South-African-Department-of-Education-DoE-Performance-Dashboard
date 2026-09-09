# South African Department of Education (DoE) Performance Dashboard

An analytical Power BI project analyzing regional secondary school examination performance across South African provinces and districts. The data pipeline extracts raw performance data, applies cleanup transformations via Power Query (M), models the tabular schema, and calculates key educational metrics using DAX.

---

## 🖥️ Dashboard Layout & Report Specification

### Visual Layout Diagram
```text
===================================================================================================
|  SOUTH AFRICAN DEPARTMENT OF EDUCATION — NATIONAL PERFORMANCE DASHBOARD                          |
===================================================================================================
| [ Province Slicer: All ]  [ District Slicer: All ]  [ Search District... ]                      |
===================================================================================================
|                                                                                                 |
|  +---------------------+  +---------------------+  +---------------------+  +-----------------+  |
|  | TOTAL ENROLMENT     |  | LEARNERS WROTE      |  | OVERALL PASS RATE   |  | BACHELOR PASS   |  |
|  | [ Total Enrolment ] |  | [Total Wrote]       |  | [Pass Rate %]       |  | [Bachelors %]   |  |
|  +---------------------+  +---------------------+  +---------------------+  +-----------------+  |
|                                                                                                 |
===================================================================================================
|                                                   |                                             |
|  CHART 1: PASS RATE BY PROVINCE                   |  MAP: DISTRICT GEOSPATIAL DISTRIBUTION       |
|  (Bar Chart: [Pass Rate %] sorted DESC)          |  (Bubble Map using [Map Location])           |
|                                                   |                                             |
|  Gauteng         ███████████████████              |           .---.                             |
|  Western Cape    ██████████████████               |          /     \  (Gauteng)                 |
|  Free State      █████████████████                |         (  SA   )                           |
|  KwaZulu-Natal   ███████████████                  |          \     /  (KZN)                     |
|  Mpumalanga      ██████████████                   |           `---'                             |
|  Limpopo         ████████████                     |                                             |
|  Eastern Cape    ██████████                       |                                             |
|                                                   |                                             |
===================================================================================================
|                                                   |                                             |
|  CHART 2: GENDER DISTRIBUTION                     |  TABLE: DISTRICT PERFORMANCE MATRIX         |
|  (Donut Chart: [Total Male] vs [Total Female])    |  (Ranked by DAX Measure [District Rank])    |
|                                                   |                                             |
|        Female      Male                           |  Rank | District | Province | Pass Rate %   |
|        (52%)       (48%)                          |  -----+----------+----------+------------   |
|        /----\     /----\                          |    1  | Tshwane  | Gauteng  |  XX.X%       |
|       |      |   |      |                         |    2  | Metro    | W. Cape  |  XX.X%       |
|        \----/     \----/                          |    3  | Zululand | KZN      |  XX.X%       |
|                                                   |                                             |
===================================================================================================
