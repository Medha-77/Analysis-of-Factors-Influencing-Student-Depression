# Student Depression Data Analysis

## Overview

This project analyzes student depression data to identify potential factors influencing student well-being. By combining the power of SQL Server for data preparation and Tableau for interactive visualization, we aim to uncover correlations between student depression and various academic, financial, and lifestyle factors. The goal is to provide actionable insights that can help educators, administrators, and support services better understand and address student mental health challenges.

## Key Objectives

*   **Data Preparation:** Clean, transform, and prepare student depression data for analysis.
*   **Correlation Identification:** Explore relationships between student depression and factors such as academic pressure, financial stress, study satisfaction, sleep duration, and study hours.
*   **Interactive Visualization:** Develop an interactive Tableau dashboard that effectively communicates key findings and insights.
*   **Insight Generation:** Identify patterns and trends in the data that can inform interventions and support strategies.

## Technologies and Tools

*   **SQL Server:** Used for data management, cleaning, and transformation.
*   **Tableau Desktop:** Used for data visualization, analysis, and dashboard creation.
*   **Tableau Cloud:** Used for publishing and sharing the interactive dashboard.

## Data Preparation (SQL Server)

The following steps were performed using SQL Server to prepare the data for analysis:

*   **Database Creation:** A new database named `Tableau Project 1` was created.

    ```sql
    CREATE DATABASE [Tableau Project 1]
    ```

*   **Data Import:** Student depression data was imported into a table named `[Depression Student Dataset]` within the `[Tableau Project 1]` database.

    ```sql
    USE [Tableau Project 1]

    SELECT * FROM [dbo].[Depression Student Dataset]
    ```

*   **Data Cleaning and Transformation:**

    *   **Gender Column Standardization:** The `Gender` column was standardized to ensure consistency.  Values 'Female' were updated to 'F', and 'male' were updated to 'M'. This was done to simplify analysis and reduce the number of unique values.

        ```sql
        SELECT Gender, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Gender

        UPDATE [dbo].[Depression Student Dataset] SET Gender = 'F' WHERE Gender = 'Female'

        UPDATE [dbo].[Depression Student Dataset] SET Gender = 'M' WHERE Gender = 'male'

        SELECT * FROM [dbo].[Depression Student Dataset] WHERE Gender IS NULL --Checking for null values. None Found

        SELECT * FROM [dbo].[Depression Student Dataset] WHERE Gender = '' --Checking for empty strings. None Found
        ```

    *   **Age Group Column Creation:** A new column, `Age_Group`, was created to categorize students into age groups.  This was done to group students into broader categories for potentially more meaningful analysis.  Students aged 18-24 were categorized as 'A1', 25-30 as 'A2', and those older than 30 as 'A3'.

        ```sql
        SELECT age, COUNT(*) [Count] FROM [dbo].[Depression Student Dataset] GROUP BY age ORDER BY age DESC

        ALTER TABLE [dbo].[Depression Student Dataset] ADD Age_Group VARCHAR(MAX)

        UPDATE [dbo].[Depression Student Dataset]
        SET age_group =
            CASE
                WHEN Age BETWEEN 18 AND 24 THEN 'A1'
                WHEN Age BETWEEN 25 AND 30 THEN 'A2'
                ELSE 'A3'
            END

        SELECT age_group, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY age_group
        ```

    *   **Column Distribution Analysis:** The distribution of values within key columns was analyzed to understand the data and identify potential issues. The `INFORMATION_SCHEMA.COLUMNS` was used to get table metadata. Then, count aggregates were created on each potential dimension.

        ```sql
        SELECT * FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME LIKE 'Depression Student Dataset'

        SELECT Academic_Pressure, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Academic_Pressure

        SELECT Study_Satisfaction, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Study_Satisfaction

        SELECT Sleep_Duration, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Sleep_Duration

        SELECT Dietary_Habits, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Dietary_Habits

        SELECT Have_you_ever_had_suicidal_thoughts, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Have_you_ever_had_suicidal_thoughts

        SELECT Study_Hours, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Study_Hours

        SELECT Financial_Stress, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Financial_Stress

        SELECT Family_History_of_Mental_Illness, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Family_History_of_Mental_Illness

        SELECT Depression, COUNT(*) FROM [dbo].[Depression Student Dataset] GROUP BY Depression
        ```

    *   **Index Column Creation:** An `Index_Column` was added to serve as a unique identifier for each record.

        ```sql
        ALTER TABLE [Depression Student Dataset] ADD Index_Column INT IDENTITY(1,1)
        ```

    *   **Depression Column Update:** The `Depression` column, originally numerical (0 and 1), was converted to a VARCHAR and the values were updated to 'No' (for 0) and 'Yes' (for 1).  This was done to improve readability and make the column more suitable for categorical analysis in Tableau.

        ```sql
        UPDATE [Depression Student Dataset] SET Depression = 'No' WHERE Depression = 0

        ALTER TABLE [Depression Student Dataset] ALTER COLUMN DEPRESSION VARCHAR(MAX)

        UPDATE [Depression Student Dataset] SET Depression = 'Yes' WHERE Depression = '1'

        SELECT Depression, COUNT(*) FROM [Depression Student Dataset] GROUP BY Depression
        ```

## Data Visualization and Analysis (Tableau)

The prepared data from SQL Server was imported into Tableau Desktop to create visualizations and analyze the relationships between various factors and student depression. The following key visualizations were developed:

*   **Depression Rate by Academic Pressure:** A bar chart showing the percentage of students reporting depression ('Yes' in the Depression column) for different levels of academic pressure.
![Image](https://github.com/user-attachments/assets/7d07dd2a-d55d-4a0c-a480-1f23510bf236)

*   **Correlation between Financial Stress and Depression:** A visualization [Specify the type of chart] visualizing the relationship between financial stress levels and depression scores.
![Image](https://github.com/user-attachments/assets/2e346085-25e8-4fe9-9339-3cfc45deae33)

*   **Study Satisfaction vs. Depression:** A box plot comparing the distribution of depression scores for students with different levels of study satisfaction.
![Image](https://github.com/user-attachments/assets/623cda18-9fcd-4cde-a830-070109d82781)

*   **Impact of Sleep Duration on Depression:** A line graph showing the average depression score for students with different sleep durations.
![Image](https://github.com/user-attachments/assets/440c8c72-6da8-41cd-897c-5e0c2ccffaa0)

*   **Relationship between Study Hours and Depression:** A bar chart showing the percentage of students reporting depression for different study hour ranges.
![Image](https://github.com/user-attachments/assets/35a56293-bd33-4d82-821c-1786526b969b)


## Interactive Dashboard

An interactive Tableau dashboard was created to provide a comprehensive view of the data and enable users to explore the relationships between different factors and student depression. The dashboard includes:

*   **Filters:** Allow users to filter the data by age group, gender, academic pressure, study satisfaction, and other relevant factors.
*   **Interactive Charts:** Charts dynamically update based on user selections and filters.
*   **Summary Statistics:** Displays key summary statistics, such as the overall depression rate, the distribution of age groups, and the average sleep duration.
*   **Drill-Down Capabilities:** Allows users to drill down into specific segments of the data to gain deeper insights, such as viewing the depression rate for specific combinations of age group and academic pressure.

## Access the Dashboard

The interactive dashboard is published on Tableau Cloud 
![Image](https://github.com/user-attachments/assets/5bb5cdb4-3ffe-49b2-87b4-79e75b82f376)


## Conclusion

This project provides valuable insights into the factors potentially influencing student depression. By leveraging the capabilities of SQL Server and Tableau, we have created an interactive dashboard that empowers users to explore the data and identify areas where interventions and support services can be targeted most effectively. These findings can be used to inform strategies for promoting student mental health and well-being. The detailed data preparation steps and interactive visualizations provide a solid foundation for further research and action.
