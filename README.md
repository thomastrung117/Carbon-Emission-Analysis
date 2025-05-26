# Carbon-Emission-Analysis

## Which products contribute the most to carbon emissions?
```SQL
SELECT product_name, 
       ROUND(SUM(carbon_footprint_pcf), 2) AS total_carbon_emissions
FROM product_emissions
GROUP BY product_name
ORDER BY total_carbon_emissions DESC
LIMIT 10;
```
RESULT:
| product_name                                                                                                                       | total_carbon_emissions | 
| :--------------------------------------------------------------------------------------------------------------------------------- | ---------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00             | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00             | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00             | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00             | 
| TCDE                                                                                                                               | 198150.00              | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00              | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00              | 
| Electric Motor                                                                                                                     | 160655.00              | 
| Audi A6                                                                                                                            | 111282.00              | 
| Average of all GM vehicles produced and used in the 10 year life-cycle.                                                            | 100621.00              | 

## What are the industry groups of these products?
```SQL
SELECT pe.product_name, ig.industry_group, 
       ROUND(SUM(pe.carbon_footprint_pcf), 2) AS total_carbon_emissions
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY pe.product_name, ig.industry_group
ORDER BY total_carbon_emissions DESC
LIMIT 10;
```

RESULT:
| product_name                                                                                                                       | industry_group                     | total_carbon_emissions | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | ---------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3718044.00             | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3276187.00             | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 1532608.00             | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 1251625.00             | 
| TCDE                                                                                                                               | Materials                          | 198150.00              | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 191687.00              | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 167000.00              | 
| Electric Motor                                                                                                                     | Capital Goods                      | 140647.00              | 
| Audi A6                                                                                                                            | Automobiles & Components           | 111282.00              | 
| Average of all GM vehicles produced and used in the 10 year life-cycle.                                                            | Automobiles & Components           | 100621.00              | 

## What are the industries with the highest contribution to carbon emissions?

```SQL
SELECT ig.industry_group, 
       ROUND(SUM(pe.carbon_footprint_pcf), 2) AS total_carbon_emissions
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY ig.industry_group
ORDER BY total_carbon_emissions DESC
LIMIT 10;
```

RESULT:
| industry_group                                   | total_carbon_emissions | 
| -----------------------------------------------: | ---------------------: | 
| Electrical Equipment and Machinery               | 9801558.00             | 
| Automobiles & Components                         | 2582264.00             | 
| Materials                                        | 577595.00              | 
| Technology Hardware & Equipment                  | 363776.00              | 
| Capital Goods                                    | 258712.00              | 
| "Food, Beverage & Tobacco"                       | 111131.00              | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486.00               | 
| Chemicals                                        | 62369.00               | 
| Software & Services                              | 46544.00               | 
| Media                                            | 23017.00               | 

### What are the companies with the highest contribution to carbon emissions?

```SQL
SELECT c.company_name, 
       ROUND(SUM(pe.carbon_footprint_pcf), 2) AS total_carbon_emissions
FROM product_emissions pe
JOIN companies c ON pe.company_id = c.id
GROUP BY c.company_name
ORDER BY total_carbon_emissions DESC
LIMIT 10;
```

RESULT:
| company_name                            | total_carbon_emissions | 
| --------------------------------------: | ---------------------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 9778464.00             | 
| Daimler AG                              | 1594300.00             | 
| Volkswagen AG                           | 655960.00              | 
| "Mitsubishi Gas Chemical Company, Inc." | 212016.00              | 
| "Hino Motors, Ltd."                     | 191687.00              | 
| Arcelor Mittal                          | 167007.00              | 
| Weg S/A                                 | 160655.00              | 
| General Motors Company                  | 137007.00              | 
| "Lexmark International, Inc."           | 132012.00              | 
| "Daikin Industries, Ltd."               | 105600.00              | 



### 6️⃣ Trend of Carbon Footprints (PCFs) Over the Year

Evaluate the historical trend of carbon emissions:
```SQL
SELECT year, 
       ROUND(SUM(carbon_footprint_pcf), 2) AS total_carbon_emissions
FROM product_emissions
GROUP BY year
ORDER BY year ASC;
```

RESULT:
| year | total_carbon_emissions | 
| ---: | ---------------------: | 
| 2013 | 503857.00              | 
| 2014 | 624226.00              | 
| 2015 | 10840415.00            | 
| 2016 | 1640182.00             | 
| 2017 | 340271.00              | 

### Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

