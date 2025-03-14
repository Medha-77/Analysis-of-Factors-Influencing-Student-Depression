# 📊 **Student Depression Data Analysis**  

## 📌 **Overview**  
This project analyzes **student depression data** to identify potential factors affecting student well-being. By leveraging **SQL Server** for **data preparation** and **Tableau** for **interactive visualization**, we aim to uncover **correlations** between **student depression** and various **academic, financial, and lifestyle factors**.  

### 🎯 **Key Objectives**  
✅ **Data Preparation:** Clean, transform, and organize student depression data for analysis.  
✅ **Correlation Identification:** Analyze relationships between depression and factors such as **academic pressure, financial stress, study satisfaction, sleep duration, and study hours**.  
✅ **Interactive Visualization:** Develop an engaging **Tableau dashboard** to effectively communicate key insights.  
✅ **Insight Generation:** Identify **patterns and trends** that can help **educators, administrators, and mental health professionals** improve student support systems.  

## 🛠 **Technologies and Tools**  
- **SQL Server:** Used for **data management, cleaning, and transformation**.  
- **Tableau Desktop:** Used for **data visualization, analysis, and dashboard creation**.  
- **Tableau Cloud:** Used for **publishing and sharing the interactive dashboard**.  

---

## 🗄 **Data Preparation (SQL Server)**  
The following steps were executed in **SQL Server** to clean and prepare the dataset for analysis:  

### 📌 **Database Creation**  
A new database **`Tableau_Project_1`** was created:  
```sql
CREATE DATABASE [Tableau_Project_1]
```

### 📌 **Data Import**  
Student depression data was imported into a table named **`Depression_Student_Dataset`**:  
```sql
USE [Tableau_Project_1]
SELECT * FROM [dbo].[Depression_Student_Dataset]
```

### 🛠 **Data Cleaning and Transformation**  
✔ **Standardizing Gender Column** to maintain consistency:  
```sql
UPDATE [dbo].[Depression_Student_Dataset] SET Gender = 'F' WHERE Gender = 'Female'
UPDATE [dbo].[Depression_Student_Dataset] SET Gender = 'M' WHERE Gender = 'male'
```

✔ **Creating Age Group Categories** for better analysis:  
```sql
ALTER TABLE [dbo].[Depression_Student_Dataset] ADD Age_Group VARCHAR(MAX)
UPDATE [dbo].[Depression_Student_Dataset] SET Age_Group = 
  CASE 
    WHEN Age BETWEEN 18 AND 24 THEN 'A1'
    WHEN Age BETWEEN 25 AND 30 THEN 'A2'
    ELSE 'A3' 
  END
```

✔ **Analyzing Column Distribution** to detect anomalies:  
```sql
SELECT Academic_Pressure, COUNT(*) 
FROM [dbo].[Depression_Student_Dataset] 
GROUP BY Academic_Pressure
```

✔ **Adding a Unique Identifier Column (`Index_Column`)**:  
```sql
ALTER TABLE [dbo].[Depression_Student_Dataset] ADD Index_Column INT IDENTITY(1,1)
```

✔ **Updating the Depression Column to Categorical Values (`Yes/No`)**:  
```sql
UPDATE [Depression_Student_Dataset] SET Depression = 'No' WHERE Depression = 0
UPDATE [Depression_Student_Dataset] SET Depression = 'Yes' WHERE Depression = 1
```

---

## 📊 **Data Visualization and Analysis (Tableau)**  
The prepared dataset from **SQL Server** was imported into **Tableau Desktop** to create meaningful visualizations and analyze the relationships between key variables affecting student depression.  

### **🔍 Key Visualizations & Insights**  

📌 **Depression Rate by Academic Pressure**  

A **bar chart** displaying the percentage of students experiencing **depression** at different **academic pressure levels**. 

![Depression Rate by Academic Pressure](https://github.com/user-attachments/assets/7d07dd2a-d55d-4a0c-a480-1f23510bf236)  

📌 **Correlation Between Financial Stress and Depression**  

A **[chart type]** visualizing how **financial stress 💰** influences **depression levels**.  

![Financial Stress vs. Depression](https://github.com/user-attachments/assets/2e346085-25e8-4fe9-9339-3cfc45deae33)  

📌 **Study Satisfaction vs. Depression**  

A **box plot 📦** comparing **depression rates** among students with different **study satisfaction levels 📚**.  

![Study Satisfaction vs. Depression](https://github.com/user-attachments/assets/623cda18-9fcd-4cde-a830-070109d82781)  

📌 **Impact of Sleep Duration on Depression**  

A **line graph 📈** illustrating how **sleep duration 😴** affects **depression scores**.  

![Sleep Duration vs. Depression](https://github.com/user-attachments/assets/440c8c72-6da8-41cd-897c-5e0c2ccffaa0)  

📌 **Relationship Between Study Hours and Depression**  

A **bar chart 📊** depicting how different **study hour ⏳ ranges** correlate with **student depression levels**.  

![Study Hours vs. Depression](https://github.com/user-attachments/assets/35a56293-bd33-4d82-821c-1786526b969b)  

---

## 🚀 **Interactive Dashboard Features**  
An **interactive Tableau dashboard** was developed to provide a **comprehensive** and **dynamic** view of the data, enabling users to explore different variables influencing student depression.  

🔹 **Filters:** Allows users to filter data by **age group, gender, academic pressure, financial stress, and study habits**.  
🔹 **Interactive Charts:** Updates visualizations dynamically based on user selections.  
🔹 **Summary Statistics:** Displays **key metrics** such as **overall depression rate, average sleep duration, and academic pressure trends**.  
🔹 **Drill-Down Capabilities:** Enables users to **deep dive** into specific student groups for detailed insights.  

---

## 🎯 **Conclusion**  
This project provides **valuable insights** into the factors affecting **student depression**. By utilizing **SQL Server** for **data cleaning** and **Tableau** for **visualization**, we created an **interactive dashboard** that empowers **educators, administrators, and mental health professionals** to:  

✅ Identify **key risk factors** contributing to **student depression**.  
✅ Develop **targeted intervention strategies** to **enhance student well-being**.  
✅ Make **data-driven decisions** to improve **academic policies and student support programs**.  

---
  
