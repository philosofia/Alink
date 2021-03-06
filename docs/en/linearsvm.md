## Description
Linear svm pipeline op.

## Parameters
| Name | Description | Type | Required？ | Default Value |
| --- | --- | --- | --- | --- |
| C | the penalty item parameter. | Double |  | 1.0 |
| optimMethod | optimization method | String |  | null |
| withIntercept | Whether has intercept or not, default is true | Boolean |  | true |
| maxIter | Maximum iterations, The default value is 100 | Integer |  | 100 |
| epsilon | Convergence tolerance for iterative algorithms (>= 0), The default value is 1.0e-06 | Double |  | 1.0E-6 |
| featureCols | Names of the feature columns used for training in the input table | String[] |  | null |
| labelCol | Name of the label column in the input table | String | ✓ |  |
| weightCol | Name of the column indicating weight | String |  | null |
| vectorCol | Name of a vector column | String |  | null |
| standardization | Whether standardize training data or not, default is true | Boolean |  | true |
| vectorCol | Name of a vector column | String |  | null |
| predictionCol | Column name of prediction. | String | ✓ |  |
| predictionDetailCol | Column name of prediction result, it will include detailed info. | String |  |  |
| reservedCols | Names of the columns to be retained in the output table | String[] |  | null |


## Script Example
#### Script
```
import numpy as np
import pandas as pd
data = np.array([
    [2, 1, 1],
    [3, 2, 1],
    [4, 3, 2],
    [2, 4, 1],
    [2, 2, 1],
    [4, 3, 2],
    [1, 2, 1],
    [5, 3, 2]])
df = pd.DataFrame({"f0": data[:, 0], 
                   "f1": data[:, 1],
                   "label": data[:, 2]})

batchData = dataframeToOperator(df, schemaStr='f0 int, f1 int, label int', op_type='batch')

colnames = ["f0","f1"]
svm = LinearSvm().setFeatureCols(colnames).setLabelCol("label").setPredictionCol("pred")
model = svm.fit(batchData)
model.transform(batchData).print()
```

#### Result
#### Result
f0 | f1 | label | pred 
---|----|-------|-----
2|1|1|1
3|2|1|1
4|3|2|2
2|4|1|1
2|2|1|1
4|3|2|2
1|2|1|1
5|3|2|2
