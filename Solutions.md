### Exercise 1 - Design a Data Warehouse
#### Task 1 - Design the dimension table MyDimDate
(1-MyDimDate.jpg)
Write down the fields in the MyDimDate table in any text editor one field per line. 
        dateid
        date
        year
        month
        monthname
        quarter
        quartername
        weekday
        weekdayname

#### Task 2 - Design the dimension table MyDimWaste
(2-MyDimWaste.jpg)

Write down the fields in the MyDimWaste table in any text editor one field per line.

        wasteid
        wastetype

#### Task 3 - Design the dimension table MyDimZone
(3-MyDimZone.jpg)

Write down the fields in the MyDimZone table in any text editor one field per line.
        zoneid
        collectionzone
        city

#### Task 4 - Design the fact table MyFactTrips
(3-MyDimZone.jpg)

Write down the fields in the MyFactTrips table in any text editor one field per line.

        tripid
        wasteid
        zoneid
        dateid
        wastecollected

### Exercise 2 - Create schema for Data Warehouse on PostgreSQL
#### Task 5 - Create the dimension table MyDimDate
(5-MyDimDate.jpg)

    CREATE TABLE public."MyDimDate"
    (
        dateid integer NOT NULL,
        year integer NOT NULL,
        month integer NOT NULL,
        monthname varchar(10) NOT NULL,
        quarter integer NOT NULL,
        quartername ivarchar(20) NOT NULL,
        PRIMARY KEY (dateid)
    );

#### Task 6 - Create the dimension table MyDimWaste
(6-MyDimWaste.jpg)

    CREATE TABLE public."MyDimWaste"
        (
            wasteid integer NOT NULL,
            wastetype varchar(10) NOT NULL,
            PRIMARY KEY (wasteid)
        );

#### Task 7 - Create the dimension table MyDimZone
(7-MyDimZone.jpg)

     CREATE TABLE public."MyDimZone"
        (
            zoneid integer NOT NULL,
            collectionzone varchar(10) NOT NULL,
            city varchar(20) NOT NULL
            PRIMARY KEY (zoneid)
        );

#### Task 8 - Create the fact table MyFactTrips
(8-MyFactTrips.jpg)

    CREATE TABLE public."MyFactTrips"
    (
        tripid integer NOT NULL,
        wasteid integer NOT NULL,
        zoneid integer NOT NULL,
        dateid integer NOT NULL,
        wastecollected numeric NOT NULL,
        PRIMARY KEY (tripid)
        CONSTRAINT FK_wasteid FOREIGN KEY(wasteid)
            REFERENCES public."MyDimWaste"(wasteid),
        CONSTRAINT FK_zoneid FOREIGN KEY(zoneid)
            REFERENCES public."MyDimZone"(zoneid),
        CONSTRAINT FK_dateid FOREIGN KEY(dateid)
            REFERENCES public."MyDimDate"(dateid),
    );

### Exercise 3 - Load data into the Data Warehouse
#### Task 9 - Load data into the dimension table DimDate
(9-DimDate.jpg)

        select * from public."DimDate" limit 5; 

#### Task 10 - Load data into the dimension table DimTruck
(10-DimTruck.jpg)

        select * from public."DimTruck" limit 5; 

#### Task 11 - Load data into the dimension table DimStation
(11-DimStation.jpg)

        select * from public."DimStation" limit 5;

#### Load data into the fact table FactTrips
(12-FactTrips.jpg)

        select * from public."FactTrips" limit 5;

### Exercise 4 - Write aggregation queries and create MQTs

#### Task 13 - Create a grouping sets query
(13-groupingsets.jpg)

    select ft.stationid,dt.trucktype,sum(ft.wastecollected) as totalwastecollected
    from "FactTrips" as ft
    left join "DimStation" as ds
    on ft.stationid = ds.stationid
    left join "DimTruck" as dt
    on ft.truckid=dt.truckid
    group by grouping sets(ft.stationid,dt.trucktype,ft.wastecollected);

#### Task 14 - Create a rollup query
(14-rollup.jpg)

    select dd.year,ds.city,ft.stationid,sum(ft.wastecollected) as totalwastecollected
    from "FactTrips" as ft
    left join "DimStation" as ds
    on ft.stationid = ds.stationid
    left join "DimDate" as dd
    on ft.dateid=dd.dateid
    group by rollup(dd.year,ds.city,ft.stationid,ft.wastecollected);

#### Task 15 - Create a cube query
(15-cube.jpg)

    select dd.year,ds.city,ft.stationid,avg(ft.wastecollected) as avgwastecollected
    from "FactTrips" as ft
    left join "DimStation" as ds
    on ft.stationid = ds.stationid
    left join "DimDate" as dd
    on ft.dateid=dd.dateid
    group by cube(dd.year,ds.city,ft.stationid,ft.wastecollected);

#### Task 16 - Create an MQT
(16-mqt.jpg)

    CREATE MATERIALIZED VIEW max_waste_stats (city, stationid, trucktype, maxwastecollected) AS
    (select ds.city, ft.stationid, dt.trucktype, max(ft.wastecollected) as maxwastecollected
    from "FactTrips" as ft 
    left join "DimStation" as ds
    on ft.stationid = ds.stationid
    left join "DimTruck" as dt
    on ft.truckid=dt.truckid
    group by ds.city, ft.stationid, dt.trucktype);


### Exercise 5 - Create a dashboard using Cognos Analytics

Use the DataForCognos_date.csv file to generate the following charts.

#### Task 17 - Create a pie chart in the dashboard
(17-pie.jpg)

#### Task 18 - Create a bar chart in the dashboard
(18-bar.jpg)

#### Task 19 - Create a line chart in the dashboard
(19-line.jpg)

#### Task 20 - Create a pie chart in the dashboard
(20-pie.jpg)
