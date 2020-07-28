# Product Recognizer Mobile App

## Overview
Packaged goods provide a challenge to people who are blind. It is impossible to distinguish between two different unopened canned goods on the basis of touch, sound, smell or taste. Blind people must rely on a sighted person when shopping for packaged goods and often label each item with a tactile label in order to distinguish between the products at home. 

Computer vision technology, however, can provide independence to those who are blind. An app that can "see" and identify the item that someone is holding will enable the person to easily find the product they require in the pantry at home or even at the store.

This mobile app uses computer vision to classify objects shown through the phone's camera. An image classification model was written in TensorFlow and trained on 16 varieties of canned goods. Inference is performed using a TensorFlow Lite version of the model. I modified a TensorFlow Lite example Java app (https://github.com/tensorflow/examples/tree/master/lite/codelabs/flower_classification/android), by adding a main page, relegating the second and third predictions to the expanded section of the lower screen, and removing the TensorFlow Lite banner.

## App
The main page enables the user to choose the category of items to recognize (at this time, however, both buttons initialize inference with the canned goods model - see "Future Work" below). 

Once the user is on the inference screen, the app continuously makes inferences on what it "sees" through the phone's camera in near real-time. The lower screen containing the prediction can be expanded to show the top 3 predictions and confidence scores, as well as details about the image and inference time.

<p align="center">
  <img src="https://github.com/rmbright19/ProductRecognizerApp/blob/master/images/app_0000.jpg" img width="200" alt="App main page">
  <img src="https://github.com/rmbright19/ProductRecognizerApp/blob/master/images/app_0001.jpg" img width="200" alt="Recognizing Progresso Chicken & Dumpling Light">
  <img src="https://github.com/rmbright19/ProductRecognizerApp/blob/master/images/app_0002.jpg" img width="200" alt="Expanded lower screen">
</p>

The model recognizes 16 different canned goods, and is able to correctly identify products even when they are held upside down or with the text occluded.
<p align="center">
  <img src="https://github.com/rmbright19/ProductRecognizerApp/blob/master/images/app_0003.jpg" img width="200" alt="Winco Diced Tomatoes with Italian Herbs">
  <img src="https://github.com/rmbright19/ProductRecognizerApp/blob/master/images/app_0017.jpg" img width="200" alt="Campbell's Bean with Bacon upside down">
</p>

## Data
So that the model would several different levels of visual difference among the items, I chose 4 brands of canned goods and 4 products from each brand. I photographed each of the 16 products, varying the location/background of the item, the camera angle, and the item orientation (right side up, upside down, angled, sideways). Additionally, I occluded parts of the can labels, even covering the label's text entirely in some images.

## Model
The model was trained via transfer learning on a pre-trained MobileNetV2 model. By using transfer learning, I was able to get acceptable accuracy (72% on the validation set) for my prototype app with very little data. The whole training/validation dataset consisted in 60 images of each product. The training/validation split was 80/20, so training was done on about 48 images of each of the 16 items. I trained the model using GPU in Google Colab.

## Future Work
In order to assist a person who is blind or has low vision, the app will need to read the predictions and possibly confidence scores out loud. Additionally, the model should be able to classify a large number of common products. I would ideally like to add separate models for chips, herbs/spices, etc., with a button for each on the main page. Finally, it would be handy if instead of the app continuously making inferences, the user was able to start and stop the inference process from the classification screen.
