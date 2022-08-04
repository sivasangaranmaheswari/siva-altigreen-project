# siva-altigreen-project

This repository contains the work done by me in the duration of my internship at Altigreen Propulsion Labs.

---

# List of Work Done

1.	**Exploratory Data Analysis**

Data corresponding to multiple vehicles were given to me. A legend containing the meaning of columns was also given to me. The vehicle data has 3 different types of features. One set of features come from the sensors like vehicle speed, motor speed, motor temperature, accelerator pedal, etc. The next set of features come from the BMS system, like SOC, DTE, etc. The final set of features come from the GPS system, like latitude, longitude, altitude, GPS speed, etc. The data also has different fault flags. The total no. of columns in each vehicle dataset file is 70. Each of the faults are given a code and a name. Different sets of fault codes are combined into a field. There are the following fault fields in the dataset: Fault Code 1, Fault Code 2, BMS Status 1, BMS Status 2, VDM Fault, BMS Relay State and BMS Failsafe Status. Remaining columns are features. 
The aim of this project is to predict the occurrence of a fault a significant time (like 15 minutes) before it actually occurs so that some kind of user intervention is possible.
First, some exploration of the data needs to be done and some insights need to be derived before modelling. 
Among the features, I have dropped out certain features marked in the legend as (Reserved) or (Not Applicable). Out of the remaining features, only one of them, FRN Status, is a categorical feature, and the rest are continuous features. Coming to the faults, each of the fault fields has a number which needs to be decoded using the legend file. Each fault field contains a number, which, when represented in binary format, each of its bits represents a fault. Doing bitwise AND of a fault field with a fault code from the legend gives its presence or absence in that record. In all, combining all the fault bits together, there are 86 faults. 

---
## Example:
Code for CONTACTOR_STATE_INV fault = 32768. If fault_code1 field has value 49216, then 49216 & 32768 = 32768. So, this fault is present. Similarly, if it has value 30000, then 30000 & 32768 = 0. So, this fault is absent.

image.png

2. **Visualizing the data**

In this program, I have visualized different features of the data to get a visual insight of how exactly the faults are activated for various feature values. Putting it clearly, I have tried to separate the faulty features from the non-faulty ones, by categorizing with respect to different features.

3.	**Model – 1: Mapping features to faults.**
In this model, each timestep is considered as an example, with the input as the features and target as the individual fault. Thus, it is being formulated as a 2-class classification problem. Since each fault needs a separate model, we need to build an ML model for each fault. For ML modelling, XGBoost is used for the following reasons: XGBoost is similar to a decision tree but improves its classification performance due to its property of “boosting” the learning rate in successive decision trees. It is also not a black-box model. It is possible to find which feature the model is using for its predictions, and this can be combined with the domain knowledge to derive many useful insights.

