# Hospital Quality & Readmissions Dashboard

## Overview

An interactive Power BI dashboard analyzing hospital readmission rates and patient satisfaction across 5,400+ U.S. hospitals using CMS (Centers for Medicare & Medicaid Services) public data. This project demonstrates the relationship between clinical outcomes and patient experience metrics.

## Business Problem

Hospital readmissions cost Medicare approximately $26 billion annually. Healthcare administrators need to identify which facilities, conditions, and patient populations drive preventable readmissions to enable targeted quality improvement initiatives.

## Data Sources

All data sourced from [CMS Provider Data Catalog](https://data.cms.gov/):

- **Hospital General Information** - Facility details, ownership type, location
- **Hospital Readmissions Reduction Program** - 30-day readmission ratios by condition
- **HCAHPS Patient Satisfaction Survey** - Patient experience scores (~198M survey responses)

## Key Features

- **Executive Summary Page**: KPI cards, readmission rates by condition, geographic map, hospital detail table with conditional formatting
- **Patient Satisfaction Analysis Page**: Scatter plot with trend line showing correlation between readmissions and satisfaction, breakdown by hospital ownership type
- **Interactive Filtering**: State-level slicer for regional analysis
- **DAX Measures**: Custom calculations for benchmarking and performance metrics

## Key Insights

1. **Florida hospitals underperform**: 1.02 avg readmission ratio vs 1.00 national benchmark (2% higher)
2. **Negative correlation identified**: Hospitals with higher readmission rates tend to have lower patient satisfaction scores
3. **Ownership matters**: For-profit (Proprietary) hospitals show lowest patient satisfaction; Department of Defense and Physician-owned facilities rank highest
4. **44% of hospitals exceed benchmark**: 2,375 of 5,421 hospitals have readmission ratios above 1.0
5. **Hip/Knee replacement** has the highest average readmission ratio among the six tracked conditions

## Dashboard Preview

### Executive Summary
![Executive Summary](screenshots/executive_summary.png)

### Patient Satisfaction Analysis
![Patient Satisfaction](screenshots/patient_satisfaction.png)

## Technical Details

**Tools Used:**
- Microsoft Power BI Desktop
- Power Query (data cleaning & transformation)
- DAX (Data Analysis Expressions)

**Data Model:**
- Star schema with Hospitals as central dimension table
- Fact tables: Readmissions, Patient_Satisfaction
- Relationships via Facility ID (one-to-many)

**DAX Measures Created:**
```dax
Avg Readmission Ratio = AVERAGE(Readmissions[Excess Readmission Ratio])

Hospitals Above Benchmark = CALCULATE(DISTINCTCOUNT(Readmissions[Facility ID]), Readmissions[Excess Readmission Ratio] > 1)

Avg Patient Rating = AVERAGE(Patient_Satisfaction[Patient Survey Star Rating])

Total Hospitals = COUNTROWS(Hospitals)

Total Survey Responses = SUM(Patient_Satisfaction[Number of Completed Surveys])
```

## How to Use

1. Download the `.pbix` file
2. Open with Power BI Desktop (free from Microsoft)
3. Use the State slicer to filter by region
4. Click on any visual to cross-filter the dashboard
5. Hover over data points for detailed tooltips

## Future Enhancements

- Add time-series analysis with historical data
- Include cost impact calculations
- Build predictive model for readmission risk
- Add drill-through pages for individual hospital analysis

## Author

**David Chirino**  
Data Analyst | Tampa, FL  
