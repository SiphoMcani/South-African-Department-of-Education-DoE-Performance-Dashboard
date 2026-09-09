-- Aggregate Totals
Total Enrolment = SUM('DoE_Dataset1'[Number of Enrollment])
Total Learners Who Wrote = SUM('DoE_Dataset1'[Number Wrote])
Total Passes = SUM('DoE_Dataset1'[Number Passed])
Total Failures = SUM('DoE_Dataset1'[Number Failed])
Total Bachelors = SUM('DoE_Dataset1'[Number Passed with Bachelors])

-- Key Performance Ratios
Pass Rate % = DIVIDE([Total Passes], [Total Learners Who Wrote], BLANK())
Bachelor Pass Rate % = DIVIDE([Total Bachelors], [Total Learners Who Wrote], BLANK())
Exam Participation % = DIVIDE([Total Learners Who Wrote], [Total Enrolment], BLANK())

-- Dynamic Spatial & Ranking Logic
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
