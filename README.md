<a name="readme-top"></a>

[![LinkedIn][linkedin-shield]][https://www.linkedin.com/in/alexander-ifenaike/]


# MLOps Pipelines: Architecting solutions to forecasting reservation cancellation tendencies in hotels

![Pipelines](images/ml_pipelines.png)

In this repository, I describe a project that illustrates a data processing and machine learning (ML) workflow incorporating **Apache Airflow** and **MLflow** for a fully customizable and ready for a production environment.

Here's a brief explanation of the steps involved: 
* **Raw Data:** The starting point is raw data, which may come from various sources.
* **Batch:** There is also a batch data source which might be processed periodically.
* **Preprocessing:** Raw data is first preprocessed to clean and normalize it, making it suitable for ML algorithms. This may include handling missing values, normalizing ranges, etc.
* **Feature Engineering:** The preprocessed data undergoes feature engineering where new features are created or existing ones are transformed to improve the ML model's performance.
* **Training:** The processed data is then fed into the training phase where an ML model is taught using historical data.
* **Validation:** After the model has been trained, it goes through validation to evaluate its performance, usually against a separate dataset not seen by the model during training.
* **Model Registry:** Successfully validated models are stored in a model registry, which acts as a repository for trained models.
* **Inference Pipeline:** For new data (which can also come in batches), an inference pipeline is used where the model applies what it has learned to make predictions.
* **Predictions:** The end result is predictions based on the input data through the model.

## Code organization

```sh
.
├── README.md
├── airflow
│   ├── dags
│   │   ├── inference_pipeline.py
│   │   └── training_pipeline.py
├── artifacts
├── data
│   ├── features_store
│   ├── preprocessed
│   ├── hotel_bookings.parquet
│   └── sample_for_inference.parquet
├── mlflow
├── notebooks
│   ├── 0_exploratory_data_analysis.ipynb
│   └── 1_preprocessed_data_check.ipynb
├── requirements.txt
└── steps
    ├── condition_step.py
    ├── config.py
    ├── feature_engineering_step.py
    ├── inference_step.py
    ├── preprocess_step.py
    ├── train_step.py
    └── utils
        ├── _artifact.py
        └── data_classes.py
```

The repository is structured as follows:

* **Data Exploratory Analysis (EDA)** is performed on **notebooks**,
* Each stage of the Machine Learning process (**Preprocessing**, **Training**, **Inference**, etc...) is defined as a module designed to be implemented into a pipeline. They are all located in the *steps/* folder.
* **Airflow** and **Mlflow** are deployed locally within this repository.
* In the *data* folder is located the original dataset that was provided for this assignement, in addition of a sample for batch prediction. *data/features_store* and *data/preprocessed* are directories to store the data once processed by some stages of the pipelines, such as **preprocessing** or **features_engineering** steps.
* The same idea for *artifacts* that contains **encoders** generated during the **features_engineering** step.


<p align="right">(<a href="#readme-top">back to top</a>)</p>



## Getting started

The code runs with Airflow and Mlflow. 

To launch these applications, open a terminal for each and type their respective command lines after having installed them. 

```sh
# Terminal 1
mlflow server --backend-store-uri mlflow/ --artifacts-destination mlflow/ --port 8000
```

```sh
# Terminal 2
airflow standalone
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>
