# Image Captioning with InceptionV3 and LSTM

This repository contains the implementation of an **Image Captioning Model** using a combination of **InceptionV3** (for image feature extraction) and an **LSTM** (for generating captions). The model generates textual descriptions of images using the Microsoft Common Objects in Context [(MS COCO)](http://cocodataset.org/#home) dataset.

# COCO Dataset

The COCO dataset is one of the largest, publicly available image datasets and it is meant to represent realistic scenes. What I mean by this is that COCO does not overly pre-process images, instead these images come in a variety of shapes with a variety of objects and environment/lighting conditions that closely represent what you might get if you compiled images from many different cameras around the world.

To explore the dataset, you can check out the [dataset website](https://cocodataset.org/#explore)

## Dataset
The model is trained on the **COCO Dataset**, which consists of:
- 5000 images
- 5 captions per image
  
Download the below dataset and store in working directory for further use:

`http://images.cocodataset.org/zips/val2017.zip`

`http://images.cocodataset.org/annotations/annotations_trainval2017.zip` --> captions_val2017.json

# Explore

Click on the explore tab and you should see a search bar that looks like the image below. Try selecting an object by it's icon and clicking search!

<img width="825" alt="COCO_Explorer" src="https://user-images.githubusercontent.com/37503046/175939855-dc4b0b3c-2c45-4f81-bd35-c0ee368dd1b1.png">


You can select or deselect multiple objects by clicking on their corresponding icon. Below are some examples for what a sandwich search turned up! You can see that the initial results show colored overlays over objects like sandwiches and people and the objects come in different sizes and orientations.

<img width="562" alt="COCO_sandwiches" src="https://user-images.githubusercontent.com/37503046/175940295-b94b5a46-357f-4011-8fc0-aff104f421b9.png">


# Captions

COCO is a richly labeled dataset; it comes with class labels, labels for segments of an image, and a set of captions for a given image. To see the captions for an image, select the text icon that is above the image in a toolbar. Click on the other options and see what the result is.
<img width="666" alt="COCO_Captions" src="https://user-images.githubusercontent.com/37503046/175941984-2f9665d5-5cea-475d-aca6-0184c1b9717d.png">


When we actually train our model to generate captions, we'll be using these images as input and sampling one caption from a set of captions for each image to train on.

## Dataset Visualization
![coco-examples](https://user-images.githubusercontent.com/37503046/175942061-c23dce55-3d2f-4110-afa0-5ad4df9ad07c.jpg)

## Model Architecture
This project uses a **two-part model**:
1. **Feature Extractor (Encoder)**: A pre-trained **InceptionV3** model is used to extract feature vectors from images. These vectors represent the visual information.
2. **Caption Generator (Decoder)**: An **LSTM-based** network generates a caption, conditioned on the image features and previously generated words.

The architecture includes:
- **Encoder model** for image feature layer and sequence layer
- **Decoder model** combine both image feature and sequence layer
- **Dense Layers** with **ReLU** and **Softmax** activations for output
- **Final model** with input and output and compile it with **Adam** optimizer

## 🔧 Requirements & Installation

### Run in Google Colab (Recommended)

1. Upload notebook to Colab or open via GitHub → **Open in Colab**
2. Enable GPU  
   `Runtime → Change runtime type → GPU`
3. Mount Google Drive to load dataset
4. Run cells in order
