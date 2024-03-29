[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/yDpbj8_M)

# Project Overview

In this project, we integrate the MQTT dataset from Kaggle into a PostgreSQL table, perform initial analysis and preprocessing using PySpark, and build machine learning models using PySpark and TensorFlow. The models include different classifiers and regressors, which are tuned, and the best model is selected. The final step involves running the models on Google Cloud Compute and creating a comprehensive report on the results.

## About the Dataset

The [MQTT dataset](https://www.kaggle.com/datasets/cnrieiit/mqttset/) is related to a smart home environment where sensors retrieve information about temperature, light, humidity, CO-Gas, motion, smoke, door, and fan at different time intervals.

## Dataset Columns
To better understand our dataset, we decided on constraints and description for each of the columns. In order to perform data engineering methods, we believe providing these details was an essential step towards smart and resourceful data engineering.

| Column                     | Constraints and Type | Description                                     |
|----------------------------|----------------------|-------------------------------------------------|
| tcp_flags                  | Not nullable, hex    | TCP flags                                       |
| tcp_time_delta             | Not nullable         | Time difference between two TCP packets         |
| tcp_len                    | Not nullable, int    | Length of TCP packets                            |
| mqtt_conack_flags          | Nullable="0", hex    | MQTT Flags                                      |
| mqtt_conack_flags_reserved | Not nullable, double | Reserved MQTT Flag                               |
| mqtt_conack_flags_sp       | not nullable, double  |  Another MQTT Flag                               |
| mqtt_conack_val            |double, 0-158         | Indicates the result of the connection attempt between a client and a broker |
| mqtt_conflag_cleansess     |not nullable          | MQTT clean flag |
| mqtt_conflag_passwd        |not nullable          | MQTT password presence |
| mqtt_conflag_qos           |not nullable          | Quality of service level |
| mqtt_conflag_reserved      |not nullable          | Resevered Flag |
| mqtt_conflag_retain        |not nullable          | Whether message should be reserved |
| mqtt_conflag_uname         |not nullable          | Username present or not |
| mqtt_conflag_willflag      |not nullable          | Last will message flag |
| mqtt_conflags              |nullable="0", hex     | Indicates whether the client requests a clean session or a persistent session with the broker. |
| mqtt_dupflag               |not nullable, binary  | Indicates that a message is a duplicate and has been resent because the intended recipient did not acknowldge it |
| mqtt_hdrflags              |nullable="0", hex     | The first byte of the fixed header in the MQTT packet |
| mqtt_kalive                |double                | Kepp-alive interval used for MQTT connections |
| mqtt_len                   |not nullable, int     | Length of MQTT packets |
| mqtt_msg                   |not nullable, double  | MQTT messages |
| mqtt_msgid                 |not nullable          | MQTT message ID  |
| mqtt_msgtype               |not nullable, int 0-14| Type of MQTT message  |
| mqtt_proto_len             |not nullable, double  | Length related to MQTT protocol |
| mqtt_protoname             |nullable="0", "MQTT"  | Name of MQTT protocol |
| mqtt_qos                   |not nullable, double  | Quality of service for MQTT |
| mqtt_retain                |not nullable, double  | Retain flag for MQTT |
| mqtt_sub_qos               |not nullable, double  | Quality of Service level for MQTT subscription |
| mqtt_suback_qos            |not nullable, double  | Quality of Service level in MQTT subscription acknowledgments |
| mqtt_ver                   |not nullable, double  | MQTT protocol version |
| mqtt_willmsg               |not nullable, double  | The "last will" message in MQTT |
| mqtt_willmsg_len           |not nullable, double  | Length of the MQTT "last will" message |
| mqtt_willtopic             |not nullable, double  | MQTT "last will" topic |
| mqtt_willtopic_len         |not nullable, double  | Length of the MQTT "last will" topic |
| target                     |legitimate/dos/malformed/slowite/bruteforce/Flooding, not nullable, string | Attack or not, if attack then what kind |
| train (column introduced by us) |int, not nullable     | Test (0) or Train (1) dataset |


## About the Models

### PySpark ML

1. Linear Regression:
   - Hyperparameters:
        - regParam: Influences how well or poorly the regressor fits to the curve
        - maxIter: controls how long each model would train for before stopping, the quicker we stop the less likely we are to overfitting
   - Testing Accuracy after Hyperparameter tuning: 83.11%

3. Random Forest Decision Tree:
   - Hyperparameters:
        - maxDepth: How deep any given tree would go; greater max depth would take longer to train, but would be increase accuracy
        - numTrees: How many trees make up the maxdepth, more tress results in more randsomness, in turn the model will be less liekly to overfit
   - Testing Accuracy after Hyperparameter tuning: 86.76%

### PyTorch

1. Deep Neural Network:
   - Architecture: 4 hidden layers, 128 neurons each
   - Activation: RReLU (to have a little randomness), Loss: Cross Entropy, Optimizer: Adam
   - Learning Rate: 0.005, Decay Rate: 0.995
   - Testing Accuracy: 83.21%

2. Shallow Neural Network:
   - Architecture: 2 hidden layers, 8 neurons each
   - Activation: ReLU, Loss: Cross Entropy, Optimizer: Adam
   - Learning Rate: 0.05 (No decay)
   - Testing Accuracy: 83.31%
  

## Code Walkthrough Video URL
The following video contains a clear and concise walkthrough of our code from Task 1 through Task4, alongwith the extra credit. In this code walk through, we showed Task 1 and 2 run locally on our machine, however Task 3 and 4 were run on the cloud. 
https://cmu.box.com/s/0u2fkt3g2r9tlgy6dyb7ya2jbs7c0krv
### Screen recroding for Task 1 and 2 on cloud
https://cmu.box.com/s/20vkxi44ji219tgekqo7sq0zi3vqj9v2
### Essentials to run the code:
1. Please make sure that the correct path to the .csv files is given in order to import the data correctly
2. Please make sure all the necessary libraries have been downloaded before hand
3. The .jars file for Postgres should be placed in the JARS folder.
4. Since we ran the extra credit part using our credentials, you will not be able to run the postgresql unless you use your credentials. 




