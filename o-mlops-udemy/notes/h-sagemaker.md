## Sagemaker

* Set up Sagemaker and Sagemaker Studio
* Create Jupyterlab Space


### AWS Feature Engineering

* Upload all data to S3
* Follow the steps in Data Wrangler > Data Flow
* Create an Entire flow using the GUI.
* can add custom scripts as well.

### Custom Transformation Code

```sh
import time
import pandas as pd
from statsmodels.stats.outliers_influence import variance_inflation_factor
from statsmodels.tools.tools import add_constant
import numpy as np

# Add two new indicators
df["no_previous_contact"] = (df["pdays"] == 999).astype("int8")
df["not_working"] = df["job"].isin(["student", "retired", "unemployed"]).astype("int8")
df['pdays']=df['pdays'].astype(np.float64) #cast pdays column type to double precision

# Add unique ID and event time for features store
df['FS_ID'] = df.index + 1000
current_time_sec = int(round(time.time()))
df['FS_time'] = pd.Series([current_time_sec]*len(df), dtype="float64") 

# compute the vif and drop columns greater than 1.2 threshold
def compute_vif(df, threshold):
    names=['age','euribor3m','campaign','not_working', 'no_previous_contact']
    considered_features= [name for name in names if name in df.columns]
    subset=df[considered_features]  
    subset=subset.dropna()  
    subset['intercept'] = 1
    vif = pd.DataFrame()
    vif["Variable"] = subset.columns
    vif["VIF"] = [variance_inflation_factor(subset.values, i) for i in range(subset.shape[1])]
    vif = vif[vif['Variable']!='intercept']
    vif=vif.sort_values('VIF', ascending=False)
    print(vif)       
    drop_clm=vif.index[vif.VIF.gt(threshold)].tolist()
    drop_clm_names=vif.loc[drop_clm]['Variable'].tolist()
    df.drop(drop_clm_names, axis=1, inplace=True)
    return df
df=compute_vif(df, 1.2)


```


### Using Sagemaker SDK and Our Feat Engg Script
* Makes use of Containers
* Need to pass our script as argument inside the relevant code blocks of the Notebook
```sh
import pandas as pd
import numpy as np
import argparse
import os
from sklearn.preprocessing import OrdinalEncoder

def _parse_args():

    parser = argparse.ArgumentParser()

    # Data, model, and output directories
    # model_dir is always passed in from SageMaker. By default this is a S3 path under the default bucket.
    parser.add_argument('--filepath', type=str, default='/opt/ml/processing/input/')
    parser.add_argument('--filename', type=str, default='bank-additional-full.csv')
    parser.add_argument('--outputpath', type=str, default='/opt/ml/processing/output/')
    parser.add_argument('--categorical_features', type=str, default='y, job, marital, education, default, housing, loan, contact, month, day_of_week, poutcome')

    return parser.parse_known_args()

if __name__=="__main__":
    args, _ = _parse_args()
    df = pd.read_csv(os.path.join(args.filepath, args.filename))
    df = df.replace(regex=r'\.', value='_')
    df = df.replace(regex=r'\_$', value='')
    # Add two new indicators
    df["no_previous_contact"] = (df["pdays"] == 999).astype(int)
    df["not_working"] = df["job"].isin(["student", "retired", "unemployed"]).astype(int)
    df = df.drop(['duration', 'emp.var.rate', 'cons.price.idx', 'cons.conf.idx', 'euribor3m', 'nr.employed'], axis=1)
    # Encode the categorical features
    df = pd.get_dummies(df)
    # Train, test, validation split
    train_data, validation_data, test_data = np.split(df.sample(frac=1, random_state=42), [int(0.7 * len(df)), int(0.9 * len(df))])   # Randomly sort the data then split out first 70%, second 20%, and last 10%
    # Local store
    pd.concat([train_data['y_yes'], train_data.drop(['y_yes','y_no'], axis=1)], axis=1).to_csv(os.path.join(args.outputpath, 'train/train_script.csv'), index=False, header=False)
    pd.concat([validation_data['y_yes'], validation_data.drop(['y_yes','y_no'], axis=1)], axis=1).to_csv(os.path.join(args.outputpath, 'validation/validation_script.csv'), index=False, header=False)
    test_data['y_yes'].to_csv(os.path.join(args.outputpath, 'test/test_script_y.csv'), index=False, header=False)
    test_data.drop(['y_yes','y_no'], axis=1).to_csv(os.path.join(args.outputpath, 'test/test_script_x.csv'), index=False, header=False)
    print("## Processing completed. Exiting.")

```

### Refer to the notebook in the sagemaker codes for reference regarding Model Training, Tuning and Deployment..

### Create Custom Models
* Tensorflow
* Pytorch
* Decision Trees
* Custom Containers. (make sure to create the sagemaker role and add the policies from the codes folder..)