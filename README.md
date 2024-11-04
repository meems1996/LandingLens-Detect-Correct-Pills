# Example of using LandingLens to detect the correct pills from an image using Object Detection
Overview of the repository
1. 📁 Training Dataset folder
2. 📁 Inference Dataset folder
3. 📄 pill_detector.ipynb 

## Overview
This is an example of using LandingLens. A quick guide to how to set it up and build a fast project to get to see how it works. 

### Use Case and Goal
It's important to identify the use case and the goal of the project before we begin and invest the time and resources to train a model. 

For this example, the use case for this project is both for fun (to test LandingLens) and to also automate a task. 

The fun part of this project is identifying the different types of pills. In the pharmaceutical field this would have an actual advantage. Making sure to automate the task of identifying the correct pills. In this example, the pills are already sorted by their type and are easy to identify with a human eye pretty fast. So this is the fun part of the project. 

The second part of the project is to automate a task. Counting the pills. The use case here is making sure to know how many are left and when to ask for a refill. This allows the person to know when they need to get a refill for their prescription so they don't run out of medication. 

### Images for the Dataset
_Garbage in, garbage out!_

Using fewer but high quality images. 

### Managing Classes

## Use Case 
Sometimes I forget how many pills I have left and when I need to ask for a refill. Usually I have to count them by hand. If the pills are just a few it's not difficult, but if I want to plan a long vacation and see when I will need a renewal and if they won't last, counting them by hand is cumbersome. 

Using LandingLens you can create a simple detector in no time to count how many you have left. Knowing how many I take per day I created a simple code to let me know when I will need a refill. Most refills can be done same day, but it's good to add a day or two buffer if something goes wrong or if the pharmacy for some reason can't fulfill the request the same day. 

## Goal of this repository

The goal of this repository is to give an easy to understand and simple example of using LandingLens to gather a set of images, train a model on the dataset of images, and use the API with the trained model on a new image to see how well it was trained. 

This repository uses the Object Detection project type. Object Detection is used to identify multiple objects in an image with bounding boxes. With Object DEtection project types its important to draw precise and tight boxes around the objects of interest, like the pills in my examples. 

It's important for the model to realize that the background is not important to the detection, so I am excluding as much of the background round each pill as I can. This is because the model will look at every pixel inside the bounding box (the box you draw around the object) and it will consider each and every pixel to be important. 

## Workflow of building the model in LandingLens
Building a model involves 4 main steps: Upload, Label, Train, and Predict. 
* Upload your training dataset (in our case the 18 images of pills)
* Label what you want recognized by the model (in this case the three different types of pills: b12 vitamin, antidepressant, and a painkiller)
* Train (Start the training on the dataset)
* Predict (Upload a new image on the trained model to see how well it worked, or didn't work)

### Uploading the dataset
* Use high quality data. Remember the saying "garbage in, garbage out". 
* Quality over quantity here matters. 
* LandingLens requires at least 10 labeled images for training. In this example we are using a dataset of 18 images. 

### Labeling the images in the dataset
* There are 3 different classes in this example, the 3 different types of pills we want detected. More classes(categories) = more complex model. In this example it was important to provide a decent amount of images to be labeled for b12 vitamins and the antidepressants because the two pills look very similar. It was important to provide images of what makes them different (the b12 pill is cleaner and smaller, while the antidepressant has a ridge on it and some numbers as well)

<div align="center">
<img src="README screenshots/image.png" alt="drawing" width="1000" style="border-radius: 15px; border: 2px solid #3498db;""/>
</div>

### Training the model
* After the images were labeled we can begin training the model. In this example, training the model on the dataset of 18 images of pills took 3 minutes. 
* After the images are labeled we click the button to begin training the model.

<div align="center">
<img src="README screenshots/image-1.png" alt="drawing" width="600" style="border-radius: 15px; border: 2px solid #3498db;""/>
</div>

### Making predictions on a new image
* To get ready to use the model we click the deploy tab on the app and create an endpoint. 
* PIck a name for the endpoint, in this case it's Detect pills.
* This will give us an API command we can use.

```python
from PIL import Image
from landingai.predict import Predictor
# Enter your API Key
endpoint_id = "8d1eb3ea-f05e-4b5c-bffb-8e9882c95045"
api_key = "FILL_YOUR_API_KEY"
# Load your image
image = Image.open("image.png")
# Run inference
predictor = Predictor(endpoint_id, api_key=api_key)
predictions = predictor.predict(image)
```
> You can get an API key from a button under the API command View API Key and Secret

<div align="center">
<img src="README screenshots/image-2.png" alt="drawing" width="600" style="border-radius: 15px; border: 2px solid #3498db;""/>
</div>

