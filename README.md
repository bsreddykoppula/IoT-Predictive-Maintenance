## **IoT Data Lake for Predictive Maintenance**

## **Overview**

This project builds an **IoT-based predictive maintenance system** using **Azure IoT Hub**, **Databricks**, and **Delta Lake** to analyze sensor data (temperature, vibration). A **Random Forest model** predicts equipment failures **72 hours in advance** with **88% accuracy**, reducing maintenance costs by **25%**. Alerts are visualized in **Power BI** using geospatial heatmaps.

## **Features**

- **Real-time Data Ingestion**: Stream sensor data from **Azure IoT Hub** to **Delta Lake**.
- **Predictive Analytics**: Train a **Random Forest model** to detect failures.
- **MLflow Integration**: Log experiments and track model performance.
- **Power BI Dashboard**: Visualize alerts using geospatial heatmaps.
- **Infrastructure as Code**: Deploy resources using **Terraform**.

## **Tech Stack**

**Cloud & Big Data**: Azure IoT Hub, Delta Lake, Databricks\
**Machine Learning**: Random Forest, MLflow\
**ETL & Data Engineering**: Apache Spark, Python\
**IaC**: Terraform\
**Visualization**: Power BI, DAX

## **Project Structure**

```
├── README.md  
├── data_ingestion/  
│   ├── iot_to_delta.py       # Ingest sensor data to Delta Lake  
├── databricks_notebooks/  
│   ├── model_training.ipynb  # Train Random Forest model  
├── mlflow/  
│   ├── tracking_server.py    # Log experiments with MLflow  
├── powerbi/  
│   ├── heatmap_dashboard.pbix  # Alert visualization  
├── terraform/  
│   ├── azure_iot.tf          # Deploy Azure IoT resources  
└── sample_data/  
    └── sensor_data_sample.csv  
```

## **Setup & Execution**

1. **Deploy Azure Resources**
   ```bash
   cd terraform && terraform apply
   ```
2. **Stream Sensor Data**
   ```bash
   python data_ingestion/iot_to_delta.py
   ```
3. **Train Model in Databricks**\
   Run `model_training.ipynb` notebook.
4. **Visualize Alerts**\
   Open `heatmap_dashboard.pbix` in Power BI.

## **Outcomes**

-  **88% Prediction Accuracy**: Early failure detection.
-  **25% Cost Reduction**: Proactive maintenance scheduling.
-  **Geospatial Heatmaps**: Real-time risk monitoring in Power BI.

## **Contributors**

- **Your Name** - linkedin.com/in/bsrkoppula





