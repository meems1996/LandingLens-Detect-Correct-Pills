# Example of using LandingLens to detect the correct pills from an image
Overview of the repository
1. 📁 Training Dataset folder
2. 📁 Inference Dataset folder
3. 📄 pill_detector.ipynb 

The goal of this repository is to give an easy to understand and simple example of using LandingLens to gather a set of images, train a model on the dataset of images, and use the API with the trained model on a new image to see how well it was trained. 

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
<img src="image.png" alt="drawing" width="1000" style="border-radius: 15px; border: 2px solid #3498db;""/>
</div>

### Training the model
* After the images were labeled we can begin training the model. In this example, training the model on the dataset of 18 images of pills took 3 minutes. 
* After the images are labeled we click the button to begin training the model.

<div align="center">
<img src="image-1.png" alt="drawing" width="600" style="border-radius: 15px; border: 2px solid #3498db;""/>
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
<img src="image-2.png" alt="drawing" width="600" style="border-radius: 15px; border: 2px solid #3498db;""/>
</div>

