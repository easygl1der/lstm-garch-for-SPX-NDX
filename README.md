# Hybrid LSTM-GARCH Volatility Forecasting Model

This directory contains the research paper, experimental code, and results for a comparative study on hybrid LSTM-GARCH frameworks for volatility forecasting in the NASDAQ-100 (NDX) and S&P 500 (SPX) markets.

## Overview

This project implements a hybrid deep learning framework that combines Long Short-Term Memory (LSTM) networks with GARCH-family econometric models to predict financial market volatility. The study demonstrates that:

1. **GARCH predictions significantly enhance LSTM performance**: Integrating one-step-ahead GARCH volatility forecasts as exogenous features consistently improves predictive accuracy across both markets.

2. **Implied volatility degrades performance**: Counter-intuitively, adding market implied volatility indices (VNX for NDX, VIX for SPX) consistently worsens model predictions, suggesting redundancy or noise within this framework.

## Directory Structure

```
model/
├── comparative_study.tex          # Main research paper (LaTeX source)
├── comparative_study.pdf          # Compiled PDF version
├── references.bib                 # Bibliography database
├── images/                        # Figures and plots used in the paper
│   ├── 2025_11_02_a3cad18d123fa484cda0g-3.jpg   # LSTM architecture diagram
│   ├── NDX-lstm-garch.png                        # NDX prediction results
│   └── SPX-lstm-garch.png                        # SPX prediction results
├── NDX/                           # NASDAQ-100 experiments
│   ├── code/
│   │   └── main.ipynb            # NDX model training and evaluation
│   ├── data/                     # Raw and processed NDX data
│   └── result/                   # NDX experimental results and models
└── SPX/                          # S&P 500 experiments
    ├── code/
    │   └── main.ipynb           # SPX model training and evaluation
    ├── data/                    # Raw and processed SPX data
    └── result/                  # SPX experimental results
```

## Research Methodology

### Data
- **NDX**: 5-minute intraday price data, VNX (NASDAQ-100 Volatility Index)
- **SPX**: 5-minute intraday price data, VIX (S&P 500 Volatility Index)
- **Target**: Daily Realized Volatility (RV) calculated from intraday returns

### Models Tested
1. **Baseline**: LSTM with historical RV only
2. **LSTM + IV**: LSTM with RV and implied volatility
3. **LSTM + GARCH variants**: LSTM with RV and GARCH-family predictions
   - GARCH(1,1)
   - GJR-GARCH (captures leverage effect)
   - TARCH/ZARCH (threshold asymmetry)
   - EGARCH (exponential GARCH)
   - AVGARCH (absolute value GARCH)
   - FIGARCH (fractional integration for long memory)
4. **LSTM + IV + GARCH**: Full hybrid with all three feature types

### Evaluation Metrics
- MSE, MAE, RMSE (absolute error metrics)
- HMSE, HMAE (heteroscedasticity-adjusted metrics)
- QLIKE (quasi-likelihood loss)

## How to Compile the Paper

### Prerequisites
You need a LaTeX distribution installed on your system:
- **Windows**: [MiKTeX](https://miktex.org/) or [TeX Live](https://www.tug.org/texlive/)
- **macOS**: [MacTeX](https://www.tug.org/mactex/)
- **Linux**: TeX Live (usually available via package manager)

### Compilation Steps

#### Method 1: Using Command Line

```bash
# Navigate to the model directory
cd TGI/model

# Compile the LaTeX document (run twice for proper references)
pdflatex comparative_study.tex
bibtex comparative_study
pdflatex comparative_study.tex
pdflatex comparative_study.tex
```

**Note**: The document uses BibTeX for bibliography management. The compilation sequence is necessary to:
1. First `pdflatex`: Process the document structure
2. `bibtex`: Generate bibliography entries
3. Second `pdflatex`: Insert bibliography references
4. Third `pdflatex`: Resolve all cross-references (tables, figures, citations)

#### Method 2: Using LaTeX Editors

Most LaTeX editors (TeXstudio, Overleaf, TeXworks, etc.) have a "Build" or "Compile" button that automatically handles the multi-pass compilation.

**In TeXstudio/TeXworks:**
1. Open `comparative_study.tex`
2. Select "Build & View" (F5 or F1 depending on editor)
3. The editor will automatically run `pdflatex` → `bibtex` → `pdflatex` → `pdflatex`

**In Overleaf:**
1. Upload all files to a new project
2. Click "Recompile"
3. The system automatically handles all compilation passes

### Required LaTeX Packages

The document uses the following packages (automatically installed by most modern LaTeX distributions):
- `amsmath`, `amsfonts`, `amssymb` - Mathematical typesetting
- `graphicx`, `adjustbox` - Image handling
- `caption`, `float` - Table and figure positioning
- `url`, `hyperref` - URL and hyperlink support

## Running the Experiments

### NDX Experiments
```bash
# Open the Jupyter notebook
jupyter notebook TGI/model/NDX/code/main.ipynb

# Or using JupyterLab
jupyter lab TGI/model/NDX/code/main.ipynb
```

The notebook includes:
- Data loading and preprocessing
- Realized Volatility calculation from 5-minute data
- GARCH model training (all 6 variants)
- LSTM model training with various feature combinations
- Model evaluation and comparison

### SPX Experiments
```bash
# Open the Jupyter notebook
jupyter notebook TGI/model/SPX/code/main.ipynb
```

Similar structure to NDX, but using S&P 500 data and VIX index.

## Key Results

### NASDAQ-100 (NDX)
- **Best models**: `RV + GARCH` (MSE: 0.000004), `RV + AVGARCH` (MSE: 0.000005)
- **Baseline**: `RV` only (MSE: 0.000004)
- **Worst**: `RV + VNX + GARCH` (MSE: 0.000074)

### S&P 500 (SPX)
- **Best models**: `RV + GJR-GARCH` (MSE: 0.000003), `RV + FIGARCH` (MSE: 0.000004)
- **Baseline**: `RV` only (MSE: 0.000003)
- **Adding VIX consistently degrades performance**

## Citation

If you use this code or methodology in your research, please cite:

```
Yue Yihua, Rong Jia, Lv Zimeng, Xiao Tongren, Li Ke (2025).
A Comparative Study of Hybrid LSTM Frameworks for Volatility Forecasting 
in the NASDAQ-100 and S&P 500 Markets.
```

## Code Repository

The complete code is available at: https://github.com/easygl1der/lstm-garch-for-SPX-NDX

## Requirements for Running Code

### Python Dependencies
```bash
pip install numpy pandas matplotlib torch arch yfinance scikit-learn jupyter
```

### Core Libraries
- `torch` - PyTorch for LSTM implementation
- `arch` - GARCH model estimation
- `pandas`, `numpy` - Data manipulation
- `matplotlib` - Visualization
- `scikit-learn` - Data preprocessing and metrics

## License

This research is provided for academic and educational purposes. Please refer to the LICENSE file for detailed terms.

## Contact

For questions or collaborations, please open an issue on the GitHub repository or contact the authors through the institutional affiliations listed in the paper.


