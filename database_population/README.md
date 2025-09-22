# 🎓 NYC SAT Results – Data Cleaning & Integration  

## 🧹 Cleaning Process
Starting from the raw **`sat-results.csv`**, we applied the following transformations in Python (`pandas`):

- **Column names standardized** → lowercased, spaces replaced with underscores.  
- **Selected relevant fields** → `dbn`, `school_name`, SAT scores, number of test takers, % tested, academic tier rating.  
- **Renamed SAT score fields** →  
  - `sat_critical_reading_avg_score`  
  - `sat_math_avg_score`  
  - `sat_writing_avg_score`  
- **Numeric cleaning** → stripped `"s"`, `"S"`, `"N/A"`, `%`, and other non-numeric tokens; converted to numeric with `NaN` where needed.  
- **Range validation** →  
  - SAT scores restricted to `[200–800]`  
  - Academic tier rating restricted to `[1–4]`  
  - `% tested` converted from `"85%"` → `0.85`  
- **Deduplication** → removed duplicate rows by `dbn`.  
- **Row pruning** → dropped rows missing all three SAT scores.  
- **Final typing** →  
  - SAT scores & academic tier rating → `REAL` (float)  
  - Number of test takers → `INT`  
  - `% tested` → `REAL` (decimal)  

---

## ⚠️ Key Challenges
- **Messy strings** (`"s"`, `"S"`, `"N/A"`, `%`) required normalization.  
- **Duplicate column names** in the raw CSV (`sat critical reading` appeared twice, one with a typo).  
- **Schema alignment** with DOE datasets → standardized on long descriptive names (`sat_critical_reading_avg_score`) for consistency.  
- **Integration** → SAT table added to the shared `nyc_schools` schema for cross-dataset joins.  

---

## 🗄️ SQL Schema & Integration
The cleaned SAT results were integrated into the **`nyc_schools`** schema, alongside:

- `high_school_directory`  
- `school_demographics`  
- `school_safety_report`  

### Final Table Definition
```sql
CREATE TABLE IF NOT EXISTS nyc_schools.cleaned_sat_results (
  dbn                              VARCHAR(15) PRIMARY KEY,
  school_name                      TEXT NOT NULL,
  num_of_sat_test_takers           INT,
  sat_critical_reading_avg_score   REAL,
  sat_math_avg_score               REAL,
  sat_writing_avg_score            REAL,
  pct_students_tested              REAL,
  academic_tier_rating             REAL
);

