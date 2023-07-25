#Q.1. Create a table "STATION" to store information about weather observation stations:
create database ASSIGNMENT_MAJORA;
use ASSIGNMENT_MAJORA;

create table STATION
(ID INTEGER PRIMARY KEY,
CITY CHAR(20),
STATE CHAR(2),
LAT_N REAL,
LONG_W REAL);

#Q.2. Insert the following records into the table:
INSERT INTO STATION VALUES (13, 'Phoenix', 'AZ', 33, 112);
INSERT INTO STATION VALUES (44, 'Denver', 'CO', 40, 105);
INSERT INTO STATION VALUES (66, 'Caribou', 'ME', 47, 68);

#Q.3. Execute a query to look at the table STATION in undefined order:
select*from STATION;

#Q.4. Execute a query to select Northern stations (Northern latitude > 39.7):
select*from STATION
WHERE LAT_N > 39.7;

#Q.5. Create another table, 'STATS', to store normalized temperature and preciptation data:
CREATE TABLE STATS
(ID INTEGER REFERENCES STATION(ID),
MONTH INTEGER CHECK (MONTH BETWEEN 1 AND 12),
TEMP_F REAL CHECK (TEMP_F BETWEEN -80 AND 150),
RAIN_I REAL CHECK (RAIN_I BETWEEN 0 AND 100),
PRIMARY KEY (ID, MONTH));

#Q.6. Populate the table STATS with some statistics for january and july:
INSERT INTO STATS VALUES (13, 1, 57.4, 0.31);
INSERT INTO STATS VALUES (13, 7, 91.7, 5.15);
INSERT INTO STATS VALUES (44, 1, 27.3, 0.18);
INSERT INTO STATS VALUES (44, 7, 74.8, 2.11);
INSERT INTO STATS VALUES (66, 1, 6.7, 2.10);
INSERT INTO STATS VALUES (66, 7, 65.8, 4.52);

select*from STATS;

#Q.7. Execute a query to display temperature stats (from stats table) for each city (from station table):
SELECT CITY, TEMP_F FROM STATION
    INNER JOIN STATS
    ON STATS.ID = STATION.ID
    ORDER BY CITY;
    
#Q.8. Execute a query to look at the table STATS, ordered by month and greatest rainfall, with columns rearranged. It should also show the corresponding cities: 
SELECT MONTH, RAIN_I, CITY 
FROM STATS  
JOIN STATION 
ON STATS.ID = STATION.ID 
ORDER BY MONTH, RAIN_I DESC;

#Q.9. Execute a query to look at temperatures for July from table STATS, lowest temperatures first, picking up city name and latitude.
SELECT LAT_N, CITY, TEMP_F FROM STATS, STATION
WHERE MONTH = 7
AND STATS.ID = STATION.ID
ORDER BY TEMP_F;

#Q.10. Execute a query to show MAX and MIN temperatures as well as average rainfall for each city :
SELECT CITY, MAX(TEMP_F), MIN(TEMP_F), AVG(RAIN_I)  FROM STATS
INNER JOIN STATION 
    ON STATS.ID = STATION.ID
    GROUP BY CITY;
    
#Q.11. Execute a query to display each city’s monthly temperature in Celcius and rainfall in Centimeter:
    CREATE VIEW METRIC_STATS ( CITY, MONTH, TEMP_C, RAIN_C) AS 
    SELECT CITY,
    MONTH,
    (TEMP_F -32)* 5/9 ,
    RAIN_I * 0.3937
    FROM STATS
       INNER JOIN STATION 
    ON STATS.ID = STATION.ID;
    
    SELECT*FROM METRIC_STATS;
    
#Q.12. Update all rows of table STATS to compensate for faulty rain gauges known to read 0.01 inches low:
UPDATE STATS SET RAIN_I = RAIN_I + 0.01;
 
SET SQL_SAFE_UPDATES=0;
UPDATE STATS SET RAIN_I = RAIN_I + 0.01;

SELECT * FROM STATS;

#Q.13. Update Denver's July temperature reading as 74.9:
UPDATE STATS SET TEMP_F = 74.9
WHERE ID = 44
AND MONTH = 7;

SELECT * FROM STATS;

    










