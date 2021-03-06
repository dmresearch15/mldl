# Classification with H2O XGBoost in R #

XGBoost is an optimized distributed gradient boosting library designed to be highly efficient, flexible, and portable. XGBoost provides parallel tree boosting (also known as GBDT, GBM) that solves many data science problems in a fast and accurate way.

## Dataset ##
The dataset used in this example can be obtained from here:
 - [titanic_list.csv](https://raw.githubusercontent.com/Avkash/mldl/master/data/titanic_list.csv)

Note: Use "wget" and above links to pull the the data locally or use the URL above directly to load data into H2O.
  
## Get the R Source Code ##
  - [H2O XGBoost Classification with Titanic Dataset R Code](https://github.com/Avkash/mldl/blob/master/code/R/H2O_XGBoost_Classification_titanic.R)
  
## Classification with H2O XGBoost in R ##

###: Importing H2O Library
```python
library(h2o)
```

###: Initializing h2O
```python
h2o.init()
```

### : Getting H2O Cluster status
```python
h2o.clusterStatus()
```

###: Importing Dataset
```python
df = h2o.importFile("https://raw.githubusercontent.com/Avkash/mldl/master/data/titanic_list.csv")
```

###: Understanding Dataset
```python
h2o.describe(df)
```

###: Getting a list of columns in our dataset
```python
h2o.colnames(df)
```

###: Setting Response column
```python
response = "survived"
```

###: Setting Response column to factor so we can get unique values in it
```python
h2o.levels(h2o.asfactor(df['survived']))
```

###: Setting Response column to factor so we can build classification model
```python
df[response] = h2o.asfactor(df[response])
```

###: Verifying Response column as factor 
```python
h2o.describe(df[response])
```

###: spliting the dataset into train, test and validation  
```python
df_split = h2o.splitFrame(df, ratios = c(0.8,0.1))
train = df_split[[1]]
valid = df_split[[2]]
test = df_split[[3]]
print(nrow(train))
print(nrow(valid))
print(nrow(test))
```

###: Setting all columns/features into a local variable
```python
features =h2o.colnames(df)
```

###: Settings all features for model building
```python
features = setdiff(features, response)
print(features)
```

###: Ignoring list of features which are not required for model building
```python
ignore_list = c('name', 'ticket', 'home.dest')
features = setdiff(features, ignore_list)
print(features)
```

###: Using H2O XGBoost Library and setting proper Parameters and Training H2O XGBoost model 
```python
titanic_xgb = h2o.xgboost(ntrees = 100
                  , max_depth = 10
                  , learn_rate = 0.01
                  , sample_rate = 0.9
                  , col_sample_rate_per_tree = 0.9
                  , min_rows = 5
                  , seed = 4241
                  , score_tree_interval= 100,
                  x = features, 
                  y = response, 
                  training_frame = train, 
                  validation_frame = valid)
```

###: understanding the model metrics and various detials
```python
titanic_xgb
```

###: XGBoost model performance on validation data
```python
h2o.performance(titanic_xgb, valid = TRUE)
h2o.auc(titanic_xgb, valid = TRUE)
```

###: Generating Variable Importance Plot for the XGBoost Model
```python
h2o.varimp_plot(titanic_xgb)
```

###:  H2O XGBoost Scoring History
```python
h2o.score_history(titanic_xgb)
```

###: PERFORMING PREDICTIONS USING a TEST DATA SET with Auto ML Leader model
```python
h2o.predict(titanic_xgb, newdata =  test)
```

###: Getting AUC metrics from the test data using XGBoost Leader Model

```python
h2o.performance(titanic_xgb, newdata = test)
h2o.auc(titanic_xgb)
```
