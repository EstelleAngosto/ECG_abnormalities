# ECG_anomalities

In this project, we tried to study ECG excerpts to classify different types of heartbeat.
We classify it in two categories : abnormal and normal heartbeat.

# Datasource

Our source of data is a group of ECG recordings provided by the MIT and the Beth Israel Deaconess Medical Center.
It's an open source archive that contains 48 half-hour excerpts of two-channel ambulatory ECG recordings.
These excerpts are about a group of person wich have different forms of arrhythmia. Some of them didn't have this pathology.
You can download it there : https://physionet.org/content/mitdb/1.0.0/

# Source for this notebook

This notebook is in a big part inspired by the work of Andrew Long who created a tutorial on this subject : 
https://towardsdatascience.com/detecting-heart-arrhythmias-with-deep-learning-in-keras-with-dense-cnn-and-lstm-add337d9e41f

We also used the documentation of the different library : 
sklearn_som : https://sklearn-som.readthedocs.io/en/latest/
hmm_learn : https://hmmlearn.readthedocs.io/en/latest/

# Analysis and preparation of the dataset

Our data source is composed of groups of files that correspond to a patient. These files represent the ECG signal and the annotations for each heartbeat.
You can find the list of the annotations and their explanations there : https://archive.physionet.org/physiobank/annotations.shtml

The analysis of the annotations of all the recordings presents that 30% of them coresponds to an abnormal heatbeat.

![newplot](https://user-images.githubusercontent.com/82390655/220096063-83a3a71b-a551-4481-95cf-665d33529b3a.png)
