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

## Project Objectives

The main objectives of this project were to:

- Analyse electricity consumption and production across Norway.
- Compare energy activity across the five Norwegian price areas, NO1–NO5.
- Examine the contribution of different electricity production sources.
- Identify regional electricity surpluses and deficits.
- Analyse monthly and hourly spot-price patterns.
- Investigate seasonal changes in hydropower reservoir filling.
- Compare hydrological conditions across Norwegian price areas.
- Explore the relationship between reservoir conditions and electricity spot prices.
- Build an interactive Power BI dashboard using multiple datasets and a structured data model.
- Strengthen practical skills in Power Query, DAX, data modelling, and business-oriented data visualisation.

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

This project combines multiple publicly available Norwegian energy datasets.

### Electricity Consumption Data

**Source:** Elhub

The consumption dataset contains electricity usage information by:

- Date and time
- Price area
- Consumer group
- Electricity consumption in kWh

The data was used to analyse:

- Total electricity consumption
- Regional consumption differences
- Consumption by consumer group
- Monthly consumption trends
- Hourly consumption patterns

### Electricity Production Data

**Source:** Elhub

The production dataset contains electricity generation information by:

- Date and time
- Price area
- Production source
- Electricity production in kWh

The data was used to analyse:

- Total electricity production
- Regional production differences
- Production by energy source
- Monthly production trends
- Hourly production patterns

### Electricity Spot Price Data

**Source:** Historical Norwegian electricity spot-price data

The spot-price dataset contains electricity prices for Norway’s five bidding zones:

- NO1
- NO2
- NO3
- NO4
- NO5

The data was transformed and analysed in NOK/kWh.

It was used to analyse:

- Average electricity spot price
- Regional price differences
- Monthly spot-price trends
- Hourly spot-price patterns
- Spot price in relation to electricity consumption and production

### Hydropower Reservoir Data

**Source:** Norwegian Water Resources and Energy Directorate (NVE)

Reservoir statistics were retrieved from the NVE public API.

The dataset includes:

- Date
- Year
- Week
- Reservoir filling level
- Reservoir capacity
- Stored hydropower energy
- Previous week reservoir filling
- Weekly change in reservoir filling
- Electricity price area

The reservoir dataset was used to analyse:

- Average reservoir filling
- Seasonal reservoir patterns
- Regional hydrological differences
- Weekly reservoir changes
- Reservoir conditions in relation to electricity spot prices

## Data Coverage

The analysis focuses on Norway’s five electricity price areas:

- NO1 – Eastern Norway
- NO2 – Southern Norway
- NO3 – Central Norway
- NO4 – Northern Norway
- NO5 – Western Norway

The datasets contain different time granularities:

- Electricity consumption: hourly
- Electricity production: hourly
- Spot prices: hourly
- Reservoir statistics: weekly

Because the reservoir dataset is weekly while the other datasets are more detailed, aggregation was necessary when combining hydrological and electricity-market information.

## Data Preparation and Transformation

Power Query was used to clean, reshape, and standardise the datasets before loading them into the Power BI data model.

### Consumption Data Preparation

The electricity consumption dataset was cleaned and transformed by:

- Removing unnecessary columns.
- Removing fields that were not required for analysis.
- Creating a clean Date field.
- Extracting Year, Month, Month Number, and Hour.
- Standardising the Price Area field.
- Checking and correcting data types.
- Preparing the consumption values for analysis in kWh.

The final consumption table includes fields such as:

- Date
- Year
- Month
- Month Number
- Hour
- Price Area
- Consumption Group
- Consumption kWh

### Production Data Preparation

The electricity production dataset was prepared using a similar process.

The main transformation steps included:

- Removing unnecessary columns.
- Creating a clean Date field.
- Extracting Year, Month, Month Number, and Hour.
- Standardising Price Area values.
- Checking numeric data types.
- Preparing production values for analysis in kWh.
- Simplifying the production-source categories for clearer reporting.

A calculated column was created to group production sources into cleaner categories such as Hydro, Wind, Solar, Thermal, and Other.

### Spot Price Data Preparation

The original spot-price dataset contained separate columns for each Norwegian price area:

- NO1
- NO2
- NO3
- NO4
- NO5

The dataset was transformed from wide format into long format using Power Query.

The NO1–NO5 columns were unpivoted into:

- Price Area
- Spot Price NOK/kWh

Additional fields were then created for:

- Date
- Hour

This transformation made the data easier to connect to the shared Date and Price Area dimension tables.

### Reservoir Data Preparation

Hydropower reservoir statistics were retrieved from the NVE public API and transformed in Power Query.

The main preparation steps included:

- Expanding the API records.
- Renaming technical field names into more readable business names.
- Converting the date field into Date format.
- Keeping the relevant hydrological fields.
- Filtering the data to the required analytical period.
- Creating a Price Area field from the NVE area number.
- Restricting the analysis to NO1–NO5.
- Formatting Reservoir Filling as a percentage.
- Preparing Stored Energy values in TWh.
- Preparing Weekly Change for percentage analysis.

The final reservoir dataset contains fields such as:

- Date
- Year
- Week
- Price Area
- Reservoir Filling
- Capacity TWh
- Stored Energy TWh
- Previous Week Filling
- Weekly Change

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

The final Power BI report contains six analytical pages, each focusing on a different part of the Norwegian electricity system.

---

### 1. Norway Energy Overview

The overview page provides a high-level summary of Norway’s electricity system.

It includes:

- Total Electricity Consumption
- Total Electricity Production
- Net Energy Balance
- Renewable Share
- Production Mix by Energy Source
- Monthly Electricity Consumption vs Production
- Year and Price Area slicers

The page provides a quick overview of overall energy performance and makes it easy to compare consumption and production patterns over time.

---

### 2. Consumption Analysis

The Consumption Analysis page focuses on electricity demand.

It includes:

- Electricity Consumption by Price Area
- Electricity Consumption by Consumer Group
- Monthly Electricity Consumption Trend
- Average Electricity Consumption by Hour of Day
- Year and Price Area slicers

This page helps identify regional differences, the largest consumer categories, seasonal consumption patterns, and the typical daily demand profile.

---

### 3. Production Analysis

The Production Analysis page focuses on electricity generation.

It includes:

- Electricity Production by Price Area
- Electricity Production by Energy Source
- Monthly Electricity Production Trend
- Average Electricity Production by Hour of Day
- Year and Price Area slicers

This page highlights regional production differences and shows the strong contribution of hydropower to Norway’s electricity system.

---

### 4. Energy Balance

The Energy Balance page compares electricity production and consumption.

It includes:

- Net Energy Balance KPI
- Consumption vs Production by Price Area
- Energy Balance by Price Area
- Monthly Energy Balance Trend
- Year and Price Area slicers

The page helps identify which regions generate more electricity than they consume and which regions have a deficit.

A positive energy balance indicates that production exceeds consumption, while a negative balance indicates that consumption exceeds production.

---

### 5. Power Market & Price Analysis

The Power Market & Price Analysis page focuses on electricity spot prices and their relationship with electricity activity.

It includes:

- Average Spot Price KPI
- Average Spot Price by Price Area
- Monthly Spot Price Trend
- Average Spot Price by Hour of Day
- Spot Price vs Consumption and Production
- Year and Price Area slicers

This page helps identify how electricity prices vary between NO1–NO5, across months, and throughout the day.

The combined chart also makes it possible to compare electricity prices with production and consumption patterns.

---

### 6. Hydrology & Reservoir Analysis

The Hydrology & Reservoir Analysis page focuses on hydropower reservoir conditions.

It includes:

- Average Reservoir Filling KPI
- Reservoir Filling Over Time
- Average Reservoir Filling by Price Area
- Weekly Change in Reservoir Filling
- Reservoir Filling vs Spot Price
- Year and Price Area slicers

The page shows how reservoir levels change seasonally and how hydrological conditions differ across NO1–NO5.

Weekly reservoir change provides a short-term view of whether reservoirs are being replenished or drawn down.

The comparison between reservoir filling and spot prices provides additional market context, although it should be interpreted as a relationship rather than proof of causation.
