# Applying IoTDevID to a New Dataset: the CIC IoT Dataset 2022 Case Study

# Overview
In this repository you will find a Python implementation of the methods in the paper Applying IoTDevID to a New Dataset: the [CIC IoT Dataset 2022](https://www.unb.ca/cic/datasets/iotdataset-2022.html) Case Study.

# Summary


In an age where a new IoT device is added to our lives every day, one of the most important ways to keep these devices up to date and secure is to recognise them, diagnose their problems, and take the necessary measures by using device identification. The IoTDevID method we propose uses machine learning to identify a device using features extracted from network packets. In this method, identifying features which cause overfitting are eliminated and the feature set created by a multilayer feature selection method among the distinguishing features is tested on multiple datasets. Thus, it promises robust and generalisable identification. IoTDevID can identify both IP and non-IP devices, and its identification success is greatly enhanced by incorporating the aggregation algorithm. In this study, we will validate our work by testing our IoTDevID work on a new dataset, [CIC IoT Dataset 2022](https://www.unb.ca/cic/datasets/iotdataset-2022.html).


# Requirements and Infrastructure: 

Wireshark and Python 3.10 were used to create the application files. Before running the files, it must be ensured that [Wireshark](https://www.wireshark.org/), [Python 3.10+](https://www.python.org/downloads/) and the following libraries are installed.

| Library | Task |
| ------ | ------ |
|[ Scapy ](https://scapy.net/)| Packet(Pcap) crafting |
|[ tshark ](https://www.wireshark.org/)| Packet(Pcap) crafting |
|[ Sklearn ](http://scikit-learn.org/stable/install.html)| Machine Learning & Data Preparation |
| [ Numpy ](http://www.numpy.org/) |Mathematical Operations|
| [ Pandas  ](https://pandas.pydata.org/pandas-docs/stable/install.html)|  Data Analysis|
| [ Scipy  ](https://pypi.org/project/scipy/)|  Data Analysis, Mathematical Operations|
| [ Matplotlib ](https://matplotlib.org/users/installing.html) |Graphics and Visuality|
| [Seaborn ](https://seaborn.pydata.org/) |Graphics and Visuality|
| [tabulate ](https://pypi.org/project/tabulate/) |Pretty-print tabular data output|
| [tqdm ](https://tqdm.github.io/) |Progress meter|



The technical specifications of the computer used for experiments are given below.

|  | |   |
| ------ |--|  ------ |
|Central Processing Unit|:|12th Gen Intel(R) Core(TM) i7-12700H   2.30 GHz|
| Random Access Memory	|:|	16.0 GB (15.7 GB usable)|
| Operating System	|:|	Windows 11 Home |

# Data: 
Using the [CIC IoT Dataset 2022](https://www.unb.ca/cic/datasets/iotdataset-2022.html) data, feature extraction was performed, and the feature sets obtained were used in different ways at different stages of the study as indicated in the following table.

| Data | Description |
| ------ | ------ |
|[ PCAP Files ](http://205.174.165.80/IOTDataset/CIC_IOT_Dataset2022/)| Raw Network data, Input of Feature Extraction - Used in Section III.C|
|[ All Sessions [54 CSV]](https://drive.google.com/file/d/12AY9GOdhVMaEoYAIyTrrF6sl6R26mVib/view)| Output of Feature Extraction, Used in Section IV.A|
|[AA, AI, IA, II](https://drive.google.com/file/d/1rCk38jOXAdWfoVWtfoKXpcBNjuSgXeBp/view?usp=sharing)| Merged Sessions |
|[AA, AI, IA, II %10 sample](https://drive.google.com/file/d/1ADeh0nNFWT4BpIExnv-BoBzrtMJBHaC8/view?usp=sharing)| Size reduced merged sessions - Used in Section IV.B |
|[ AA+non-IP Devices](https://drive.google.com/file/d/1G8bDKCpfW6pun6zNBMXsNpyDwt_KPjvF/view?usp=sharing)| Size reduced AA with Non-IP/Zigbee data - Used in Section IV.C |




# Implementation: 

We used jupyter notebook (ipynb) to present the codes. The file with the ipynb extension has the advantage of saving the state of the last run of that file and the screen output. Thus, screen output can be seen without re-running the files. Files with the ipynb extension can be run using [jupyter notebook](http://jupyter.org/install). 




## Feature Extraction (PCAP2CSV) 
#### Section III.C in the article

* [01.0 - Features_Extraction](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/01.0%20-%20Features_Extraction.ipynb): This file convert the files with pcap extension to single packet-based, CSV extension fingerprint files and creates the labeling.

* [01.1 - Unknown-MAC-cleaning](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/01.1%20-%20Unknown-MAC-cleaning.ipynb): This file removes fingerprints other than known MAC addresses. These fingerprints are unlabelled because their MAC addresses are unknown.

* [01.2 - Creating_smaller_DF_with_Selected_features](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/01.2%20-%20Creating_smaller_DF_with_Selected_features.ipynb): In feature extraction, about 100 features are created. However, we will not use most of these features. This file reduces the file size by removing the features we don't use.

* [01.3 - Creating Session_ID.ipynb](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/01.3%20-%20Creating%20Session_ID.ipynb): This file assigns an identification number to each session to indicate which sessions have the same devices.

## PERFORMANCE EVALUATION
#### Section IV.A in the article

* [02.0 - CIC results with Session ID vs Session ID ](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/02.0%20-%20CIC%20results%20with%20%20Session%20ID%20vs%20Session%20ID%20.ipynb): It uses sessions with the same ID number as training and testing data and classifies them with the DT model.

* [02.1 - Heatmap of session results](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/02.1%20-%20Heatmap%20of%20session%20results.ipynb): Displays the results of the classification operation in the previous step on a heatmap in terms of F1  score.

* [02.2 - Statistics of class-based results - failed device classes](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/02.2%20-%20Statistics%20of%20class-based%20results%20-%20failed%20device%20classes.ipynb):  This file gives statistics on the distribution of Idle-Active pairs and the most failing devices as the class base results.

#### Section IV.B in the article
* [03.0 - Split_training_testing](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/03.0%20-%20Split_training_testing.ipynb): Combines sessions for broader representation in training and testing datasets. Each newly created dataset is then as small as 10% of its size.
* [03.0 - Hyperparameter Optimization](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/03.0%20-%20Hyperparameter%20Optimization.ipynb) :In this file, hyperparameter optimization is applied via [sklearn-Randomizedsearch](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html) to DT model.
* [03.1 - General evaluation of the all sessions](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/03.1%20-%20General%20evaluation%20of%20the%20all%20sessions.ipynb): In this file, results are obtained for the Idle and Active datasets using individual, and aggregated methods. A group size of 13 was used in the aggregation  operations.

#### Section IV.C in the article
* [04.0 - Preprocessing other data](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/04.0%20-%20Preprocessing%20other%20data.ipynb): Non-IP devices are filtered from Power and Interactions sessions and added to Active training and testing datasets.
* [04.1 - General evaluation with other data](https://github.com/kahramankostas/IoTDevID-CIC/blob/main/04.1%20-%20General%20evaluation%20with%20other%20data.ipynb):  In this file, results are obtained for the Idle and Active datasets using individual, and aggregated methods with Non-IP devices. The group size of 13 was used in the aggregation  operations.




# License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details


# Citations
If you use the source code please cite the following paper:

```
cite
```

Contact:
*Kahraman Kostas
kahramankostas@gmail.com*


