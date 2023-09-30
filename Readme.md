### Scenario
A solid waste management company collects and recycles solid waste across major cities in the country of Brazil. The company operates hundreds of trucks of different types to collect and transport solid waste. The company would like to create a data warehouse so that it can create reports like

* total waste collected per year per city
* total waste collected per month per city
* total waste collected per quarter per city
* total waste collected per year per trucktype
* total waste collected per trucktype per city
* total waste collected per trucktype per station per city

Design and implement a data warehouse for the company.

#### Objectives
In this assignment:

* Design a Data Warehouse
* Load data into Data Warehouse
* Write aggregation queries
* Create MQTs
* Create a Dashboard

#### Exercise 1 - Design a Data Warehouse
The solid waste management company has provied the sample data they wish to collect.

|Trip no:|Waste Type|Waste Collected|Collection Zone|City          |Date     |
|--------|----------|---------------|---------------|--------------|---------|
| 1      |Dry       |45.23          |South          |Sao Paulo     |23-Jan-20|
| 2      |Wet       |43.12          |Central        |Rio de Janeiro|24-Jan-20|
| 3      |Electronic|40.19          |West           |Sao Paulo     |23-Jan-20|

Design a Star Schema warehouse by identifying the columns for the various dimension and fact tables in the schema.

#### Task 1 - Design the dimension table MyDimDate
Write down the fields in the MyDimDate table in any text editor one field per line. 

#### Task 2 - Design the dimension table MyDimWaste
Write down the fields in the MyDimWaste table in any text editor one field per line.

#### Task 3 - Design the dimension table MyDimZone
Write down the fields in the MyDimZone table in any text editor one field per line.

#### Task 4 - Design the fact table MyFactTrips
Write down the fields in the MyFactTrips table in any text editor one field per line.

### Exercise 2 - Create schema for Data Warehouse on PostgreSQL

#### Task 5 - Create the dimension table MyDimDate

#### Task 6 - Create the dimension table MyDimWaste

#### Task 7 - Create the dimension table MyDimZone

#### Task 8 - Create the fact table MyFactTrips

### Exercise 3 - Load data into the Data Warehouse
Load the data into the tables.

After the initial schema design, due to opertional issues, data could not be collected in the format initially planned.

This implies that the previous tables (MyDimDate, MyDimWaste, MyDimZone, MyFactTrips) and their associated attributes are no longer applicable to the current design. The company has loaded data using CSV files per the new design

#### Task 9 - Load data into the dimension table DimDate
Load DimDate.csv data into DimDate table.
Query first 5 rows in the table DimDate.

#### Task 10 - Load data into the dimension table DimTruck
Load DimTruck.csv data into DimTruck table.
Query first 5 rows in the table DimTruck.

#### Task 11 - Load data into the dimension table DimStation
Load DimStation.csv data into DimStation table.
Query first 5 rows in the table DimStation.

#### Task 12 - Load data into the fact table FactTrips
Load FactTrips.csv data into FactTrips table.
Query first 5 rows in the table FactTrips.

### Exercise 4 - Write aggregation queries and create MQTs

#### Task 13 - Create a grouping sets query
Create a grouping sets query using the columns stationid, trucktype, total waste collected.

#### Task 14 - Create a rollup query
Create a rollup query using the columns year, city, stationid, and total waste collected

#### Task 15 - Create a cube query
Create a cube query using the columns year, city, stationid, and average waste collected.

#### Task 16 - Create an MQT
Create an MQT named max_waste_stats using the columns city, stationid, trucktype, and max waste collected.

### Exercise 5 - Create a dashboard using Cognos Analytics

Use the DataForCognos_date.csv file to generate the following charts.

#### Task 17 - Create a pie chart in the dashboard
Create a pie chart that shows the waste collected by truck type.

#### Task 18 - Create a bar chart in the dashboard
Create a bar chart that shows the waste collected station wise.

#### Task 19 - Create a line chart in the dashboard
Create a line chart that shows the waste collected by month wise.

#### Task 20 - Create a pie chart in the dashboard
Create a pie chart that shows the waste collected by city.

