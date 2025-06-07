Signature Verification using Siamese Neural Network
==================================================

This project implements a deep learning-based signature verification system using a Siamese Neural Network. 
The model learns to compare two signature images and determine whether they are from the same person (genuine) or not (forged).

Overview
--------

This system is designed for offline signature verification using a Siamese neural network architecture. 
It employs Convolutional Neural Networks (CNNs) to extract features from input images and compares them using 
Euclidean distance to determine similarity.


Model Architecture
------------------

- Base CNN Encoder: Shared network to extract features from both input images
- Distance Function: Euclidean distance computed between feature vectors
- Loss Function: Mean Squared Error (MSE)
- Optimizer: Adam

The model is trained to reduce the distance between similar signatures and increase the distance for dissimilar ones.

Dataset Format
--------------

The training data should be provided in a CSV file (train_data.csv) with the following format:

image1,image2,label
001/001_01.PNG,001/001_02.PNG,1
001/001_01.PNG,001_forg/001_05.PNG,0

1: Same person (genuine signature pair)
0: Different persons (forged pair)

Installation
------------

Install the required dependencies using pip:

pip install tensorflow numpy pandas opencv-python

Training the Model
------------------

Ensure the train_data.csv and signature image folders are correctly set up. Then, run the training script:

python signature_verification.py

This will:
- Load and preprocess the image pairs
- Train the Siamese neural network
- Save the trained model as siamese_model.h5

Signature Verification
----------------------

You can verify if a test signature matches a reference signature using the verify_signature() function:

result = verify_signature(model, "test_signature.png", "reference_signature.png", threshold=0.5)
print(result)

Output:
- "Test Signature is authentic."
- "Test Signature is a forgery."

Model Saving and Loading
------------------------

To save the trained model:

model.save('siamese_model.h5')

To load the saved model:

from tensorflow.keras.models import load_model
model = load_model('siamese_model.h5', custom_objects={'euclidean_distance': euclidean_distance})

Features
--------

- Siamese network architecture for one-shot learning
- Simple image preprocessing (grayscale, resize, normalize)
- Flexible CSV-based pairing system
- Easily extensible and production-ready

