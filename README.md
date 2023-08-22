  --IN SQL-PROJECT
  --IN MY SQL PROJECT
 --	Write some T-SQL statements to create at least three tables for a small database that will track customers, purchases, and retail store locations for a business.  Creating foreign key constraints are not necessary as the relationships between the tables should be obvious from your table definitions.  You will use these tables to answer the rest of the questions on this test. 
 customers | CREATE TABLE `customers` (
  `custID` int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `custName` varchar(50) DEFAULT NULL 
) ;   
CREATE TABLE `purchases` (
  `purchasesID` int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `storeFK` int(11) DEFAULT NULL,
  `custID` int(11) DEFAULT NULL,
  `purchase_date` date DEFAULT NULL
)  ;   

CREATE TABLE `retail_store_locations` (
  `storeID` int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `items` varchar(50) DEFAULT NULL,
  `cost` float DEFAULT NULL,
  `store_city` varchar(50) DEFAULT NULL
)  ;   
 --write a query that will show the total dollar amounts of sales for each city and how many customers made purchases in each city during the month of November 2012.

SELECT 
	store.store_city as City,
    count(pa.custID) as 'Number of Customers', 
    SUM(cost) as 'Total Amounts of Sales'

FROM retail_store_locations store
	INNER JOIN purchases pa ON pa.storeFK = store.storeID 

WHERE pa.purchase_date BETWEEN '2012-11-01' AND '2012-11-30' 
GROUP BY City
ORDER BY City ASC;  
 --Write another query to show the total overall sales for the top 10 cities with the most customers for all of the year 2012.  (Your final result should contain just one number in a single row.)

SELECT 
    COUNT(cu. custID) as 'No of Customers', 
    SUM(store.cost) as 'Total Amounts of Sales', 
    store.store_city as City

 

FROM retail_store_locations store 
INNER JOIN purchases pa ON pa.storeFK = store.storeID
INNER JOIN customers cu ON cu.custID = pa.custID

 

WHERE pa.purchase_date BETWEEN '2012-01-01' AND '2012-12-31'
GROUP BY (City)

LIMIT 10; 
--Write a few statements to add yourself as a new customer into your database that also checks to make sure nobody else with the same name already exists: 
INSERT INTO customers (custName)

SELECT 'Shahid' - Replace 'Shahid' with desired customer name
WHERE NOT EXISTS (
    SELECT 1 * FROM customers WHERE custName = 'Shahid’ - Replace Shahid'
); 
--Write a query to delete all of the customers from your database who have never spent more than $10.00 at your stores.  Is this question ambiguous?  If so, why?

DELETE cus, pur
FROM customers AS cus
INNER JOIN purchases AS pur ON cuscus = pur.custID
WHERE pur.storeFK IN (
    SELECT storeID 
    FROM retail_store_locations
    GROUP BY storeID 
    HAVING SUM(cost) < 10
) ;   

The question is not ambiguous 


 
