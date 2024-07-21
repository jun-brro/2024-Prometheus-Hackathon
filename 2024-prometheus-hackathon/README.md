# Prometheus Hackathon 2024

This repository contains the code and documentation for the participation in the Prometheus Hackathon 2024.

[KAGGLE PAGE LINK](https://www.kaggle.com/competitions/2024-1-prometheus-hackathon/)

## METHOD

### Data Augmentation Techniques
#### 1. Random Horizontal Flip
Randomly flips the image horizontally with a probability of 50%.

#### 2. Random Rotation
Rotates the image randomly within a range of -60 to +60 degrees.

#### 3. Random Cutout
Applies random cutout transformations, where 1 to 3 square patches of 70x70 pixels are removed from the image. This technique helps the model become more robust by forcing it to focus on various parts of the image.

#### 4. Resizing
All images are resized to a fixed dimension of 224x224 pixels to maintain consistency and compatibility with pre-trained models.

---

### Dataset
#### Original Dataset
Path: /content/food_dataset/train
Size: 80% of the original dataset is used for training, and 20% is used for validation.
#### Augmented Dataset
Transformations Applied: RandomHorizontalFlip, RandomRotation, RandomCutout, Resize
Number of Augmentations: Each image in the training dataset is augmented twice, effectively tripling the size of the training set.
#### Test Dataset
Path: /content/food_dataset/test
Transformations: Only resizing to 224x224 pixels.

---

### Implementation
#### AugmentedDataset Class
A custom AugmentedDataset class is implemented to handle the application of multiple augmentations to the original training dataset. The class takes an original dataset and a list of augmentation transforms to generate an augmented dataset.

#### RandomCutout Class
A custom transformation class RandomCutout is implemented to randomly mask out square patches from the images.

---

### Data Loaders
Training Loader: Loads the augmented training dataset.
Validation Loader: Loads the validation dataset.
Test Loader: Loads the test dataset.

#### Usage
Showing Samples
The show_samples function is used to visualize random samples from the dataset, displaying the augmented images along with their labels.


## Model Structure

First Approach: Pytorch **Resnet50** (pretrained, IMAGENET1K_V2)

Final Approach: **Model Ensemble** (Resnet50, VGGNet16, InceptionV3)

#### Resnet50: IMAGENET1K_V2 | layer4 ~ learnable
![resnet50_architecture](https://github.com/user-attachments/assets/435421e5-2f65-4fa2-bf2e-e0b25f7cd600)


#### VGGNet16: IMAGENET1K_V1 | classifier[6] ~ learnable
![vgg16_architecture](https://github.com/user-attachments/assets/663d6a49-8ff4-455d-994f-153ecb2d7342)


#### InceptionV3: IMAGENET1K_V1 | fc parameters learnable
![inceptionv3_architecture](https://github.com/user-attachments/assets/9c15dc2e-4596-4610-a516-f7be3aadf870)


#### FC layer: 512 -> Dropout -> 19 -> LogSoftmax
![image](https://github.com/user-attachments/assets/1d3541b8-0487-475c-bbb4-9bf1130182f7)

## Result
Final Evaluation 0.88818
