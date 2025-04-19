# Housing Inflation Analysis

This repository provides scripts to analyze and visualize U.S. home‑price inflation and expectations. It includes:

- **Data ingestion** from FRBNY's Home Price Expectations survey and Zillow’s Single‑Family Home Value Index (ZHVI)
- **Inflation calculations** (12‑ and 36‑month realized inflation) and lagged series
- **Expectation series** (one‑year‑ahead and three‑year‑ahead predictions)
- **Merged dataset** extending forecasts into the future
- **Plots**:
  - Existing home sales vs. 10‑year Treasury yield (inverted) with recession shading
  - Realized vs. one‑year‑ahead home‑price inflation
  - Realized vs. three‑year‑ahead home‑price inflation
  - Correlograms of cross‑correlations between inflation and expectations

## Requirements

- Python 3.7+
- pandas
- numpy
- matplotlib
- seaborn
- statsmodels

Install dependencies via:
```bash
pip install pandas numpy matplotlib seaborn statsmodels
```

## Data

1. Download FRBNY survey from:
   `FRBNY-SCE-Data (1).xlsx` (`Home price expectations` sheet)
2. Download Zillow ZHVI CSV for SFR/condo tier 0.33–0.67:
   `Metro_zhvi_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv`
3. Place these under `data/`.

## Usage

### 1. Merge and preprocess data
Run `scripts/plot_sales_yield.py` to:
- Read and merge FRBNY expectations with Zillow home‑price series
- Compute realized inflation (`infl`, `infl_36`) and lagged values
- Plot sales vs. inverted 10‑yr yield with recession shading

```bash
python scripts/plot_sales_yield.py \
  --frbny data/FRBNY-SCE-Data.xlsx \
  --zillow data/Metro_zhvi_uc_sfrcondo_*.csv \
  --output output/
```

### 2. Plot expectations vs. reality
Run `scripts/plot_expectations.py` to:
- Plot realized 12‑month inflation vs. one‑year‑ahead expectations
- Plot realized 36‑month inflation vs. three‑year‑ahead expectations

```bash
python scripts/plot_expectations.py \
  --input merged_df.csv \
  --output output/
```

### 3. Correlogram analysis
Run `scripts/plot_correlogram.py` to:
- Compute cross‑correlations (24‑month max lag) between realized inflation and expectations
- Generate correlogram and reversed‑series correlogram

```bash
python scripts/plot_correlogram.py \
  --input merged_df.csv \
  --output output/
```

## Recessions
Plotted recessions (NBER):
- Mar 2001 – Nov 2001
- Dec 2007 – Jun 2009
- Feb 2020 – Apr 2020

## License
Released under the MIT License.

