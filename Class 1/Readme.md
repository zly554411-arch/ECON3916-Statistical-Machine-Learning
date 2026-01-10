# 🍔 Global Purchasing Power Parity Analysis via the Big Mac Index

## Objective

This project applies the **Law of One Price** to real-world exchange rate data using *The Economist's* Big Mac Index, testing whether currency valuations reflect purchasing power parity across international markets.

## Methodology

- **Data Construction**: Manually ingested 2015 Big Mac Index data using Python dictionaries, capturing local Big Mac prices and official exchange rates across multiple countries
- **Implied PPP Calculation**: Computed theoretical exchange rates based on the ratio of Big Mac prices between each country and the United States
- **Currency Valuation Analysis**: Derived percentage deviations between market exchange rates and PPP-implied rates to identify overvalued and undervalued currencies
- **Technical Implementation**: Leveraged Pandas for data manipulation and cross-country comparative analysis

## Economic Framework

The **Big Mac Index**, coined as "Burgernomics" by *The Economist*, provides an accessible test of purchasing power parity (PPP). Under the Law of One Price, identical goods should cost the same across countries when expressed in a common currency. Deviations from this equilibrium suggest currency misalignment and potential arbitrage opportunities.

By comparing the actual exchange rate to the PPP-implied exchange rate (derived from Big Mac prices), we can assess whether currencies are trading above or below their theoretical fair v
