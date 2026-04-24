
 
### Data Preparation & Missing Data Handling
 

 .Missing timestamps were identified and aligned with a complete hour index because it can lead to incorrect lag/rolling calculations
.Duplicates timestamps were removed and select only hourly data
 .Applied linear interpolation and forward fill ( ffill ) to ensure past information used without future leakage
.Columns with all missing values were removed to avoid noise
.Column names and formats were standardized to ensure consistency across merged datasets(weather and economic data)
.Outliers were detected using a rolling mean (+3,-3) standard deviation approach and replaced with rolling mean values to maintain data continuity
.A binary feature is_spike is created to indicate anomaly points(1=spike,0=normal),it ensures that information about abnormal events is preserved even after smoothing

### Temporal Feature Engineering


.Lag features were created (1h,2h,3h,6h,12h,48h,168h) because past demands directly influence future demands
.Supply-related lag features (e.g:-generation,coal,solar) were created because demand is affected by supply condiyions
.Rolling mean (3h,24h,168h) is applied to capture the underlying trend
.Hour and Day of week is extracted to see daily and weekly  patterns
.Economic data(yearly based) is reshaped(converted data from wide->long->pivot format) and merged with the hourly dataset
.Select only relevant economic indicators(e.g GDP,energy use) and merge with hourly dataset using leftjoin
.Cyclic encoding is done to capture periodic trends
.Lag-based target variable is created using shift(-1)


### Train-Test Split Strategy


.Data was sorted chronologically to maintain time order
.Train-test split was performed based on time
.Training data includes past observations (<2024)
.Testing data includes future observations(>=2024)
.Features(X) and target(y) were separated after splitting


### Model & Evaluation

.Models used:Random forest,LightGBM,Linear regression,XGBoost to compare performances based on MAPE
.The final model was selected based on low MAPE value
.Preprocessing was applied before modeling to prepare data in suitable format for training
.Numerical features->Imputation + Scaling to handle missing values and maintain consistency
.Categorical features ->One-hot encoding to convert it into numerical columns
.MAPE is used as an evaluation metric
.Models comparison showed that XGBoost/LightGBM perform better than other models
.Used RandomizedSearchCV with TimeSeriesSplit to tune model hyperparameters while preventing data leakage





