# H2O model details from R, Python and Scala API # 

H2O model are accessible in between any of the environment as long as you have proper Id available. Once you know the model Id (which u can get using h2o.ls() command in R and Python) you can pass model ID as below in any of the API:

## Getting models in R based on model id ##
```
model_in_r = h2o.getModel('model_id')
model_in_r
```
## Getting models in python based on model id ##
```
model_in_python = h2o.get_model('model_id')
model_in_python
```

## Getting models in Scala based on model id ##
```
[WIP]
```

## Model details ##
 - [R](https://github.com/Avkash/mldl/blob/master/orgs/h2o/guide/algo/model/h2o_model_details_r.md)
 - [Python](https://github.com/Avkash/mldl/blob/master/orgs/h2o/guide/algo/model/h2o_model_python.md)
 - [Scala](https://github.com/Avkash/mldl/blob/master/orgs/h2o/guide/algo/model/h2o_model_details_scala.md)
