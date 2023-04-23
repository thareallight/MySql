# MySql

**Table creation input include:**
CREATE TABLE "int_breweries"
(SALES_ID integer,
SALES_REP text,
EMAILS text,		
BRANDS text,
PLANT_COST real,
UNIT_PRICE real,
QUANTITY real,
COST real,
PROFIT real,
COUNTRIES text,
REGION text,
MONTHS text,
YEARS integer,
primary key (SALES_ID))


SELECT *
FROM int_breweries
LIMIT 5

--**Q1 Write an SQL query to fetch “SALES_REP” from breweries  table using the alias name as WORKER_NAME.**


SELECT sales_rep AS "workers_name"
FROM int_breweries;

--**Q2 Write an SQL query to fetch “BRANDS” from breweries table in upper case.**

SELECT DISTINCT UPPER (brands) AS uppercasebrands
FROM int_breweries;

--**Q3 Write an SQL query to print all details from the breweries table;
--sort the QUANTITY column in Ascending order and the COSTS column in Descending order**

SELECT *
FROM int_breweries
ORDER BY quantity ASC;

SELECT *
FROM int_breweries
ORDER BY cost DESC;

--**Q4 Write an SQL query to print the profit made from two BRANDS,
“trophy” and “eagle” in the first quarter of 2019**

SELECT brands, months, SUM(profit) AS Total_profit
FROM
	(SELECT brands, profit, years, months
	FROM int_breweries
	WHERE months IN ('January', 'February', 'March') AND years = 2019) Shuttle
WHERE brands = 'trophy' OR brands = 'eagle lager'
GROUP BY brands, months
ORDER BY Total_profit ASC;

--**Q5 Write a query that reduces the cost of the trophy brand by 2%..**

SELECT brands, cost * 0.02 AS "2% cost reduction"
FROM int_breweries
WHERE brands = 'trophy'; 

--**Q6 Which sales rep made the highest profit in Ghana in the year 2017?**

SELECT sales_rep, countries, years, SUM (profit) AS "total profit"
FROM int_breweries
WHERE countries = 'Ghana' AND years = 2017
GROUP BY sales_rep, countries, years;

--**Q7 What region recorded
the lowest quantity of goods in the last quarter of every year?**


SELECT region, years, MIN (quantity) AS "least quantity"
	FROM int_breweries
		WHERE months = 'October' OR months = 'November' OR months = 'December'
			GROUP BY region, years
				ORDER BY years;
    
	

--**Q8 The Breweries company has a yearly tradition of promoting the sales_rep
who makes the highest profit in the year. Who deserves this promotion in 2019?**

SELECT sales_rep, SUM (profit) AS "total profit"
FROM int_breweries
WHERE years = 2019
GROUP BY sales_rep
ORDER BY "total profit" DESC
LIMIT 1;

--**Q9 Regions with quantities of trophy which are less than 60000, 
need to be restocked. What regions do we restock with the trophy brand?**

SELECT region, brands, SUM (quantity) AS "total quantity"
FROM int_breweries
WHERE quantity < 6000 AND brands = 'trophy'
GROUP BY region, brands;







