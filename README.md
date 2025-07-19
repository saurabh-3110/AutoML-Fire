
# AutoML-Fire: An Automated Machine-Learning Approach to Predict Forest Fires in India


This repository contains the official source code and resources for the research paper: "AutoML-Fire: Automated machine-learning approach to predict forest fires".
This project introduces a novel automated machine learning (AutoML) framework to predict daily forest fire counts across India, leveraging Bayesian optimization and explainable AI (XAI) techniques for enhanced accuracy and interpretability.
Read the full paper: Preprint submitted to Environmental Modelling & Software

Read the full paper: [AutoML-Fire: Automated machine-learning approach to predict forest fires](https://authors.elsevier.com/c/1lQrG4sKhEgvf~)


## About The Project

Predicting these events is challenging due to complex regional variations, data imbalances (fires are rare but devastating events), and the difficulty of manually selecting and tuning machine learning models.
AutoML-FIRE is a comprehensive framework designed to address these challenges. It provides a robust, automated, and scalable solution for predicting forest fire occurrences on a pan-India scale.
Key Contributions:
- 🔥 Pan-India Prediction: The first comprehensive study to predict forest fire counts across the diverse ecological and climatic zones of India.
- 🤖 Fully Automated Framework: Utilizes Bayesian Optimization to automatically select the best-performing machine learning model and fine-tune its hyperparameters, eliminating manual bias and extensive experimentation.
- 🗺️ Regional Specificity: Employs DBSCAN clustering to segment India into distinct fire-prone regions, allowing the model to capture unique local dynamics.
- 📊 Handles Data Imbalance: Implements the SMOGN (Synthetic Minority Over-sampling Technique for Regression with Gaussian Noise) algorithm to address the skewed nature of fire-occurrence data.
- 🧠 High Interpretability: Uses SHAP (SHapley Additive exPlanations) and Partial Dependence Plots (PDP) to provide clear insights into the key drivers of forest fires, making the model's predictions transparent and understandable.
- 📈 Superior Performance: Outperforms ten conventional benchmark algorithms, demonstrating higher accuracy and reliability in predicting forest fire counts.

## How to use the codes

### Data Preparation

#### Data pre-processing
The raw datasets for this study come from different sources (as listed in Table 1) and therefore have varying spatial resolutions, temporal frequencies, and file formats (e.g., NetCDF, TIFF, point data). This section explains how to handle this complexity. Its primary goal is to transform these diverse datasets into a single, unified data cube with a daily temporal resolution and a 0.25° x 0.25° spatial grid.

1. Forest count: Download the data from Forest Survey of India (FSI) website and run the _forest_fire_preprocessing.ipynb_ file according to the instruction preovided in the file.
2. ERA5 data (Cloudcover, Humidity, Windspeed): Download the data at daily termporal resolution from the Climate Data Store (CDS). The varibles should be saved in the following folder structure
```text
data_in_nc4/
├── humidity/
│   ├── 2004/
│   │   ├──2xxx0-Relative-Humidity-2m-09h_C3S-glob-agric_AgERA5_20030101_final-v1_area_subset.nc.
│   │   ├── xxx_20040102_xx.nc
│   │   └── ...
│   ├── 2005/
│   │   ├── ...
│   │   └── ...
│   └── ...
├──[VARIABLE]
│    ├── 2004/
│       ├── ...

```
Use _era5_preprocessing.ipynb_ to make single file of each variable containg all years data at daily temporal resolution.

3. NASA data (Soil moisture): Use the _download_using_links.ipynb_ to download the files form the links(.txt file) available through the website and save them as the structure same as above. Use gldas_preprocessing.ipynb to make single file for soilmoiture variable.

4. Forest cover: Download the annual files available at the source given in the paper and utilize _forestcover_preprocessing.ipynb_ to get a unified file at daily resolution.

5. BERKEARTH (tmin & tmax): Download the yearly files available from the source given in the paper and save them in a folder and utilize _berkearth_preprocessing.ipynb_ to get a unified csv file.

5. Rain: Download the data from the source which would be a zipped folder. Unzip it and utilize _rain_preprocessing.ipynb_ to get a unified file.

6. NOAA (NDVI): Download the files using the script _downloading_ndvi.ipynb_ and save the files according to the structure given above. Subsequently use the _ndvi_preprocessing.ipynb_ for make the unified file.

#### Combining data.

Use _combining_data.ipynb_ to comhine the data and also get the filtered data of only top 30% of grids. 

The _clustering.ipynb_ has the instruction on determing the clusters and create data files for each cluster. 

##### Making year lagged rain feature: 
Use _lagged_rain.ipynb_ for creating the lagged rain features for the top 30% grids file as well as the cluster individual files.

### Data Analysis 

This section focuses on understanding the key drivers of forest fire predictions. It details how to run the scripts for SHAP analysis and feature sensitivity analysis using Partial Dependence Plots (PDP).

#### SHAPley Analysis and feature importance
Utilize _shap_feature_importance.ipynb_ for the top 30% grids and cluster files for run the shap analysis and generate the corresponding plots.

#### Feature sensitivity  
Use _pdp_w_ice.ipynb_ and _only_pdp.ipynb_ to generate the required plots.

### Model Development

This section covers the core of the project: training the AutoML-FIRE framework using the prepared data for each identified region. It explains how to configure and execute the main training script that automates model selection and hyperparameter tuning.
 
#### SMOGN
Apply SMOGN to the main file and cluster files using _smogn.ipynb_ before the model development.

#### Model training
