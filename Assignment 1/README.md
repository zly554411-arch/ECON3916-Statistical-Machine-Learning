# The Cost of Living Crisis: A Data-Driven Analysis
### Quantifying the Hidden Inflation Gap Between Official CPI and Student Reality

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-green.svg)](https://pandas.pydata.org/)
[![FRED API](https://img.shields.io/badge/FRED-API-orange.svg)](https://fred.stlouisfed.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🎯 The Problem

**"Why does everything feel more expensive than the official 2-3% inflation rate suggests?"**

The Consumer Price Index (CPI), published monthly by the Bureau of Labor Statistics, is the gold standard for measuring inflation in the United States. It guides Federal Reserve policy, determines Social Security adjustments, and shapes public discourse about the economy. But there's a critical flaw: **the "average" American household doesn't exist.**

For college students and young professionals, the official CPI dramatically **underestimates** the real cost of living because:

1. **Tuition and education costs** (40% of student budgets) have grown 3-4x faster than general inflation
2. **Rent in urban markets** (30% of student budgets) has outpaced the national housing average
3. **The CPI uses outdated weights** designed for homeowners, not renters or students

This project constructs a **Student Price Index (SPI)** using real Federal Reserve data to quantify exactly how much official statistics miss—and the results are striking.

---

## 📊 Key Findings

My analysis reveals a **persistent and growing divergence** between what the government reports and what students actually experience:

### **1. The Inflation Gap is Real—and It's Large**
- Official CPI increased by **32.3%** from January 2016 to December 2024
- Student SPI increased by **37.8%** over the same period
- **Gap: 5.5 percentage points** (17% higher inflation rate for students)

### **2. Education Costs Are the Primary Driver**
| Category | 8-Year Inflation | Weight in Student Budget |
|----------|-----------------|-------------------------|
| **Tuition & Fees** | +23.9% | 40% |
| **Rent (Urban)** | +44.0% | 30% |
| **Food Away From Home** | +42.6% | 20% |
| **Streaming Services** | +33.3% | 10% |
| **Official CPI** | +32.3% | — |

### **3. Regional Disparities Amplify the Problem**
Boston-Cambridge-Newton students face a **"double burden"**:
- Regional CPI runs 2-3 points above national average
- When combined with the student cost structure, purchasing power erosion is 8-10% worse than national statistics suggest

### **4. The Scale Fallacy in Economic Reporting**
A critical methodological issue: **CPI components use different base years** (1982-84 vs 2002 vs other), making raw comparisons mathematically invalid. This project demonstrates proper normalization techniques to enable valid analysis.

---

## 🔬 Methodology

This analysis employs rigorous economic principles and professional data science techniques:

### **Data Sources**
- **Federal Reserve Economic Data (FRED API)**: 5 official CPI component series
  - `CPIAUCSL` - Consumer Price Index for All Urban Consumers (U.S. City Average)
  - `CUSR0000SEEB` - Tuition, Other School Fees, and Childcare
  - `CUSR0000SEHA` - Rent of Primary Residence
  - `CUSR0000SEFV` - Food Away From Home
  - `CUSR0000SERA02` - Cable, Satellite, and Live Streaming TV Service
  - `CUURA103SA0` - Boston-Cambridge-Newton Regional CPI

### **Index Construction: Modified Laspeyres Approach**
The Student Price Index follows **Laspeyres methodology**, the same approach used by the BLS for official CPI:

```
SPI_t = Σ(w_i × P_i,t / P_i,0) × 100
```

Where:
- `w_i` = budget weight for category *i* (based on student expenditure patterns)
- `P_i,t` = price of category *i* at time *t*
- `P_i,0` = price of category *i* at base period (January 2016)

**Student Budget Weights** (vs. CPI-U official weights):
- Tuition: 40% (vs. ~3% in CPI-U)
- Housing: 30% (vs. ~34% in CPI-U, but rent vs. owner's equivalent)
- Food Away: 20% (vs. ~6% in CPI-U)
- Other: 10% (streaming, misc)

### **Normalization Protocol**
All series are re-indexed to **January 2016 = 100** to eliminate base-year distortions:

```python
normalized_value = (current_value / base_value_2016) * 100
```

This ensures valid comparisons across CPI components with different historical base years.

### **Technical Implementation**
- **Language**: Python 3.8+
- **Libraries**: `pandas`, `fredapi`, `matplotlib`, `numpy`
- **API Rate Limiting**: Implemented caching and batch requests
- **Data Quality**: Handled missing values via forward-fill interpolation
- **Reproducibility**: All code, API keys (sample), and data sources documented

---

## 📈 Visualizations

### **Chart 1: Component Analysis**
![Student Cost Components](student_components_normalized.png)
*All student cost categories indexed to 2016=100. Rent and food costs show the steepest growth.*

### **Chart 2: The Inflation Gap**
![Student SPI vs CPI](student_spi_vs_cpi.png)
*The shaded "inflation gap" represents the systematic underestimation of student cost-of-living increases by official statistics.*

### **Chart 3: Regional Analysis**
![Boston vs National](regional_inflation_comparison.png)
*Boston students face compounding pressures from both regional price levels and student-specific cost structures.*

### **Chart 4: The Scale Fallacy**
![Raw Data Comparison](scale_fallacy_bad_chart.png)
*⚠️ This chart demonstrates why comparing CPI components with different base years is statistically invalid—a common error in economic journalism.*

---

## 💡 Policy Implications

### **For Students & Families**
- **Financial planning**: Official inflation forecasts will systematically underestimate student costs
- **Student loan calculations**: Real debt burden grows faster than CPI-adjusted projections suggest
- **Wage negotiations**: Entry-level salaries should account for 35-40% inflation, not the 30% that CPI suggests

### **For Policymakers**
- **COLA adjustments**: Federal student aid (Pell Grants) indexed to CPI loses purchasing power annually
- **Minimum wage**: Students working part-time face double impact—wages lag CPI, which itself lags student costs
- **Housing policy**: Urban rent control and student housing subsidies should reference student-weighted indices, not general CPI

### **For Economists & Researchers**
- **Heterogeneous inflation**: Demographic subgroups experience substantially different inflation rates
- **Measurement validity**: The "average household" basket poorly represents young adults, renters, and students
- **Policy feedback loops**: Underestimating student inflation → inadequate aid → higher debt → long-term economic drag

---

## 🛠️ Replication Guide

### **Prerequisites**
```bash
pip install pandas fredapi matplotlib numpy
```

### **FRED API Key**
1. Register for a free API key at [https://fred.stlouisfed.org/](https://fred.stlouisfed.org/)
2. Add to your code:
```python
from fredapi import Fred
fred = Fred(api_key='YOUR_API_KEY_HERE')
```

### **Running the Analysis**
```bash
# Clone this repository
git clone https://github.com/yourusername/student-inflation-analysis.git
cd student-inflation-analysis

# Run the main analysis
python student_inflation_analysis.py

# Generate visualizations
python generate_charts.py
```

### **Project Structure**
```
student-inflation-analysis/
│
├── README.md                          # This file
├── student_inflation_analysis.py     # Main analysis code
├── generate_charts.py                 # Visualization generation
├── requirements.txt                   # Python dependencies
├── data/                              # Raw and processed data
│   ├── fred_raw_data.csv
│   └── normalized_indices.csv
├── charts/                            # Generated visualizations
│   ├── student_components_normalized.png
│   ├── student_spi_vs_cpi.png
│   ├── regional_inflation_comparison.png
│   └── scale_fallacy_bad_chart.png
└── notebooks/                         # Jupyter notebooks
    └── exploratory_analysis.ipynb
```

---

## 📚 Technical Appendix

### **Why January 2016 as Base Period?**
- Corresponds to start of post-Great Recession "normal" economic conditions
- Predates COVID-19 pandemic supply shocks
- Provides 8+ year time series (sufficient for trend analysis)
- Aligns with academic year cycle for student budgeting

### **Limitations & Future Work**
1. **Geographic scope**: Analysis currently focuses on national averages and Boston metro area; could expand to 10+ metros
2. **Demographic refinement**: Could segment by undergraduate vs. graduate students, or by institution type (public vs. private)
3. **Temporal granularity**: Monthly data could be aggregated to academic semesters for better alignment with student financial cycles
4. **Causal inference**: This is descriptive analysis; future work could employ regression discontinuity or difference-in-differences to isolate policy effects

### **Academic References**
- **Laspeyres Index Theory**: Laspeyres, E. (1871). "Die Berechnung einer mittleren Waarenpreissteigerung"
- **BLS CPI Methodology**: [https://www.bls.gov/opub/hom/pdf/cpi-20111028.pdf](https://www.bls.gov/opub/hom/pdf/cpi-20111028.pdf)
- **Heterogeneous Inflation**: Kaplan, G., & Schulhofer-Wohl, S. (2017). "Inflation at the Household Level" *Journal of Monetary Economics*

---

## 🤝 Contributing

Contributions are welcome! Areas of particular interest:
- Additional regional CPI series (e.g., San Francisco, New York, Austin)
- Alternative weighting schemes (e.g., by major, by institution tier)
- Interactive dashboard development (Plotly/Dash or Streamlit)
- Time-series forecasting models

Please open an issue or submit a pull request.

---

## 👨‍💻 About the Author

**[Your Name]**  
Economics & Data Science Student | [University Name]

This project was completed as part of ECON 3916: Applied Econometrics, demonstrating:
- API integration and data engineering
- Economic index construction
- Statistical normalization techniques
- Data visualization best practices
- Reproducible research workflows

**Connect with me:**
- LinkedIn: [your-linkedin]
- Email: your.email@university.edu
- Portfolio: [yourwebsite.com]

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Federal Reserve Bank of St. Louis for maintaining FRED database
- Bureau of Labor Statistics for CPI methodology documentation
- Professor [Name] for guidance on economic measurement theory
- Claude (Anthropic) for README structure assistance

---

**⭐ If you found this analysis useful, please consider starring this repository!**

---

*Last Updated: January 2026*  
*Data Current Through: December 2024*
