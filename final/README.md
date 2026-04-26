# Predicting Adolescent Fertility Rates

**ECON 3916 — Final Project**

Predicting country-level adolescent fertility rates (births per 1,000 women ages 15–19) using socioeconomic, demographic, and health indicators from the World Bank World Development Indicators.

**Model:** Random Forest Regressor | **CV R²:** 0.9575 | **Test R²:** 0.9601

---

## Repository Structure

```
fertility-project/
├── app.py                     # Streamlit web application
├── model.pkl                  # Trained Random Forest model
├── requirements.txt           # Python dependencies
├── 3916-final-project.ipynb   # Main analysis notebook
└── README.md                  # This file
```

---

## 1. Environment Setup

**Prerequisites:** Python 3.9 or higher and pip or Anaconda.

**Install dependencies:**

```bash
pip install -r requirements.txt
```

Or with Anaconda:

```bash
conda create -n fertility_env python=3.9
conda activate fertility_env
pip install -r requirements.txt
```

---

## 2. Data Acquisition

The dataset must be downloaded manually from the World Bank DataBank — it is not included in this repository.

**Steps:**

1. Go to https://databank.worldbank.org/source/world-development-indicators
2. Under **Series**, search and add the following 20 indicators:

| Series Name | Code |
|---|---|
| Adolescent fertility rate (births per 1,000 women ages 15-19) | SP.ADO.TFRT |
| Current health expenditure (% of GDP) | SH.XPD.CHEX.GD.ZS |
| Fertility rate, total (births per woman) | SP.DYN.TFRT.IN |
| GDP per capita (constant 2015 US$) | NY.GDP.PCAP.KD |
| Government expenditure on education, total (% of GDP) | SE.XPD.TOTL.GD.ZS |
| Immunization, measles (% of children ages 12-23 months) | SH.IMM.MEAS |
| Labor force participation rate, female (% ages 15-64) | SL.TLF.ACTI.FE.ZS |
| Life expectancy at birth, female (years) | SP.DYN.LE00.FE.IN |
| Life expectancy at birth, total (years) | SP.DYN.LE00.IN |
| Maternal mortality ratio (per 100,000 live births) | SH.STA.MMRT |
| Mortality rate, under-5 (per 1,000 live births) | SH.DYN.MORT |
| Population growth (annual %) | SP.POP.GROW |
| Population, total | SP.POP.TOTL |
| Prevalence of HIV, total (% of population ages 15-49) | SH.DYN.AIDS.ZS |
| Primary completion rate, total (% of relevant age group) | SE.PRM.CMPT.ZS |
| School enrollment, primary (% gross) | SE.PRM.ENRR |
| School enrollment, primary and secondary, gender parity index (GPI) | SE.ENR.PRSC.FM.ZS |
| School enrollment, secondary (% gross) | SE.SEC.ENRR |
| School enrollment, secondary, female (% gross) | SE.SEC.ENRR.FE |
| Urban population (% of total population) | SP.URB.TOTL.IN.ZS |

3. Under **Country** → select **All Countries**
4. Under **Time** → select **2006 to 2023**
5. Click **Download → CSV**
6. Rename the file to `world_bank_data.csv`

---

## 3. Running the Notebook

**Option A — Google Colab (recommended):**

1. Upload `3916-final-project.ipynb` to Google Colab
2. Upload `world_bank_data.csv` to Google Drive
3. Mount Google Drive at the top of the notebook:

```python
from google.colab import drive
drive.mount('/content/drive')
```

4. Update the data loading cell to:

```python
df = pd.read_csv('/content/drive/MyDrive/world_bank_data.csv')
```

5. Run all cells in order via **Runtime → Run All**

**Option B — Local Jupyter:**

```bash
pip install jupyter
jupyter notebook 3916-final-project.ipynb
```

Place `world_bank_data.csv` in the same folder as the notebook, then run all cells in order.

---

## 4. Launching the Streamlit App Locally

```bash
# Step 1 — Navigate to the project folder
cd path/to/fertility-project

# Step 2 — Run the app
streamlit run app.py
```

The app will open automatically at `http://localhost:8501`.

Use the sidebar sliders to adjust country indicators and see the predicted adolescent fertility rate update in real time.

---

## 5. Reproducing the Model

The trained model is saved as `model.pkl` and is loaded automatically by `app.py`. To retrain from scratch, run all cells in the notebook — the final cells will save a new `model.pkl`:

```python
import joblib
joblib.dump(model_2, 'model.pkl')
```

---

## Data Source

World Bank World Development Indicators
URL: https://databank.worldbank.org/source/world-development-indicators
Access date: April 15, 2026
