## Understanding-Hospital-Performance-Through-Data

### Table of Content
- [Project Overview] (#Project_Overview)
- [Recommendations] (#recommendations)
- [Data Sources] (#data-sources)

### Project Overview
This data analysis project aims to build foundational thinking skills required of healthcare data analysts, uncover trends in hosputal setting. The goal is to analyze the dataset, clesn inconsistent records, perform exploratory data analysis (EDA) and generate insights (recommendations) that can help understand the hospital performance.

## Objectives
- Identify 10 meaningful performance metrics that best explain how this hospital operates
- What the metric measures? In plain, non-technical language,
- Why the metric matters in a hospital setting? Link it to patient care, efficiency, or quality
- How it relates to the patient care continuum?
- Where does this metric sit? (ED, admission, treatment, discharge, outcome)


### Data Information
-**Dataset Name**: Healthcare Performance Dataset

-**Source**: (https://drive.google.com/file/d/1IjWGxOlBPkCQPdfMXhPcur6FeZsLswU4/view?usp=drive_link)

The Dataset contains:
- Patient & Encounter Information: (patient_id, encounter_id, age, gender)
- Visit & Operational Flow: (department, admission_type, admission_datetime, discharge_datetime, ed_arrival_time, provider_seen_time)
- Clinical & Coding Data: (icd10_diagnosis, cpt_procedure, severity_level)
- Financial & Outcome Data: (cost_of_encounter, discharge_disposition, outcome, readmission_flag)

Rows: 5000

Columns: 17

## Tools and Technologies Used
- Excel
- PowerBi

## Data Cleaning/Preparation: The following data cleaning processes were carried out: 

###  Data Loading and Inspection

- **Date/Time Standardization**: Converted all date/time columns to US timestamp format using Power Query.  
- **Admission vs Discharge Validation**: Identified cases where admission occurred before discharge. Used `MAXIFS` to find the latest valid discharge date before the current admission.  
- **Interval Calculation**: Applied an `IF` function — if discharge date is blank, return blank; otherwise, calculate the difference between discharge and admission dates.  

### Department and Outcome Corrections
- **Pediatrics Misclassification**: Flagged patients above 18 years incorrectly classified under Pediatrics. Corrected classification using conditional logic.  
- **Emergency Department Fix**: Reassigned department values misclassified as elective/urgent to “Emergency.”  
- **Discharge Disposition**: Corrected unrealistic discharge dispositions (e.g., “Skilled nursing” for expired patients). If outcome = “Expired,” then discharge disposition = “Expired.”  
- **Readmission Flag**: If readmission flag = 1, labeled as “Readmitted,” else retained existing outcome.  
- **Readmission Rate**: If interval between admissions ≥ 30 days, flagged as 1 (readmission), else 0.  

### Medical Codes
- **ICD-10 & CPT Codes**: Used `XLOOKUP` to map codes to descriptions, making data interpretable for non-medical professionals.  

### Patient Demographics
- **Gender Consistency**: For patients with conflicting gender entries, selected the most frequent value. If no majority, chose the first recorded gender using `INDEX` and `MATCH`.  
- **Age Consistency**: For patients with multiple ages, calculated the mean age per patient for consistency.  

### Handling Missing Values
- **Cost of Encounter**: Imputed missing values with the median cost  

### Converting Data Types
- **Date Columns**: Standardized all date columns to US format using Power Query.  

### Standardizing Column Names
- Ensured all column names followed a consistent naming convention for readability and easier querying
- Standardization of the Cost of Encounter column with the dollar symbol.  

### Duplicate Check
- Duplicates: No duplicate records were found.  

## Exploratory Data Analysis
Several analyses and visualizations were performed to understand the dataset. The following questions were explored. 
- How efficiently patients move through care?
- Where delays may exist
- What outcomes patients experience?
- Which operational signals leadership should monitor?
- How efficiently patients move through care
- What is this hospital doing well operationally?
- Where do you suspect bottlenecks or risks exist?
- Which results would concern leadership?
- What clarifying questions would you ask clinicians or administrators before recommending action?

## Results/Findings
The analysis result is as follows;
#### What is this hospital doing well operationally?
- Efficient Discharge Process: 74.7% of patients fully recovered and returned home
- Prompt Provider Response in ED: Adequate staffing and functional triage improved patient safety
- Well-Managed Elective Care: Low severity and re-admission rates indicate strong planning
- Effective Emergency Workflow: Even with high emergency volume, outcomes remain reasonable.

#### Where do you suspect bottlenecks or risks exist?
- Re-admissions within 30 days: May indicate gaps in discharge education, follow-up, or medications adherence.
- High-Severity Emergency Load: Sudden spikes could strain staff, equipment and bed capacity
- ED Wait Time: Extended waits may reflect staffing shortages, limited imaging and lab resources or inefficient triage
- Cost Variability Across Encounters: Suggests potential overuse of diagnosis or resource inefficiencies.

#### Which results would concern leadership?
- High Re-admission Rates: Might signals possible quality gaps in treatment or discharge planning
- Severe Emergency Cases with Poor Outcomes: Indicates patient safety risk and possible capacity limits
- Long ED Wait Times: Impacts patient satisfaction and safety
- High Cost, High-Frequency Procedures: Drives workload and spending. E.g Procedure 81002
- Procedure and Diagnosis Cost Drives (Procedures 81002): Highest encounter count and cost. Key workload and financial driver while diagnosis N39 (Most common) had high demand for routine management and chronic care planning and A08 being less frequent but highest average cost. Cost-intensive, not volume-driven

#### What clarifying questions would you ask clinicians or administrators before recommending action?
- Are repeat visits by the same patient counted as separate encounters?
- Are clinicians experiencing workload pressure affecting discharge timing?
- Are delays caused by shared resources (labs, imaging)?
- How is discharge planning conducted and what follow-up exists to reduce re-admissions?
- Are staffing or equipment shortages contributing to ED delays or high-severity care strain?

## Recommendations
- Implement post-discharge follow-up for high-risk patients to reduce re-admissions
- Review cost standardization protocols especially for high-cost procedures like 81002
- Consider predictive staffing models for peak ED periods

## Limitations
- Missing values in important columns
- Data Quality Issues
- assumptions made during cleaning

## References
- Luke Barousse Youtube Tutorials




