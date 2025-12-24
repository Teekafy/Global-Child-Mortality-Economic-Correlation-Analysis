### Using a mapping Table. "Country to Continent" to map two columns: Code and Continent. 

```sql
-- This query creates a unified view where every country now has its continent
SELECT 
    m.Entity, 
    m.Code, 
    m.Year, 
    m.CMR, 
    m.GDP, 
    c.region
FROM child_mortality_cleaned AS m
LEFT JOIN continents2 AS c ON m.Code = c.`alpha-3`
WHERE m.Code IS NOT NULL;

-- Add to new table
CREATE TABLE child_mortality_data AS
SELECT 
    m.Entity, 
    m.Code, 
    m.Year, 
    m.CMR, 
    m.GDP,
    m.Population,
    c.region
FROM child_mortality_cleaned AS m
LEFT JOIN continents2 AS c ON m.Code = c.`alpha-3`
WHERE m.Code IS NOT NULL;
```

### Questions

**Question 1: What is the average Child Mortality Rate per Region in the most recent year?**
```sql
SELECT 
    region, 
    ROUND(AVG(CMR), 2) AS Avg_Mortality
FROM child_mortality_data
WHERE Year = 2021
GROUP BY region
ORDER BY Avg_Mortality DESC;
```
**Question 2: What are the regional averages**
```sql
SELECT region, ROUND(AVG(CMR),2) as Avg_Mortality
FROM child_mortality_data
GROUP BY region;
```
**Question 3: Which countries have "High Health Efficiency"? (Low GDP but also Low Mortality).**
```sql
SELECT 
    Entity, 
    Code, 
    CMR, 
    GDP, 
    region
FROM child_mortality_data
WHERE Year = (SELECT MAX(Year) FROM child_mortality_data) -- Recent year
  AND GDP < (SELECT AVG(GDP) FROM child_mortality_data) -- Lower than avg wealth
  AND CMR < (SELECT AVG(CMR) FROM child_mortality_data ) -- Better than avg health
ORDER BY CMR ASC;
```

 
