# Lab 2: The Illusion of Growth & The Composition Effect

## Objective

Built a Python pipeline to ingest live economic data from the Federal Reserve Economic Data (FRED) API to analyze wage stagnation and correct for statistical biases. This project demonstrates how nominal wage growth can mask stagnant real purchasing power and how compositional changes in the workforce can create misleading statistical artifacts.

## Methodology

### Data Acquisition & Processing
Leveraged the `fredapi` library to fetch real-time economic indicators from the Federal Reserve Bank of St. Louis:

- **Nominal Wage Data (AHETPI)**: Average hourly earnings of production and nonsupervisory employees
- **Consumer Price Index (CPI)**: Used to deflate nominal wages and calculate real purchasing power
- **Employment Cost Index (ECIWAG)**: Composition-adjusted wage measure that controls for workforce mix changes

### Analysis Pipeline

1. **Real Wage Calculation**: Computed inflation-adjusted wages by deflating nominal wages with CPI, revealing the true purchasing power trajectory from 1964 to present

2. **Anomaly Detection**: Identified a statistically significant spike in average wages during the 2020 pandemic period that contradicted economic fundamentals

3. **Composition Effect Correction**: Deployed the Employment Cost Index (ECI) to control for workforce composition bias. The ECI holds job mix constant, isolating true wage growth from statistical artifacts caused by workforce compositional changes

### Technical Implementation
- **API Integration**: `fredapi` for automated data retrieval
- **Data Processing**: `pandas` for time-series manipulation, filtering, and rebasing
- **Visualization**: `matplotlib` for creating publication-quality economic charts

## Key Findings

### The Money Illusion
Visualized five decades of wage data revealing that despite substantial nominal wage growth, real wages have remained largely flat since the 1970s. Workers experience the "money illusion"—feeling richer as their paychecks grow nominally while their actual purchasing power stagnates.

### The Pandemic Paradox
Uncovered a critical statistical artifact in 2020 wage data: standard measures showed a dramatic wage increase during the pandemic, but this "boom" was entirely artificial. The spike resulted from the **Composition Effect**—low-wage service workers disproportionately lost jobs, mechanically raising the average without any individual worker receiving higher pay.

By comparing standard average wages against the composition-adjusted Employment Cost Index, the analysis proved that:
- Standard metrics showed an artificial 3-5% wage spike in 2020
- ECI data revealed stable, modest wage growth throughout the pandemic
- The divergence quantified the magnitude of composition bias in economic statistics

This project demonstrates how sophisticated economic analysis requires not just data collection, but critical evaluation of measurement methodology and awareness of statistical pitfalls that can mislead policymakers and the public.
