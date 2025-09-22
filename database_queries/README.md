# 🧠 NYC School Data Exploration 

## 🏫 School Distribution
- **Brooklyn**: 121 schools  
- **Bronx**: 118 schools  
- **Manhattan**: 106 schools  
- **Queens**: 80 schools  
- **Staten Island**: 10 schools  

➡️ Schools are fairly evenly distributed across the larger boroughs, with Staten Island having the fewest.

---

## 🎓 English Language Learners (ELL)
- Only **Manhattan** has valid ELL data: **~7.57% average**  
- All other boroughs show **NaN (no data)**  

⚠️ This indicates the `school_demographics` table in the training database contains records only for **Manhattan schools**.

---

## 🔗 Special Education (SPED)
- Current query output shows **repeated values for the same school** (East Side Community School in Manhattan).  
- This happens because `school_demographics` has **multiple rows per school** (likely for different years).  


---

## ✅ Key Insights
1. **School counts** by borough are complete from `high_school_directory`.  
2. **ELL data** is incomplete (only Manhattan is covered).  
3. **SPED analysis** requires collapsing duplicates per school before ranking.  
