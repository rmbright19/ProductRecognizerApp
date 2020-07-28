# Product Recognizer Mobile App

## Overview
Packaged goods provide a challenge to people who are blind. It is impossible to distinguish between two different unopened canned goods on the basis of touch, sound, smell or taste. Blind people must rely on a sighted person when shopping for packaged goods and often label each item with a tactile label in order to distinguish between the products at home.

This mobile app uses computer vision to classify objects shown through the phone's camera. An image classification model was written in TensorFlow and trained on 16 varieties of canned goods. Inference is performed using a TensorFlow Lite version of the model. I modified a TensorFlow Lite example app (https://github.com/tensorflow/examples/tree/master/lite/codelabs/flower_classification/android), adding a main page, relegating the second and third predictions to the pull-out section of the lower screen, and removing the TensorFlow Lite banner.

## Future Work
In order to assist a person who is blind or has low vision, the app will need to read the predictions and possibly confidence scores out loud. Additionally, the model should be able to classify a large number of common products. I would ideally like to add separate models for chips, herbs/spices, etc., with a button for each on the main page. Finally, it would be handy if instead of the app continuously making inferences, the user was able to start and stop the inference process from the classification screen.

## Data
I gathered data by taking photos of each of the 16 products. I varied the location/background of the item, the camera angle, and the item orientation (right side up, upside down, angled, sideways). Additionally, I occluded parts of the can labels, even covering the label's text.

## Model
The model was trained via transfer learning on a pre-trained MobileNetV2 model. By using transfer learning, I was able to get acceptable accuracy (72% on the validation set) for my prototype app with very little data. The whole training/validation dataset consisted in 60 images of each product. The training/validation split was 80/20, so training was done on about 48 images of each of the 16 items. I trained the model using GPU in Google Colab.
