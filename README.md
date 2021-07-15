# MLFlow

invoke mlflow run MLFlow -P alpha=0.42. After running this command, MLflow runs your training code in a new Conda environment with the dependencies specified in conda.yaml.


the call to mlflow.sklearn.log_model produces two files in /Users/mlflow/mlflow-prototype/mlruns/0/7c1a0d5c42844dcdb8f5191146925174/artifacts/model. The first file, MLmodel, is a metadata file that tells MLflow how to load the model. The second file, model.pkl, is a serialized version of the linear regression model that you trained.
![images/mlrun.png]()

mlflow models serve -m /Users/mlflow/mlflow-prototype/mlruns/0/7c1a0d5c42844dcdb8f5191146925174/artifacts/model -p 1373

Once you have deployed the server, you can pass it some sample data and see the predictions. The following example uses curl to send a JSON-serialized pandas DataFrame with the split orientation to the model server.

curl -X POST -H "Content-Type:application/json; format=pandas-split" --data '{"columns":["alcohol", "chlorides", "citric acid", "density", "fixed acidity", "free sulfur dioxide", "pH", "residual sugar", "sulphates", "total sulfur dioxide", "volatile acidity"],"data":[[12.8, 0.029, 0.48, 0.98, 6.2, 29, 3.33, 1.2, 0.39, 75, 0.66]]}' http://127.0.0.1:1373/invocations
