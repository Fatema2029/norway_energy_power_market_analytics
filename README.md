# norway_energy_power_market_analytics
Power BI analysis of Norway’s electricity consumption, production, spot prices, energy balance and hydropower reservoir conditions across NO1–NO5.
# Norway Energy & Power Market Analytics

## Project Overview

This Power BI project analyses Norway’s electricity system by combining electricity consumption, electricity production, regional energy balance, spot prices, and hydropower reservoir conditions.

The analysis covers Norway’s five electricity price areas:

- NO1 – Eastern Norway
- NO2 – Southern Norway
- NO3 – Central Norway
- NO4 – Northern Norway
- NO5 – Western Norway

The purpose of the project is to provide a structured view of how electricity demand, generation, market prices, regional differences, and hydrological conditions interact within the Norwegian power system.

The final Power BI report contains six analytical dashboard pages:

1. Norway Energy Overview
2. Consumption Analysis
3. Production Analysis
4. Energy Balance
5. Power Market & Price Analysis
6. Hydrology & Reservoir Analysis

## Project Objective

The objective of this project was to build a comprehensive Power BI dashboard that provides a clear and practical understanding of Norway’s electricity system by combining several related datasets into one analytical model. Rather than looking at electricity consumption, production, prices, or hydropower conditions separately, the aim was to connect these elements and examine how they interact across Norway’s five electricity price areas, NO1–NO5.

The project was designed to explore both operational and market-related questions. This included analysing how electricity consumption and production vary across regions and over time, identifying the main sources of electricity generation, comparing regional energy surpluses and deficits, and examining how spot prices differ between price areas and throughout the day. Because hydropower plays such an important role in Norway’s electricity system, reservoir filling levels and weekly changes were also included to provide additional context around generation conditions and electricity-market behaviour.

From a technical perspective, another important objective was to strengthen practical Power BI skills by working with multiple real-world datasets. This involved cleaning and transforming data in Power Query, reshaping spot-price data, building relationships between fact and dimension tables, creating DAX measures, and designing interactive visuals that could be filtered by year and price area. Overall, the project was intended to demonstrate how Power BI can be used to turn complex energy data into a structured and understandable analytical dashboard.

## Dashboard Preview

The Power BI report contains six interactive pages covering electricity consumption, production, regional energy balance, market prices, and hydropower conditions in Norway.

### 1. Norway Energy Overview

![Norway Energy Overview](1.%20Energy%20overview.png)

The overview provides a high-level view of total electricity consumption, production, energy balance, renewable share, production mix, and monthly consumption versus production.

---

### 2. Consumption Analysis

![Consumption Analysis](2.%20Consumption.png)

This page analyses electricity consumption across Norwegian price areas and consumer groups, together with monthly and hourly demand patterns.

---

### 3. Production Analysis

![Production Analysis](3.%20Production.png)

This page examines electricity production across NO1–NO5, the contribution of different energy sources, and monthly and hourly production patterns.

---

### 4. Energy Balance

![Energy Balance](4.%20Energy%20Balance.png)

This page compares electricity production with consumption and highlights regional electricity surpluses and deficits across the Norwegian price areas.

---

### 5. Power Market & Price Analysis

![Power Market and Price Analysis](5.%20Power%20market%3A%20price%20analysis.png)

This page analyses electricity spot prices across NO1–NO5, monthly and hourly price movements, and the relationship between spot prices, electricity consumption, and production.

---

### 6. Hydrology & Reservoir Context

![Hydrology and Reservoir Context](6.%20Hydrology%3A%20reservoir%20context.png)

This page analyses reservoir filling levels, regional hydrological differences, weekly changes in reservoir filling, and the relationship between reservoir conditions and electricity spot prices.

## Business Questions

The dashboard was designed to answer the following questions:

- How much electricity is consumed and produced in Norway?
- How does electricity consumption differ between NO1–NO5?
- Which consumer groups account for the highest electricity consumption?
- How does electricity production differ across price areas?
- Which energy sources dominate Norwegian electricity production?
- Which price areas produce more electricity than they consume?
- How does the electricity balance change over time?
- How do spot prices differ across NO1–NO5?
- How do electricity prices change by month and hour of the day?
- How do production and consumption compare with electricity prices?
- How do hydropower reservoir levels change over time?
- How do reservoir conditions differ across Norwegian price areas?
- Is there a visible relationship between reservoir filling and electricity spot prices?

## Data Sources

The project combines several publicly available datasets covering different parts of the Norwegian electricity system.

Electricity consumption and production data were taken from **Elhub**. These datasets provide hourly information across the Norwegian price areas and make it possible to analyse how electricity demand and generation vary by region, consumer group, production source, month, and hour of the day.

To add a market perspective, I also used historical electricity spot-price data for the five Norwegian bidding zones, **NO1–NO5**. The original price data was structured with one column for each price area, so it was reshaped in Power Query before being connected to the rest of the model. This dataset was used to compare regional price differences and to study monthly and hourly price movements.

For the hydrology analysis, I used reservoir statistics from the **Norwegian Water Resources and Energy Directorate (NVE)**. The data was retrieved through NVE's public API and includes weekly reservoir filling, stored hydropower energy, reservoir capacity, and weekly changes in filling levels. This added an important hydrological dimension to the project, particularly because hydropower plays such a large role in Norwegian electricity production.

Together, these sources made it possible to analyse the power system from several perspectives: electricity demand, generation, regional balance, market prices, and reservoir conditions.

## Data Preparation and Transformation

Before building the dashboard, the raw datasets were cleaned and transformed in Power Query so that they could be analysed consistently within one model. Because the project combines several sources with different structures, the preparation stage focused on standardising dates, time fields, price-area identifiers, numeric formats, and category names.

### Consumption Data Preparation

The electricity consumption dataset was cleaned by removing fields that were not needed for the analysis and checking that the remaining columns used the correct data types. Date and time information was separated into useful analytical fields such as Date, Year, Month, Month Number, and Hour. The Price Area field was standardised so that NO1–NO5 could be used consistently across the model. The final table was structured to support analysis by region, consumer group, month, and hour while keeping electricity consumption values in kWh.

### Production Data Preparation

The production dataset was prepared using a similar process. Unnecessary fields were removed, date and time values were converted into analytical fields, and Price Area values were standardised. Production values were checked and formatted correctly for analysis in kWh. To make the visuals easier to interpret, the original production categories were also simplified into clearer groups such as Hydro, Wind, Solar, Thermal, and Other. This made it possible to compare Norway’s generation mix more clearly in the dashboard.

### Spot Price Data Preparation

The spot-price dataset required more restructuring because the original file stored NO1, NO2, NO3, NO4, and NO5 as separate columns. In Power Query, these regional columns were unpivoted so that the final table contained a single Price Area column and a single Spot Price NOK/kWh column. Date and Hour fields were then extracted from the original date-time information. This transformation made the table compatible with the shared Date and Price Area dimensions and allowed regional, monthly, and hourly price analysis to be performed more efficiently.

### Reservoir Data Preparation

The hydropower reservoir data was retrieved from the NVE public API and required additional cleaning before it could be integrated into the model. The API records were expanded, technical field names were renamed into more understandable business terms, and the date field was converted into a proper Date format. The data was filtered to the relevant analytical period, and the NVE area numbers were converted into the corresponding NO1–NO5 price-area labels. Reservoir Filling was formatted as a percentage, while stored hydropower energy was kept in TWh. Weekly change and previous-week filling values were also retained so that both long-term seasonal patterns and short-term reservoir movements could be analysed.

Overall, the transformation process ensured that the four main fact tables followed a consistent structure and could be connected through common Date and Price Area dimensions. This preparation was essential for creating reliable cross-page filtering and meaningful comparisons between consumption, production, spot prices, and hydrological conditions.

## Data Model and Relationships

A structured star-style data model was created in Power BI to connect the different datasets through shared dimension tables.

The main fact tables are:

- Consumption
- Production
- SpotPrice
- ReservoirData

The main dimension tables are:

- DateTable
- PriceArea

The relationships were created as one-to-many relationships, with the dimension tables on the one side and the fact tables on the many side.

### Date Relationships

- DateTable[Date] → Consumption[Date]
- DateTable[Date] → Production[Date]
- DateTable[Date] → SpotPrice[Date]
- DateTable[Date] → ReservoirData[dato_Id]

### Price Area Relationships

- PriceArea[Price Area] → Consumption[Price Area]
- PriceArea[Price Area] → Production[Price Area]
- PriceArea[Price Area] → SpotPrice[Price Area]
- PriceArea[Price Area] → ReservoirData[Price Area]

Cross-filter direction was kept as **Single** to maintain a clean and controlled model structure.

This setup allows the same Year and Price Area slicers to filter multiple datasets consistently across the dashboard.

---

## Price Area Dimension

A dedicated Price Area dimension was used to standardise Norway's five electricity bidding zones across the different datasets.

The dimension contains:

- NO1
- NO2
- NO3
- NO4
- NO5

The Price Area dimension allows the same regional slicer to filter electricity consumption, production, spot-price, and hydropower reservoir data consistently.

Using separate Date and Price Area dimensions also reduces duplication and creates a cleaner analytical model.

## Key DAX Measures

Several DAX measures were created to support the main KPIs and analytical visuals across the dashboard.

### Total Electricity Consumption

```DAX
Total Consumption kWh =
SUM(Consumption[Consumption kWh])
```

This measure calculates total electricity consumption and is used across the Overview, Consumption Analysis, Energy Balance, and Power Market pages.

---

### Total Electricity Production

```DAX
Total Production kWh =
SUM(Production[Production kWh])
```

This measure calculates total electricity generation and is used across the Overview, Production Analysis, Energy Balance, and Power Market pages.

---

### Energy Balance

```DAX
Energy Balance kWh =
[Total Production kWh] - [Total Consumption kWh]
```

A positive value indicates that electricity production exceeds consumption, while a negative value indicates that consumption exceeds production.

---

### Renewable Production

```DAX
Renewable Production kWh =
CALCULATE(
    [Total Production kWh],
    Production[Production Group] IN {
        "Hydro unspecified",
        "Wind unspecified",
        "Solar unspecified"
    }
)
```

This measure calculates electricity production from renewable sources.

---

### Renewable Share

```DAX
Renewable Share % =
DIVIDE(
    [Renewable Production kWh],
    [Total Production kWh],
    0
)
```

This measure calculates the share of total electricity generation coming from renewable sources.

---

### Average Hourly Consumption

```DAX
Average Hourly Consumption kWh =
AVERAGEX(
    VALUES(Consumption[Date]),
    CALCULATE([Total Consumption kWh])
)
```

This measure supports the analysis of the typical hourly electricity consumption pattern.

---

### Average Hourly Production

```DAX
Average Hourly Production kWh =
AVERAGEX(
    VALUES(Production[Date]),
    CALCULATE([Total Production kWh])
)
```

This measure supports the analysis of the typical hourly electricity production pattern.

---

### Average Spot Price

```DAX
Average Spot Price NOK/kWh =
AVERAGE(SpotPrice[Spot Price NOK/kWh])
```

This measure calculates the average electricity spot price and is used for regional, monthly, and hourly price analysis.

---

### Average Reservoir Filling

```DAX
Average Reservoir Filling =
AVERAGE(ReservoirData[Reservoir Filling])
```

This measure calculates the average hydropower reservoir filling level.

---

### Average Reservoir Filling Clean

```DAX
Average Reservoir Filling Clean =
CALCULATE(
    AVERAGE(ReservoirData[Reservoir Filling]),
    ReservoirData[Price Area] IN {
        "NO1",
        "NO2",
        "NO3",
        "NO4",
        "NO5"
    }
)
```

This measure restricts reservoir analysis to the five Norwegian electricity price areas.

---

### Average Stored Hydropower Energy

```DAX
Average Stored Energy TWh =
AVERAGE(ReservoirData[Store Energy TWh])
```

This measure calculates average stored hydropower energy in TWh.

---

### Average Weekly Reservoir Change

```DAX
Average Weekly Change =
AVERAGE(ReservoirData[Weekly Change])
```

This measure shows short-term changes in reservoir conditions.

Positive values indicate increasing reservoir filling, while negative values indicate reservoir drawdown.

## Dashboard Analysis

### 1. Norway Energy Overview

The Norway Energy Overview page was designed to provide a high-level summary of the electricity system before moving into more detailed analysis. It brings together the main indicators for total electricity consumption, total production, net energy balance, and renewable share, giving a quick view of the overall system performance. The production mix visual shows the contribution of different generation sources and makes the dominance of hydropower immediately visible, while the monthly consumption-versus-production chart highlights how both demand and generation change over time. Year and Price Area slicers allow the user to explore the same indicators for different periods and regions, making this page the main entry point to the dashboard.

### 2. Consumption Analysis

The Consumption Analysis page explores electricity demand in more detail and shows how consumption varies across regions, customer groups, time periods, and hours of the day. The comparison across NO1–NO5 helps identify differences in regional electricity demand, while the consumer-group analysis provides a clearer view of which categories account for the largest share of consumption. The monthly trend reveals seasonal changes in demand, particularly the effect of colder and warmer periods, and the hourly profile shows how electricity use changes throughout a typical day. Together, these visuals provide a more complete picture of when and where electricity demand is highest.

### 3. Production Analysis

The Production Analysis page focuses on how electricity is generated across Norway and how production patterns differ by location and source. Regional production is compared across the five price areas, while the production-source analysis shows the contribution of hydropower, wind, thermal, solar, and other sources. The monthly production trend helps identify seasonal variation in generation, and the hourly analysis provides additional insight into how electricity production behaves during different parts of the day. This page is particularly useful for understanding the structure of Norway’s generation system and the central role of hydropower.

### 4. Energy Balance

The Energy Balance page combines consumption and production to show whether different parts of the electricity system are operating with a surplus or deficit. A comparison of consumption and production by price area makes it possible to see which regions generate more electricity than they use and which depend more heavily on electricity supplied from elsewhere. The Energy Balance measure calculates the difference between production and consumption, while the monthly trend shows how this balance changes over time. This page adds an important regional perspective because high production alone does not necessarily indicate a surplus unless it is considered together with local electricity demand.

### 5. Power Market & Price Analysis

The Power Market & Price Analysis page introduces the market dimension of the project by examining electricity spot prices across NO1–NO5. It compares average prices between the five bidding zones and also shows how prices change from month to month and throughout the day. The combined consumption, production, and spot-price visual brings physical electricity-system activity and market prices into the same analysis, making it easier to explore periods when changes in supply or demand occur alongside price movements. This page demonstrates that Norway does not operate as one uniform electricity-price market and that regional and temporal differences can be substantial.

### 6. Hydrology & Reservoir Analysis

The Hydrology & Reservoir Analysis page adds an important hydropower perspective to the dashboard. Reservoir filling levels are analysed over time to show the strong seasonal cycle associated with inflow, storage, and electricity generation. Regional reservoir conditions are compared across NO1–NO5, while the weekly change measure provides a more detailed view of short-term replenishment and drawdown. The final comparison between reservoir filling and electricity spot prices connects hydrological conditions with market behaviour. Because electricity prices are also affected by demand, transmission capacity, imports and exports, weather, and wider European market conditions, this comparison is intended to provide additional context rather than establish a direct causal relationship.

## Key Insights and Findings

The dashboard highlights several important patterns in Norway’s electricity system.

### Hydropower Dominates Electricity Production

Hydropower represents the largest share of electricity generation in the dataset.

Wind contributes a smaller but still significant share, while thermal, solar, and other sources account for much smaller proportions.

This confirms the strong dependence of the Norwegian electricity system on hydropower.

---

### Electricity Consumption Shows Clear Seasonal Patterns

Electricity demand changes significantly throughout the year.

Consumption tends to increase during colder periods and decrease during warmer months.

This reflects the importance of heating and seasonal energy demand in Norway.

---

### Regional Differences Are Significant

The five Norwegian price areas show noticeable differences in:

- Electricity consumption
- Electricity production
- Energy balance
- Spot prices
- Reservoir conditions

This demonstrates why regional analysis is important when examining the Norwegian power market.

---

### Production and Consumption Are Not Evenly Balanced Across Regions

Some price areas produce more electricity than they consume, while others show a lower production-to-consumption balance.

The Energy Balance page helps identify regional electricity surpluses and deficits.

---

### Spot Prices Vary Across Time and Price Areas

Electricity spot prices differ between NO1–NO5 and also change considerably over time.

The monthly and hourly analyses show that spot prices are influenced by both seasonal and short-term market conditions.

---

### Reservoir Levels Follow a Strong Seasonal Cycle

Reservoir filling levels rise and fall throughout the year.

The pattern reflects periods of water inflow, storage, and hydropower generation.

The Weekly Change measure gives an additional short-term view of whether reservoir levels are increasing or decreasing.

---

### Hydrology Provides Important Market Context

Reservoir conditions are highly relevant in a hydropower-dominated electricity system.

Comparing reservoir filling with spot prices helps provide context for electricity-market developments.

However, the relationship should not be interpreted as direct causation because electricity prices are also affected by many other factors, including:

- Electricity demand
- Generation availability
- Transmission constraints
- Imports and exports
- Weather conditions
- European electricity-market conditions

## Project Challenges

Several practical challenges were addressed during the development of this project.

### Data Integration

The project combines multiple datasets with different structures and time granularities.

For example:

- Electricity consumption data is hourly.
- Electricity production data is hourly.
- Spot-price data is hourly.
- Reservoir data is weekly.

This required careful preparation and aggregation before the datasets could be analysed together.

---

### Data Transformation

The spot-price dataset originally stored NO1–NO5 as separate columns.

To make the data suitable for analysis, these columns were unpivoted into:

- Price Area
- Spot Price NOK/kWh

This made it possible to connect the spot-price data to the common Price Area dimension.

---

### Standardising Regional Data

The different datasets did not always use identical structures for regional information.

Price-area identifiers had to be standardised so that NO1–NO5 could be used consistently across:

- Consumption
- Production
- Spot prices
- Reservoir data

---

### Handling Blank and Unmatched Values

Some regional and hydrological records produced blank or unmatched values during modelling.

These issues were handled through data cleaning, filtering, and dedicated measures to ensure that the dashboard focuses on the five valid Norwegian price areas.

---

### Map Visualisation

A custom map showing Norway’s electricity price areas was explored during development.

However, Power BI’s mapping limitations and account requirements made the custom NO1–NO5 map unreliable for the final report.

Instead, regional comparisons were presented using bar and column charts, which provide a clearer and more stable analytical view.

---

### Different Time Granularities

Reservoir statistics are reported weekly, while the electricity and price datasets contain hourly observations.

Because of this difference, hydrology and electricity-market comparisons require aggregation.

The comparison between reservoir filling and spot prices should therefore be interpreted as a descriptive relationship rather than an exact one-to-one time comparison.

---

## Future Improvements

The project could be extended further in several practical ways.

### 1. Add Weather and Temperature Data

Weather conditions have a strong influence on electricity demand and hydropower availability.

A future version could integrate temperature, precipitation, and snowmelt data and connect them to the existing Date dimension.

This would make it possible to analyse questions such as:

- How strongly does temperature affect electricity consumption?
- Do periods of higher precipitation lead to improved reservoir conditions?
- How do weather changes influence electricity prices?

---

### 2. Include Electricity Import and Export Data

Norway is connected to neighbouring electricity markets through several interconnectors.

Adding import and export data would provide a more complete explanation of regional energy balances and price movements.

The data could be added as a new fact table and connected through Date and relevant market-area dimensions.

This would allow analysis of:

- Net electricity imports and exports
- Cross-border electricity flows
- How international electricity trade relates to Norwegian spot prices

---

### 3. Develop Forecasting Models

The current dashboard focuses on historical analysis.

A future version could introduce forecasting for:

- Electricity consumption
- Spot prices
- Reservoir filling

Forecasting could be developed using Power BI forecasting features, Python, or statistical and machine-learning models.

Historical trends, seasonality, weather variables, and reservoir conditions could be used as predictive inputs.

---

### 4. Automate Data Refresh

The current project uses several public data sources, including API-based reservoir data.

A future version could automate data retrieval and refresh so that the dashboard remains up to date with minimal manual work.

This could be implemented through API connections, Power Query, and scheduled refresh in the Power BI Service.

Automated refresh would make the project more suitable for continuous energy-market monitoring rather than only historical analysis.

## Conclusion

This project demonstrates how multiple public energy datasets can be combined in Power BI to create a structured view of Norway’s electricity system.

By integrating electricity consumption, production, regional energy balance, spot prices, and hydropower reservoir data, the dashboard provides both operational and market-level insights across the five Norwegian price areas, NO1–NO5.

The project shows how Power BI can be used not only for visualisation, but also for:

- Cleaning and transforming raw data
- Building relationships across multiple datasets
- Creating DAX measures and KPIs
- Analysing time-based and regional patterns
- Comparing physical electricity-system conditions with market prices
- Communicating complex energy data through interactive dashboards

The analysis highlights the importance of hydropower in Norway, the seasonal nature of electricity consumption and reservoir conditions, and the significant regional differences in production, energy balance, and spot prices.

Overall, the project strengthened practical skills in **Power BI, Power Query, DAX, data modelling, data visualisation, and energy-market analysis**, while also providing experience working with real-world public datasets.
