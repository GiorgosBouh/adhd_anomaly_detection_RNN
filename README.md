Temporal Anomaly Detection and Prediction Using RNNs: A Full Pipeline

This repository provides a complete pipeline for detecting and analyzing temporal anomalies in activity data, with a focus on ADHD-related behavioral studies. The approach leverages the HYPERAKTIV dataset, which contains high-resolution temporal data on motor activity, and integrates anomaly detection with predictive modeling using Recurrent Neural Networks (RNNs).

Pipeline Overview

The procedure consists of the following steps:

1. Anomaly Detection with Isolation Forest
The first stage involves identifying anomalies in the activity data using the Isolation Forest algorithm.

Steps:

Data Loading:
CSV files containing time-stamped activity data are read and processed.
Each file includes:
TIMESTAMP: The time of the recorded activity.
ACTIVITY: A numerical value representing activity intensity.
Anomaly Detection:
The Isolation Forest model is applied to the ACTIVITY column to identify anomalous patterns.
A contamination parameter (0.05) specifies that 5% of the data is assumed to be anomalous.
Output:
A new column, ANOMALY (0 for normal, 1 for anomaly), is appended to the dataset.
Processed files are saved in a specified output directory for further analysis.
Example Command:

python isolation_forest_anomaly_detection.py --input-dir ./raw_data --output-dir ./anomaly_data
2. Anomaly Prediction with Recurrent Neural Networks (RNNs)
The second stage involves training an RNN model to predict anomalies based on temporal activity data.

Steps:

Data Preparation:
Time-series windows of 10 consecutive time steps are created from the normalized ACTIVITY column.
The ANOMALY column serves as the target variable.
The data is split into training (80%) and testing (20%) sets.
RNN Model Architecture:
A SimpleRNN layer with 50 units and ReLU activation for capturing temporal patterns.
A Dense output layer with sigmoid activation for binary classification.
The model is compiled with the Adam optimizer and binary cross-entropy loss function.
Training and Validation:
Early stopping is applied to prevent overfitting.
Model performance is evaluated on the test set, with accuracy and loss metrics computed for each participant.
Results Aggregation:
The results for all participants are saved in a summary CSV file.
Example Command:

python rnn_anomaly_prediction.py --folder-path ./anomaly_data --output-file ./rnn_results.csv
3. Descriptive Statistics and Visualization
The final stage involves summarizing the results and visualizing key metrics.

Steps:

Accuracy Distribution: Most participants achieved high accuracy, with minimal variability.
Loss Distribution: Low error rates across participants indicate consistent model performance.
Dataset Description

The HYPERAKTIV dataset contains temporal activity data collected via wearable accelerometers. Key features:

TIMESTAMP: Time of activity measurement.
ACTIVITY: An integer value representing motor activity intensity, derived from accelerometer counts.
ANOMALY: Added during the anomaly detection stage, indicating abnormal activity patterns.
Applications

This pipeline has potential applications in:

ADHD Behavioral Studies:
Detecting irregular movement patterns for diagnosis and intervention.
Objective monitoring of treatment efficacy.
General Temporal Data Analysis:
Identifying patterns and anomalies in time-series data.
Leveraging RNNs for predictive modeling.
How to Use

Install Dependencies: Ensure all required Python libraries are installed:
pip install -r requirements.txt
Run Anomaly Detection: Process raw activity data to identify anomalies:
python isolation_forest_anomaly_detection.py --input-dir ./raw_data --output-dir ./anomaly_data
Run RNN Analysis: Train and evaluate the RNN model:
python rnn_anomaly_prediction.py --folder-path ./anomaly_data --output-file ./rnn_results.csv
Generate Statistics and Visualizations: Summarize results and create graphs:
python summarize_results.py --input-file ./rnn_results.csv --output-dir ./visualizations


This project leverages the HYPERAKTIV dataset and employs state-of-the-art machine learning techniques for temporal anomaly analysis. Special thanks to the dataset contributors for enabling this research.
