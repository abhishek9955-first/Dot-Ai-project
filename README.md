### EDA
.Generated correlation table with respect to demand to see linear relation of other columns in power dataframe

.Time series plot was generated to analyze demand trends over time

.Distribution of demand was examined using histogram,showing a right skewed distribution

.Boxplot analysis was performed to identify outliers in demand 

.Heatmap was generated to analyze relationships between features


### DATA CLEANING & FEATURE ENGINEERING

.The datetime column was converted into proper datetime format using pd.to_datetime() for time-based operations & Duplicates timestamps were removed and select only hourly data

.The datetime column was set as the index of the dataset & A complete hourly time range was generated using pd.date_range() to check for missing hours to consider missing hourly stamps which were later imputed.

.Missing values in demand_mw & generation_mw were filled using ffill() & Missing values in the remark column were replaced with the label "Normal"

.Power and weather  were merge using time index

.Used forward fill on numerical missing values, so that there is no data leakage.

. took transpose of economic table, made years into rows and the events to columns.

. Selected only a few relevant economic indicators, which affect much of electricity demand.

.Lag features were created using time shifts of 1h,2h,3h,6h,12h,24h,48h to capture short-term and long-term electricity demand

.Supply-related columns were selected and apply lag features to see each generation_demand

.Rolling mean along with rolling standard deviation were created to capture short-term,daily and weekly trends 

.Target variable was created using shift(-1) 

### Pipeline

.Split all data into before 2024 for training and after 2024 for testing.

.Defined feature engineering fuction which includes features like:

 .lag columns, rolling mean of 3,24,7*24 hours of the previous data,
  
 .rolling standard deviation of last 24 hours data.
 
 .Time-based features were extracted and cyclic encoding using sine and cosine transformations was applied

.Feature(X) and target(y) were separated by removing the target and original demand column

.Training and testing datasets were filtered to ensure valid rows and checked to avoid empty datasets

.Outliers in the target variable were handled using IQR-based clipping

->Preprocessing setup

.Missing values in numerical features were handled using median imputation and standard scaling

.Categorical features were processed using one-hot encoding

.A complete machine learning pipeline was costructed by combining preprocessing and model steps

.Evaluation metric(MAPE) was created



### Model & Evaluation

.Models used:Random forest,LightGBM,Linear regression,XGBoost to compare performances based on MAPE

.The final model was selected based on low MAPE value

.Preprocessing was applied before modeling to prepare data in suitable format for training

.Numerical features->Imputation + Scaling (standard scaler) to handle missing values and maintain consistency

.Categorical features ->One-hot encoding to convert it into numerical columns

.MAPE is used as the evaluation metric

.Models comparison showed that XGBoost/LightGBM perform better than other models

.Used RandomizedSearchCV with TimeSeriesSplit to tune model hyperparameters while preventing data leakage





