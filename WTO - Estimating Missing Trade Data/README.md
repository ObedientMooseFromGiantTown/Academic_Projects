# Estimating Missing Trade Data

## Overview  

This project develops and tests methods for estimating missing international trade flows, working with the World Trade Organization and large scale bilateral trade data. The aim is to improve the completeness and quality of trade statistics so that researchers and policymakers can rely on more accurate views of global trade patterns.   

## Project goals  

- Identify and understand gaps in WTO and partner trade datasets.   
- Review statistical and machine learning approaches for imputing missing values in economic data.   
- Implement and compare several estimation strategies for missing trade flows, including theory driven and data driven methods. 
- Build a reusable pipeline in Python or R for data cleaning, imputation and evaluation that can be applied to future datasets.   
- Design a verification and data quality module that cross checks results against external sources and flags inconsistencies.  

## Data  

The project uses bilateral trade data drawn from several main sources.   

- **WTO Integrated Database (IDB)** for detailed tariff and trade statistics.  
- **UN Comtrade** for product level bilateral trade flows.  
- **Trade Data Monitor (TDM)** for more recent years where WTO or Comtrade coverage is limited.  
- **Consolidated Tariff Schedules (CTS)** and other WTO notifications for supporting tariff and policy information.  

Multiple reference datasets support these flows.  

- Harmonised System (HS) product classifications and concordance tables across HS versions.  
- MTN product group mappings for more aggregated analysis.  
- Country name and country group reference files for consistent identifiers.  
- Country level economic indicators such as GDP, population and sectoral value added from the World Bank.  
- Bilateral sanctions and preferential trade agreement information from WTO and the Global Sanctions Data Base.  

The cleaned datasets cover hundreds of millions of import and export records between nearly 180 countries over 1996 to 2024. They include fully processed imports and exports, mirror statistics datasets that reconcile reported flows in both directions and country pair metadata that combines geography, preferences, sanctions and macro indicators. 

## Methods  

The project combines classic tools from trade economics with modern machine learning and network based methods. 

### Data preprocessing and mirror statistics  

- Filter raw imports and exports to genuine country to country flows and standardise country identifiers.  
- Harmonise HS codes across versions using concordance tables and build both detailed and aggregated product categories.  
- Apply basic mirror statistics so that export reports from one country can fill import gaps in its partners, with imports preferred where both sides report. This step boosts coverage before any modelling and isolates genuinely missing flows.  

### Imputation and modelling approaches  

The following families of models are implemented and compared.  

- **Mirror based estimation**  
  - Use partner reported flows directly, after cleaning and basic CIF versus FOB adjustments where needed.  
  - Focus on transparent rules that are easy to audit and explain.  

- **Gravity style models with clustering**  
  - Use GDP, distance, sanctions, trade agreements and other standard gravity variables to predict bilateral trade.  
  - Cluster country pairs with similar characteristics and estimate separate models inside each cluster, which helps capture heterogeneity that pooled models miss.  

- **Random forest and related tree ensembles**  
  - Train non parametric models on a rich feature set that includes economic variables, product information and network measures.  
  - Use methods such as MissForest for iterative imputation of missing values, which is well suited to mixed type data.  

- **Spatio temporal graph convolutional networks (STGCN)**  
  - Represent the world trading system as a network of countries connected by trade links that evolve over time.  
  - Learn node and edge representations through graph convolutions and combine them with temporal convolutions to model trade dynamics across years.  

Baseline methods such as mean imputation and simple forward or backward filling are also implemented for comparison, along with standard metrics such as RMSE, MAE and R² on held out data with artificially removed values.   

### Verification and data quality  

The framework includes checks that compare imputed values to external sources, test sensitivity to modelling choices and flag suspicious patterns such as negative trade values, sudden spikes or sharp breaks that do not match known economic events.   

