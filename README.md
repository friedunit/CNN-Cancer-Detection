# CNN-Cancer-Detection

## Overview

#### The goal of this project is to create an algorithm to identify metastatic cancer in small impage patches taken from larger digital pathology scans. The data used is a slightly modified version of the PatchCamelyon (PCam) benchmark set.

#### This is a binary classification problem to analyze digital images of 96 px X 96 px. 

#### The data set was downloaded from https://www.kaggle.com/c/histopathologic-cancer-detection/data

## Initial findings in the data:

* We see in the data frame description that there are 220,025 observations with all of them being unique. 
* There are 2 columns, 'id' contains the matching id with an image in the 'train' folder and 'label' is a binary integer representing 0 as false (non cancerous) and 1 as true (cancerous)
* Currently, 'id' is an object data type but we can make that a string. 'label' is currently an integer but we can make that a factor
* In the 2 folders from the downloaded data set, there are 220,025 in the 'train' folder corresponding to the id's in the data frame. The 'test' folder has 57,458
* For value counts of 'label', we can see there are many more non-cancerous (0) labels than cancerous. 130,908 to 89,117, respectively.

![image](https://github.com/friedunit/CNN-Cancer-Detection/assets/10797098/879b6ca1-c138-4da0-bc40-3573b8c5a26c)

## Model Architecture

#### For the structure of the model, I played around with a few different designs based off of the Sequential model. Here, I did 3 blocks with 3 CNN layers each. Filter size of 3x3 with the first layer having 32 filters, the second with 64 and the third with 128. Each uses 'reLU' activation and includes max pooling with 2x2 filters and a batch normalization. After the 3 layers, I added a flatten layer, 3 dropout layers and 3 dense layers before the final sigmoid dense output layer. 

![image](https://github.com/friedunit/CNN-Cancer-Detection/assets/10797098/a37e9a1e-ee79-4102-8fab-46f5147f4b52)

![image](https://github.com/friedunit/CNN-Cancer-Detection/assets/10797098/4986e3eb-c520-4771-be0f-16c3ee04bfa8)



## Findings and Conclusion

#### I ran into lots of different problems with versions of Tensorflow and model training sessions getting stuck or freezing. I finally had to reinstall version 2.15 of Tensorflow with Python 3.9.16 and got these 12 epochs to run smoothly. Looking at the accuracy and loss plots above, this model performed fairly well but we see that epoch 4 had very bad validation loss and accuracy. With the training accuracy and loss improving but validation accuracy and loss jumping around like it did, that would indicate overfitting and the model not generalizing well to the data. With more time, I would extend the number of epochs and test different hyperparameters such as optimizers, learning rate, and different layers for the model. The accuracy didn't quite flatten out yet with 12 epochs and the loss was still on the decline. 
