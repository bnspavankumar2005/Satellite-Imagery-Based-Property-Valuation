# Satellite-Imagery-Based-Property-Valuation
A Real Estate Analytics firm aims to improve its valuation framework by developing a Multimodal Regression Pipeline that predicts property market value using both tabular data and satellite imagery.



##  Repository Structure

├── cleaned_train1.csv                # Cleaned and engineered training data

├── 23116023_predictions.xlsx         # Final predictions for test set

├── 23116023_report.pdf               # Full project report

├── README.md                       

├── eda_preprocess.ipynb              # Data cleaning, EDA, feature engineering

├── sat_img_data.ipynb                # Satellite image download pipeline

├── baseline_model.ipynb              # Tabular-only regression models

└── fusion_model.ipynb                # Multimodal (Tabular + Image) model


---

## Dataset
The base dataset is derived from the King County Housing Dataset and contains features such as:

bedrooms, bathrooms, sqft_living, sqft_lot, floors, view, waterfront, condition, grade, latitude, longitude, neighborhood statistics, and sale date.

Satellite images are fetched using latitude and longitude coordinates for every house.

---

##  Satellite Image Collection
Satellite images were downloaded using the Mapbox Static API.  
For each property, its geographic coordinates were used to retrieve a high-resolution (512×512) satellite image at zoom level 18. These images capture roads, vegetation, water bodies, and neighborhood structure. Each image was stored locally and mapped to its house ID.

---

##  Data Cleaning & Feature Engineering
Performed in eda_preprocess.ipynb:
- Missing values were handled
- Outliers were inspected
- Log(price) was used for stability
- Sale year, sale month, house age, and renovation indicators were created
- Zipcodes were encoded
- Cleaned data was saved to cleaned_train1.csv

EDA and preprocessing were done together to ensure the dataset was both clean and analytically sound.

---

##  Exploratory Data Analysis
EDA showed:
- Prices are right-skewed
- Waterfront and view strongly affect price
- Neighborhood living area influences value

Satellite images visually confirmed that:
- Houses near water, greenery, and open areas tend to be more expensive
- Dense urban layouts correspond to lower prices

---

##  Baseline Model (Tabular Only)
Several regression models were tested using only tabular data:
- Linear Regression
- Lasso
- Ridge
- Random Forest
- XGBoost


---

##  Visual Feature Extraction
A pretrained ResNet-50 CNN was used to extract visual features from satellite images. Each image was converted into a 2048-dimensional feature vector. PCA reduced this to 50 dimensions to keep the model efficient.

These features represent environmental characteristics like greenery, road layout, and neighborhood structure.

---

##  Multimodal Fusion Model
The final model combines:
- Tabular features (house attributes)
- Visual features (satellite image embeddings)

Both are concatenated and passed into an XGBoost regressor. This allows the model to learn that property value depends on both physical attributes and neighborhood environment.

---

##  Model Explainability
Two interpretability tools were used:

Grad-CAM highlights which regions of a satellite image influenced the CNN, such as roads, trees, or waterfronts.

SHAP explains which tabular and visual features most influenced each prediction, ensuring transparency.

---

## How to Run

1. Run sat_img_data.ipynb to download satellite images  
2. Run eda_preprocess.ipynb for cleaning and feature engineering  
3. Run baseline_model.ipynb for tabular model  
4. Run fusion_model.ipynb for multimodal training  
5. Final predictions are saved in 23116023_predictions.xlsx  


