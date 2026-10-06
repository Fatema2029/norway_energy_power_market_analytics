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
