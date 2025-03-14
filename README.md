# Manufacturing-Production-Downtime-Analysis-for-a-Soda-Bottling-Line

## **1. Project Title**  
**Production Downtime Analysis for a Soda Bottling Line**  

## **2. Project Overview**  
This project analyzes **downtime and productivity data** for a soda bottling production line to identify inefficiencies and performance gaps. The dataset, sourced from **Maven Analytics**, includes details on **operators, products, start & end times, and downtime reasons for each batch**.  

The objective is to uncover key insights into **operator performance, machine reliability, and production bottlenecks** to improve efficiency. By leveraging **Power BI**, the data has been cleaned, modeled, and visualized to pinpoint major downtime factors, underperforming operators, and areas for process optimization.  

## **3. Problem Statement**  
Downtime in production lines significantly impacts efficiency and profitability. The goal of this analysis is to address the following questions:  

- **What is the current line efficiency?** (Total production time vs. minimum required time)  
- **Which operators are underperforming?** (Comparison of downtime minutes per operator)  
- **What are the leading causes of downtime?** (Machine failures, operator errors, or external factors)  
- **Do specific operators struggle with particular errors?** (Assessing operator-specific downtime causes)  
- **How can downtime be reduced to improve overall productivity?**  

## **4. Data Source**  
The dataset is sourced from Maven Analytics and contains four primary tables:
Downtime Factors Table – Categorizes downtime causes.
- Line Downtime Table – Tracks downtime instances by duration and operator.
- Line Productivity Table – Logs efficiency metrics per batch.
- Products Table – Contains details on manufactured products.


## **5. Methodology**  

### **Data Cleaning & Transformation (Power Query)**  
- Removed duplicates, handled missing values, and standardized downtime categories.  
- Transformed date-time columns to calculate precise **downtime duration**.  

### **Data Modeling**  ![image](https://github.com/user-attachments/assets/f2332bd8-400d-48ea-86bb-5e96a4a387de)

- Established relationships between **production logs, operators, and downtime categories**.  
- Created **calculated columns and measures** in **DAX** to perform deeper analysis.  

### **DAX Formulas Used**  
- **Total Downtime (Minutes)**  
  ```DAX
  Total Downtime = SUM(Downtime[Downtime Minutes])
  ```  
- **Downtime Percentage**  
  ```DAX
  Downtime % = DIVIDE([Total Downtime], SUM(Production[Total Production Time]), 0)
  ```  
- **Line Efficiency**  
  ```DAX
  Line Efficiency = DIVIDE(SUM(Production[Total Production Time]) - [Total Downtime], SUM(Production[Total Production Time]), 0)
  ```  
- **Top Downtime Causes**  
  ```DAX
  Top Downtime Cause = 
  VAR MaxDowntime = MAXX(VALUES(Downtime[Downtime Category]), [Total Downtime])
  RETURN
  CALCULATE(MAX(Downtime[Downtime Category]), [Total Downtime] = MaxDowntime)
  ```  
- **Operator Downtime Ranking**  
  ```DAX
  Operator Rank = RANKX(ALL(Operators), [Total Downtime], , DESC, DENSE)
  ```  
- **Operators with High Errors**  
  ```DAX
  High Error Operators = 
  FILTER(Operators, [Total Errors] > AVERAGE(Operators[Total Errors]))
  ```  

### **Analysis & Visualizations (Power BI)**  ![image](https://github.com/user-attachments/assets/9e1e3b83-7ae7-4771-b3d0-7fcc51190455)

- **Current Line Efficiency** – KPI tracking total production time vs. minimum required time.  
- **Downtime Breakdown by Cause** – Pie chart showing primary reasons for downtime.  
- **Machine Downtime Analysis** – Bar chart ranking machines by total downtime minutes.  
- **Operator Performance Dashboard** – Table highlighting each operator’s total downtime, errors, and efficiency.  
- **Operator Error Breakdown** – Heatmap analyzing which operators struggle with specific errors.  

## **6. Key Insights**  
- **Machine Adjustments** are the leading cause of downtime.  
- **Charlie and Dee** have the highest downtime minutes, requiring performance evaluation.  
- **Operator errors** significantly impact efficiency, with specific operators struggling more than others.  
- **Inventory shortages** frequently disrupt production, causing unnecessary delays.  
- **Charlie contributes the most downtime** and should be monitored closely.  
- **Dee and Charlie have the highest error counts**, suggesting a need for targeted training.  

## **7. Conclusion & Recommendations**  
- **Implement preventive maintenance** to reduce machine failures.  
- **Improve operator training programs** to minimize human errors.  
- **Optimize inventory management** to prevent stock shortages and production delays.  
- **Use real-time monitoring** to enable proactive downtime reduction strategies.  
- **Focus on machine adjustments**, as they are the leading downtime factor; consider automation.  
- **Monitor and evaluate Charlie and Dee** for potential performance improvements.  
- **Refine training programs** to address operator-specific struggles.  
- **Adjust maintenance schedules** to optimize machine uptime.  

