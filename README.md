# ECG_abnormalities

In this project, we tried to study ECG excerpts to classify different types of heartbeat.
We classify it in two categories : abnormal and normal heartbeat.

# Datasource

Our source of data is a group of ECG recordings provided by the MIT and the Beth Israel Deaconess Medical Center.
It's an open source archive that contains 48 half-hour excerpts of two-channel ambulatory ECG recordings.
These excerpts are about a group of person which have different forms of arrhythmia. Some of them didn't have this pathology.
You can download it there : https://physionet.org/content/mitdb/1.0.0/

# Source for this notebook

This notebook is in a big part inspired by the work of Andrew Long who created a tutorial on this subject : 
https://towardsdatascience.com/detecting-heart-arrhythmias-with-deep-learning-in-keras-with-dense-cnn-and-lstm-add337d9e41f

We also used the documentation of the different library : 
sklearn_som : https://sklearn-som.readthedocs.io/en/latest/
hmm_learn : https://hmmlearn.readthedocs.io/en/latest/

# Analysis and preparation of the dataset

Our data source is composed of groups of files that correspond to a patient. These files represent the ECG signal and the annotations for each heartbeat.
Each annotations are used to show the heartbeat type. We can classify these annotations in three categories : Normal, abnormal and non-beat. 
You can find the list of the annotations and their explanations there : https://archive.physionet.org/physiobank/annotations.shtml

The analysis of the annotations of all the recordings presents that 30% of them coresponds to an abnormal heatbeat.
(In this plot, -1 = non-beat, 0 = normal, 1 = abnormal)

![newplot](https://user-images.githubusercontent.com/82390655/220096063-83a3a71b-a551-4481-95cf-665d33529b3a.png)

We studied the profile of each patient to see if they all showed an anomaly in their recording.
The result presents that there are 2 of 48 who had a normal ECG.

![repartition](https://user-images.githubusercontent.com/82390655/220097892-c4af5657-6023-440e-aaa2-cce5e1b33f4f.png)

To prepare our training and validation data, we decided to split the patient group in two. 75% of them are in the training data (36 patients) and 25% in the validation data (12 patients). It seems to be the better way to work because it avoids that the annotations of a patient are in the validation and the training data. If it was the case, the AUC would show a data leakage. We also couldn't be sure that our models would work with a new patient.

We will use a window of 6 seconds around each heartbeat to be able to compare the beat before and after the current heartbeat. We will ignore the non-beat anotations.

# LSTM and SOM + HMM model

## LSTM

To implement the LSTM algoithm, we used the Keras libary : https://keras.io/api/layers/recurrent_layers/lstm/
We use the same parameter than the example to be able to compare this technique and the SOM + HMM.
To be able to execute quickly the training and the prediction and because we are limited by the capacity of Google Colab, we will work on the 10 000 first line of the training dataset.

## SOM + HMM

We created an SOM with two neurons and we trained it with the same data than LSTM. We made a transformation on the training and the validation data to obtain the distance between the neurons. These values are usefull to use it as probabilities on our HMM model.
We created also an HMM model with two states and we did a training with the tansformed trainig data. All this part are made in an unsupervised way. 

# Results

![roc_curve](https://user-images.githubusercontent.com/82390655/220125656-f5e73a69-cf63-4f8b-a88a-99eea736bd23.png)



|                 | LSTM Tutorial   | LSTM from the project | SOM + HMM       |
|:---------------:|:---------------:| :--------------------:|:---------------:|
| Prediction time |                 |                       |                 |
| AUC             |                 |                       |                 |
| Accuracy        |                 |                       |                 |




# Disclaimer
