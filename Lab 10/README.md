📊 Spurious Correlation & Multicollinearity in Macroeconomic Time Series
Overview
This project investigates the critical challenges of spurious correlation and multicollinearity in macroeconomic time-series analysis using data from the Federal Reserve Economic Data (FRED) API. Through systematic diagnostics and transformations, the analysis demonstrates how raw level data can produce misleading correlation patterns and how proper statistical techniques reveal true underlying structural relationships. The work emphasizes best practices for econometric modeling with non-stationary data.

Methodology
1. Data Collection & Visualization Retrieved macroeconomic time-series data via the FRED API and used pandas for data manipulation. Applied seaborn to create correlation matrices and scatter plots that exposed spurious relationships inherent in raw level data, demonstrating common pitfalls in naive correlation analysis.

2. Multicollinearity Diagnostics Calculated Variance Inflation Factor (VIF) scores using statsmodels to quantify the degree of redundancy among predictor variables. Identified variables exhibiting problematic multicollinearity that would compromise regression model reliability and interpretation.

3. Stationarity Transformation Transformed non-stationary level variables into Year-over-Year (YoY) growth rates to address trending behavior and achieve stationarity. This transformation removed spurious correlation patterns driven by common time trends rather than genuine economic relationships.

4. Causal Structure Mapping Constructed Directed Acyclic Graphs (DAGs) to explicitly model the true causal relationships between economic variables. This approach distinguished between correlation and causation, providing a theoretically grounded framework for understanding macroeconomic dynamics.

Key Findings
Raw level data exhibited artificially high correlations driven by common non-stationary trends rather than true relationships
VIF diagnostics revealed severe multicollinearity (VIF > 10) among several predictor variables in level form
YoY growth rate transformations successfully eliminated spurious correlations and reduced multicollinearity
DAG analysis clarified the directional causal structure, preventing misinterpretation of bidirectional relationships
Proper data transformation and causal modeling are essential for valid inference in macroeconomic analysis
Tech Stack
|------|---------|
Tool	Purpose
Python	Primary programming language for analysis
FRED API	Data retrieval from Federal Reserve Economic Database
pandas	Data manipulation and time-series handling
seaborn	Statistical data visualization
statsmodels	VIF calculation and econometric diagnostics
DAGs	Causal relationship modeling and visualization
Skills Demonstrated
API integration and automated data collection
Time-series data preprocessing and transformation
Statistical diagnostics for regression assumptions
Identification and mitigation of multicollinearity
Stationarity testing and differencing techniques
Causal inference using graphical models
Clear data visualization of complex statistical concepts
Critical evaluation of correlation vs. causation
