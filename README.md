# Brain Tumor Segmentation : BRATS Challenge 2020 
#### Dataset from : 
https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation

Dataset information:
Multimodal scans available as NIfTI files (.nii.gz) 

Four 'channels' of information – 4 different volumes of the same region
- Native (T1) 
- Post-contrast T1-weighted (T1CE)
- T2-weighted (T2)
- T2 Fluid Attenuated Inversion Recovery (FLAIR) volumes

All the imaging datasets have been segmented manually and were approved by experienced neuro-radiologists. 

Annotations (labels): 
- Label 0: Unlabeled volume
- Label 1: Necrotic and non-enhancing tumor core (NCR/NET)
- Label 2: Peritumoral edema (ED)
- Label 3: Missing (No pixels in all the volumes contain label 3)
- Label 4: GD-enhancing tumor (ET)

Our approach:
- Step 1: Get the data ready
- Step 2: Define custom data generator
- Step 3: Define the 3D U-net model
- Step 4: Train and Predict

### Step 1: Get the data ready

- Download the dataset and unzip it. 
- Segmented file name in Folder 355 has a weird name. Rename it to match others.
- Install nibabel library to handle nii files (https://pypi.org/project/nibabel/)
- Scale all volumes (using MinMaxScaler).
- Combine the three non-native volumes (T2, T1CE and Flair) into a single multi-channel volume. 
- Reassign pixels of value 4 to value 3 (as 3 is missing from original labels).
- Crop volumes to remove useless blank regions around the actual volume of interest (Crop to 128x128x128).
- Drop all volumes where the amount of annotated data is less that certain percentage. (To maximize training on real labeled volumes). 
- Save all useful volumes to the local drive as numpy arrays (npy).
- Split image and mask volumes into train and validation datasets.

### Step 2: Define custom data generator
Keras image data generator only works with jpg, png, and tif images. 
It will not recognize npy files. We need to define a custom generator to load our data from the disk. 

### Step 3: Define the 3D U-net model
Extend the standard 2D U-Net into 3D OR use 3D segmentation models library 

### Step 4: Train and Predict
- Train by loading images in batches using our custom generator. 
- Predict and plot data for visualization.
