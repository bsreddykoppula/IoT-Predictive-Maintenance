# data_ingestion/iot_to_delta.py
from azure.iot.hub import IoTHubRegistryManager
from delta.tables import DeltaTable
from pyspark.sql import SparkSession

# Connect to Azure IoT Hub
registry_manager = IoTHubRegistryManager("YOUR_CONN_STRING")

# Read device telemetry
def get_device_data(device_id):
    return registry_manager.get_device_telemetry(device_id)

device_data = get_device_data("device_01")

# Initialize Spark Session
spark = SparkSession.builder.appName("IoTDataIngestion").getOrCreate()

df = spark.createDataFrame(device_data)
df.write.format("delta").mode("append").save("abfss://delta-lake@sensorstorage.dfs.core.windows.net/sensor_data")

# databricks_notebooks/model_training.ipynb
from sklearn.ensemble import RandomForestClassifier
import mlflow
from sklearn.metrics import accuracy_score

# Load data from Delta Lake
df = spark.read.format("delta").load("abfss://delta-lake@sensorstorage.dfs.core.windows.net/sensor_data")
train, test = df.randomSplit([0.8, 0.2])

# Train model
with mlflow.start_run():
    model = RandomForestClassifier().fit(train.toPandas(), train.label)
    predictions = model.predict(test.toPandas())
    mlflow.log_metric("accuracy", accuracy_score(test.label, predictions))
    mlflow.sklearn.log_model(model, "random_forest_model")

# terraform/azure_iot.tf
resource "azurerm_iothub" "sensor_hub" {
  name                = "predictive-maintenance-iothub"
  resource_group_name = azurerm_resource_group.main.name
  sku {
    name     = "S1"
    capacity = 1
  }
}

# Setup Instructions
cd terraform && terraform apply
python data_ingestion/iot_to_delta.py
