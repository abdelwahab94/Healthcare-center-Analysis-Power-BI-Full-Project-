# Power BI Project Documentation: Healthcare Center Analysis

## Project Overview
This Power BI project provides a comprehensive analysis of a healthcare center's operations, focusing on key metrics such as total billing, insurance coverage, medication costs, and room charges. The report includes visualizations of billing by room type, state, city, and department, as well as insights into average costs and percentages of total billing by procedure and service type.

---

## Data Sources
The data used in this project is derived from multiple tables, including:

1. **Patients**: Contains patient demographics such as age, gender, and city.
2. **Visits**: Includes details about patient visits, such as admission date, discharge date, and insurance coverage.
3. **Insurance**: Provides information about insurance providers and coverage.
4. **Procedures**: Lists medical procedures and their associated costs.
5. **Departments**: Contains details about hospital departments (e.g., Cardiology, Pediatrics).
6. **Time**: Includes time-based data for trend analysis.

---

## Data Cleaning and Preparation
Before creating the data model and visualizations, the data underwent the following cleaning and preparation steps:

### 1. **Data Loading**
- Data was loaded from multiple sources, including Excel files and databases, into Power BI.
- Tables were imported using Power Query for transformation.

### 2. **Handling Missing Values**
- Missing values in columns like `Insurance Coverage` and `Diagnosis ID` were addressed:
  - For numerical columns, missing values were replaced with `0`.
  - For categorical columns, missing values were replaced with `Unknown`.

### 3. **Removing Duplicates**
- Duplicate rows in the `Visits` and `Patients` tables were identified and removed using the `Remove Duplicates` feature in Power Query.

### 4. **Data Type Conversion**
- Columns like `Admitted Date` and `Discharge Date` were converted to the `Date` data type.
- Numerical columns like `Billing Amount` and `Insurance Coverage` were converted to the `Decimal` data type.

### 5. **Creating Calculated Columns**
- A new column, `Total Billing`, was created in the `Visits` table to calculate the Total Amount of Billing:
  ```DAX
  Total Billing = Visits[Treatment Cost]+Visits[Medication Cost]+Visits[Room Charges(daily rate)]
  ```


### 6. **Data Normalization**
- Redundant columns, such as repeated city names, were removed, and a City ID column was used to link the Patients table to a Cities table.
- The Departments table was normalized to avoid redundancy in department names.

### 7. **Handling Outliers**
- Outliers in numerical columns like Billing Amount and Medication Cost were identified using box plots and addressed by capping values at the 99th percentile.

### 8. **Creating Relationships**
Relationships between tables were established in Power BI:
- `patients[City ID] <— cities[City ID]`
- `visits[Department ID] <— departments[Department ID]`
- `visits[Diagnosis ID] <— diagnoses[Diagnosis ID]`
- `visits[Insurance ID] <— insurance[Insurance ID]`
- `visits[Patient ID] <— patients[Patient ID]`
- `visits[Procedure ID] <— procedures[Procedure ID]`

---

## Data Model
The data model consists of the following tables and relationships:

### Tables
#### Patients:
- Columns: Patient ID, Patient Name, Age, Gender, City ID, Race

#### Visits:
- Columns: Visit ID, Patient ID, Admitted Date, Discharge Date, Diagnosis ID, Insurance Coverage, Emergency Visit

#### Insurance:
- Columns: Insurance ID, Insurance Provider

#### Procedures:
- Columns: Procedure ID, Procedure

#### Departments:
- Columns: Department ID, Department

#### Time:
- Columns: Date, Quarter

### Relationships
- `patients[City ID] <— cities[City ID]`
- `visits[Department ID] <— departments[Department ID]`
- `visits[Diagnosis ID] <— diagnoses[Diagnosis ID]`
- `visits[Insurance ID] <— insurance[Insurance ID]`
- `visits[Patient ID] <— patients[Patient ID]`
- `visits[Procedure ID] <— procedures[Procedure ID]`

---

## Key Visuals
The report includes the following key visuals:

### 1. Total Billing Overview
#### Metrics:
- Total Medication Cost: $546K
- Total Billing: $3.2M
- Total Insurance Coverage: $2.23M
- Total Rooms Charge: $73.2K
- Total Treatment Cost: $2.6M

### 2. Total Billing by Room Type
#### Room Types:
- General Ward: $1.95M
- Private Room: $1.25M
- Semi-Private Room: $0.55M

### 3. Total Billing by State and City
#### States/Cities:
- Birmingham: $0.77M
- Bristol: $0.35M
- Edinburgh: $0.15M
- Glasgow: $0.18M
- Leeds: $0.17M
- Liverpool: $0.16M
- London: $1.6M
- Manchester: $0.15M
- Newcastle: $0.14M
- Sheffield: $0.39M

### 4. Average Costs
#### Metrics:
- Average Billing Amount: $649.92
- Average Insurance Coverage: $456.04
- Average Medication Cost: $109.21
- Average Rooms Charge: $14.63
- Average Treatment Cost: $526.08

### 5. Percentage of Total Billing by Procedure and Department
#### Procedures:
- Cardiology: 25.91%
- General Medicine: 23.64%
- Narcology: 23.59%
- Orthopedics: 14.09%
- Pediatrics: 12.77%

#### Departments:
- Cardiology: 23.64%
- General Medicine: 23.59%
- Narcology: 14.09%
- Orthopedics: 12.77%
- Pediatrics: 23.39%

### 6. Total Billing by Month
- A line chart showing monthly billing trends.

---

## Filters and Slicers
The report includes the following filters and slicers for user interaction:

### Filters on All Pages:
- Payment Status: All

### Filters on This Page:
- Gender: All
- Race: All
- Quarter: All

---

## DAX Formulas
Key DAX formulas used in the project include:

### Total Medication Cost:
```DAX
Total Medication Cost = SUM(Visits[Medication Cost])
```

### Total Treatment Cost:
```DAX
Total Treatment Cost = SUM(Visits[Treatment Cost])
```

### Total Rooms Charge:
```DAX
Total Rooms Charge = SUM(visits[Room Charges(daily rate)])
```

### Total Insurance Coverage:
```DAX
Total Insurance Coverage = SUM(visits[Insurance Coverage])
```

### Total Billing:
```DAX
Total Billing = SUM(Visits[Billing Amount])
```

### Average Medication Cost:
```DAX
Average Medication Cost = AVERAGE(Visits[Medication Cost])
```

### Average Treatment Cost:
```DAX
Average Treatment Cost = AVERAGE(Visits[Treatment Cost])
```

### Average Rooms Charge:
```DAX
Average Rooms Charge = AVERAGE(visits[Room Charges(daily rate)])
```

### Average Insurance Coverage:
```DAX
Average Insurance Coverage = AVERAGE(visits[Insurance Coverage])
```

### Average Billing Amount:
```DAX
Average Billing Amount = AVERAGE(Visits[Billing Amount])
```
---

## User Interaction
Users can interact with the report in the following ways:

- **Drill-Downs**: Users can drill down into specific metrics, such as billing by city or department.
- **Filters**: Users can filter data by gender, race, quarter, and payment status.
- **Tooltips**: Hovering over visuals displays additional details, such as exact values and percentages.

---

## Deployment
The report is deployed on Power BI Service and can be accessed by authorized users via the Power BI web portal. Users can also interact with the report on mobile devices.

---

## Conclusion
This Power BI project provides valuable insights into the healthcare center's operations, enabling stakeholders to make data-driven decisions. The report highlights key metrics, trends, and cost breakdowns, offering a comprehensive view of the center's financial and operational performance.

