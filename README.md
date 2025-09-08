# Geographically Weighted Panel Regression (GWPR) Analysis

## 📊 Overview
This repository contains R code for conducting Geographically Weighted Panel Regression (GWPR) analysis on Indonesia's Human Development Index (IPM - Indeks Pembangunan Manusia) data. The analysis explores spatial and temporal variations in factors affecting human development across Indonesian provinces from 2017-2022.

## 🎯 Research Objectives
- Analyze factors influencing Human Development Index across Indonesian provinces
- Examine spatial heterogeneity in the relationships between variables
- Compare different panel regression models (Pooled, Fixed Effects, Random Effects)
- Apply geographically weighted regression to capture local spatial variations

## 📈 Variables Analyzed

### Dependent Variable
- **IPM**: Human Development Index (Indeks Pembangunan Manusia)

### Independent Variables
- **TPT**: Open Unemployment Rate (Tingkat Pengangguran Terbuka)
- **PP**: Per Capita Expenditure (Pengeluaran Perkapita)
- **JPM**: Population Count (Jumlah Penduduk Miskin)
- **IKK**: Construction Cost Index (Indeks Kemahalan Konstruksi)
- **APS**: School Participation Rate (Angka Partisipasi Sekolah)
- **RRLS**: Average Years of Schooling (Rata-rata Lama Sekolah)
- **PSAM**: Drinking Water Supply (Persediaan Sumber Air Minum)
- **GR**: Gini Ratio

## 📋 Prerequisites

### Required R Packages
```r
# Classical assumption testing
library(lmtest)
library(MASS)
library(car)
library(plm)
library(skedastic)
library(lawstat)
library(tseries)
library(olsrr)

# Spatial analysis
library(GWmodel)
library(sp)
library(spdep)
library(spgwr)

# Mapping and visualization
library(plotly)
library(sf)
library(ggplot2)
library(ggpubr)
library(rgdal)
library(corrplot)

# Data manipulation
library(tidyr)
library(dplyr)
library(readxl)
```

## 📁 Data Requirements

### Input Files
1. **Data_Panel_IPMIDN.xlsx** - Panel data for mapping
2. **Data_Panel_IPM_Indonesia.xlsx** - Main panel dataset
3. **Data_GWR_PANEL_IPM.xlsx** - Transformed data for GWR analysis
4. **BATAS PROVINSI DESEMBER 2019 DUKCAPIL.shp** - Indonesia provinces shapefile

### Data Structure
- **Time Period**: 2017-2022 (6 years)
- **Spatial Units**: 34 Indonesian provinces
- **Total Observations**: 204 (34 provinces × 6 years)

## 🔧 Analysis Workflow

### 1. Data Exploration
- Summary statistics
- Temporal variation analysis
- Inter-individual variation analysis
- Correlation matrix visualization
- Spatial mapping of variables across years

### 2. Classical Panel Regression
- **Pooled Least Squares (PLS)**
- **Fixed Effects Model (FEM)**
- **Random Effects Model (REM)**

### 3. Model Selection Tests
- **Chow Test**: Compare OLS vs Fixed Effects
- **Hausman Test**: Compare Fixed Effects vs Random Effects

### 4. Classical Assumptions Testing
- Normality test (Jarque-Bera)
- Autocorrelation test (Runs test)
- Spatial heterogeneity test (Breusch-Pagan)
- Multicollinearity test (VIF)

### 5. Geographically Weighted Panel Regression
- Bandwidth selection with different kernels:
  - Adaptive Gaussian
  - Adaptive Bisquare
  - Adaptive Exponential
- Parameter estimation for each location
- Significance testing
- Model goodness-of-fit assessment

### 6. Spatial Visualization
- Parameter significance mapping
- Local R-squared visualization
- Variable-specific significance patterns

## 📊 Key Features

### Spatial Analysis Capabilities
- **Adaptive bandwidth selection** using cross-validation
- **Multiple kernel functions** for weight calculation
- **Local parameter estimation** for each province
- **Spatial autocorrelation testing**

### Visualization Features
- **Choropleth maps** for each variable across time
- **Significance mapping** with color coding
- **Correlation heatmaps**
- **Time series plots**

## 🚀 Usage

1. **Set Working Directory**
```r
setwd("your/path/to/data")
```

2. **Load Required Libraries**
```r
source("load_libraries.R")
```

3. **Import Data**
```r
Data.mapping <- read_excel("Data_Panel_IPMIDN.xlsx")
Data.Panel <- read_excel("Data_Panel_IPM_Indonesia.xlsx")
within.trans <- read_excel("Data_GWR_PANEL_IPM.xlsx")
```

4. **Run Analysis**
```r
source("GEOGRAPHICALLY WEIGHTED PANEL REGRESSION.R")
```

## 📈 Output Files

### Generated Results
- `Hasil_Parameter_GWPR.csv` - Local parameter estimates
- `Hasil_PValue_GWPR.csv` - P-values for significance testing
- `Hasil_Rlocal_GWPR.csv` - Local R-squared values
- `Bandwidth_Lokasi.csv` - Location-specific bandwidths
- `Hasil_Jarak_Euclidean.csv` - Euclidean distance matrix
- `Hasil_Pembobot.csv` - Weight matrix
- `hasil_thitung.csv` - T-statistics

### Visualizations
- Spatial distribution maps for all variables (2017-2022)
- Significance maps for each explanatory variable
- Combined significance visualization

## 🔍 Key Findings Framework

The analysis framework allows for:
- **Spatial heterogeneity detection** in variable relationships
- **Local significance assessment** of explanatory variables
- **Regional policy implications** based on local parameter estimates
- **Temporal stability analysis** of spatial patterns

## 📝 Model Specifications

### Panel Regression Models
```
IPM ~ TPT + PP + JPM + IKK + APS + RRLS + PSAM + GR
```

### GWPR Model
```
IPM_i = β₀(uᵢ,vᵢ) + Σⱼ βⱼ(uᵢ,vᵢ)Xⱼᵢ + εᵢ
```
where (uᵢ,vᵢ) represents the geographic coordinates of location i.

## 🛠️ Technical Notes

### Bandwidth Selection
- Uses cross-validation approach
- Adaptive bandwidth based on data density
- Optimizes for minimum CV score

### Weight Function (Bisquare Kernel)
```
w_ij = (1 - (d_ij/b_i)²)² if d_ij < b_i
w_ij = 0 if d_ij ≥ b_i
```

## 📚 References

This analysis methodology is based on established spatial econometrics and geographically weighted regression literature, particularly suitable for analyzing spatially heterogeneous relationships in panel data contexts.

## 🤝 Contributing

Feel free to contribute by:
- Reporting bugs
- Suggesting improvements
- Adding new features
- Enhancing documentation

## 📄 License

This project is available for academic and research purposes. Please cite appropriately when using this code.

---

**Note**: Ensure all required shapefiles and data files are properly placed in the working directory before running the analysis.
