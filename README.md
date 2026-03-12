# Retail-Inventory-Intelligence-Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection

## Problem Statement

This dashboard helps retail businesses understand the relationship between product demand and inventory availability.

The objective of this analysis is to identify situations where product demand exceeds available inventory, which can lead to supply shortages and potential business losses.

Using this dashboard, businesses can monitor daily demand patterns, evaluate product availability, and understand the financial impact caused by supply shortages.

By analyzing demand and availability trends, organizations can improve inventory planning and reduce potential revenue losses.


### Steps followed 

- Step 1 : Data Collection

   The initial dataset was obtained in CSV format, containing product inventory and demand information.

   The dataset included fields such as:

   Order Date

   Product ID

   Product Name

   Unit Price

   Availability

   Demand
- Step 2 :Data Import into SQL Server

  The CSV dataset was imported into Microsoft SQL Server (SSMS) where the database was created and tables were structured.
  Basic data inspection was performed to check:
  Null values
  Incorrect product IDs
  Data inconsistencies
- Step 3 : Data Cleaning using SQL

  Some incorrect values were detected in the Product ID column.
  These were corrected using SQL update statements.

  Example:

  UPDATE prod.prod+env+inventory+dataset

  SET Product_ID = 7

  WHERE Product_ID = 21;

  Another correction:

  UPDATE prod.prod+env+inventory+dataset
   
  SET Product_ID = 11
  WHERE Product_ID = 22;
- Step 4 : Table Joins

  Two separate tables were available in the dataset:
  Product inventory dataset
  Product information dataset
  These tables were combined using SQL JOIN operations.
  A new table was created using SQL query to store the cleaned and combined dataset.

  Example:

  CREATE TABLE new_table AS
  SELECT
  a.Order_Date,
  a.Product_ID,
  a.Availability,
  a.Demand,
  b.Product_Name,
  b.Unit_Price
  FROM prod.inventory_dataset AS a
  LEFT JOIN prod.products_dataset AS b
  ON a.Product_ID = b.Product_ID;
- Step 5 :  Importing Data into Power BI

  The cleaned dataset was imported into Power BI Desktop using Microsoft SQL Server connector.
  This allowed the report to directly fetch data from the SQL database.
- Step 6 :Data Source Migration

  During the project, a requirement was introduced to change the data source from:

  Microsoft SQL Server → MySQL Database
  To achieve this:

  MySQL Connector was installed
  Dataset was imported into MySQL Workbench
  SQL cleaning operations were repeated
  Tables were joined again in MySQL
- Step 7 : Connecting MySQL with Power BI

  The MySQL database was connected to Power BI using the MySQL database connector.
  Using Power BI Advanced Editor, the data source was updated from SQL Server to MySQL database without rebuilding the entire report.
- Step 8 :Creating DAX Measures

  Several DAX measures were created to calculate key business metrics.

  Examples include:

  Total Demand

  Total Availability

  Total Loss

  Total Profit

  Average Demand per Day

  Average Availability per Day

  Average Loss Per Day

  Total Supply Shortage

  These measures were used to display business KPIs in the dashboard.
- Step 9 : New measure was created to find Average Demand Per Day.

  Following DAX expression was written for the same,

          Average Demand per day = DIVIDE([Total Demand],[Total Number of Days])

  A card visual was used to represent Average Demand Per Day

  ![Image](https://github.com/user-attachments/assets/f9e8145e-1fff-42a7-a1be-c0874f377f40)

- step 10 : New measure was created to find Average Availability Per Day 

  Following DAX expression was written or the same,

            Average Availability per Day = DIVIDE([Total Availability],[Total Number of Days]) 


  A card visual was used to represent Average Availability Per Day

   ![Image](https://github.com/user-attachments/assets/61bf8946-f83c-44cc-93a7-f7ac08c69186)


- step 11 : New measure was created to find Total Supply Shortage

  Following DAX expression was written for the same,

            Total Supply Storage = [Total Demand]-[Total Availability] 

  A card visual was used to represent Total Supply Shortage
          
  [Image](https://github.com/user-attachments/assets/1245288c-a227-42c1-a02f-e7524576d0b5)

- step 12 : New measure was created to find Total Profit

  Following DAX expression was written for the same,

            Total Profit = SUMX(FILTER('Demand/Availability Data','Demand/Availability Data'[LOSS/PROFIT]>0),'Demand/Availability Data'[LOSS/PROFIT]*'Demand/Availability Data'[unit_price])

  A card visual was used to represent Total Profit

  ![Image](https://github.com/user-attachments/assets/2a0f70b5-3d34-42b1-a9ea-329c0c20d982)

- step 13 : New measure was created to find Total Loss

  Following DAX expression was written for the same,

            Total Loss = SUMX(FILTER('Demand/Availability Data','Demand/Availability Data'[LOSS/PROFIT]<0),'Demand/Availability Data'[LOSS/PROFIT]*'Demand/Availability Data'[unit_price]) * -1 

  A card visual was used to represent Total Loss

  ![Image](https://github.com/user-attachments/assets/6e2d9799-41bf-48ee-924e-38b70866da29)


- step 14 : New measure was created to find Average Loss Per Day

  Following DAX expression was written for the same,

            Average Loss per day = DIVIDE([Total Loss],[Total Number of Days])

  A card visual was used to represent Average Loss Per Day

 ![Image](https://github.com/user-attachments/assets/1b2269ef-4995-48df-975f-173692a45a76)

     
- step 15 : The report was then published to Power BI Service.

![Image](https://github.com/user-attachments/assets/a28ff5a6-a148-42bb-886b-f079b1b8e4b6)


# Snapshot of Dashboard (Power BI Service)

<img width="1908" height="915" alt="Image" src="https://github.com/user-attachments/assets/40311a2d-0230-44c6-8cf5-27a87bfcdd19" />





<img width="1912" height="915" alt="Image" src="https://github.com/user-attachments/assets/6b5f0c78-bc52-4455-8f64-496f1f361afe" />

 
 # Report Snapshot (Power BI DESKTOP)

 
<img width="1380" height="758" alt="Image" src="https://github.com/user-attachments/assets/cedd5e9d-6b29-4557-8f59-bbe371b44453" />


<img width="1385" height="766" alt="Image" src="https://github.com/user-attachments/assets/3d384737-be13-42e4-b4df-89f2c18944ca" />

# Insights

The two pages report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Average Demand vs Availability
In many cases, the average product demand is higher than the available inventory, indicating supply shortages.


           
### [2] Supply Shortage Impact
 
The dashboard identifies situations where product availability cannot meet demand, resulting in lost sales opportunities.


 ### [3] A Financial Impact

  Supply shortages contribute to financial losses for the business when demand cannot be fulfilled.

 ### [4] Inventory Monitoring
 
Using this dashboard, businesses can track daily inventory levels and demand patterns to optimize supply chain planning.
Tools & Technologies Used
Power BI
SQL Server (SSMS)
MySQL Workbench
DAX
CSV Dataset

