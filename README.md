# pokemon-classifier
 Classification of Pokemon photos using VGG16 and Imagenet Weights (Transfer Learning)

This aims to solve an image classification of several pokemons classes using Transfer Learning from a Pre-Trained Neural Network. I will be using the ImageNet Trained VGG16 model from Tensorflow Module.

# Methodology

Below is the outline of the methodology:

1. Data Preparation and Analysis
    - Showing a sample of the photo
    - Splitting the photos by Training/Validation/Testing splits using `Split-folders`
    - Using Data Augmentation with Tensorflow's `Image Data Generator` due to small sample size (Only for Training data)
    - Converting the pictures into input arrays for the model training and evaluation
2. Model Architecture Building and First Training
    - Importing `VGG16` model with the Imagenet weights and biases
    - Freezing `VGG16` model layers
    - Adding hidden layers and output layer
    - Using the following optimizers:
        - Root Mean Square Propagation (RMSprop) <br>
        - Schochastic Gradient Descent (SGD) <br>
        - Adam Optimizer (Adam) <br>
    - Training the model
3. Second re-training
    - Un-freezing the `VGG16` model's weights and biases
    - Setting a low learning rate
    - Re-training the model
4. Comparison between first and second training, across the different optimizers
    - Comparision using average Training and Validation Accuracy between un-trainable VGG16 vs trainable VGG16 Layers
    - Comparision using Test Accuracy between all the different models


# Reproducability

## Data

The photos have already been split 70/20/10 Train/Validate/Test. <br>
Should you choose to change these percentage, the original directory is available in ```pokemon``` folder. <br>

## Dependancies

Aside from installing Deep Learning related Python modules, please install `PIL` and `split-folder` modules. <br>
File ```requirements.txt``` is available at repository for easier reproducability.

Alternatively, detailed instructions to install manually are below:

Installing `PIL`:
1. Open Anaconda Prompt
2. Change to relevant conda environment by `conda activate <environment-name>`
3. Using Anaconda Prompt, you can type either `pip install PIL` or `conda install PIL`.

Installing Split-Folders: <a href="https://pypi.org/project/split-folders/"> Link here </a>

1. Open Anaconda Prompt
2. Change to relevant conda environment by `conda activate <environment-name>`
3. You can install by typing command `pip install split-folders`


# Results 

This section is to compare the metrics between unfreezing the VGG16 model, as compared to freezing the model. The first section looks at Training and Validation Accuracy, and the second Section looks at Model Evaluation using Test Accuracy metric.

## Training and Validation Accuracy Comparison

For the below Training and Validation Accuracy values, it is an average Training and Validation Accuracy from the last 5 epochs. <br><br>

### First Comparision: "Frozen" VGG16 model except Dense Layers

Below is a table summary

| | Training Accuracy | Validation Accuracy|
| --- | --- | --- |
| | |
| Adam | <b>99.32%</b> | 75.00% |
| RMSProp | 98.74% | 64.00% |
| SGD | 97.71% | 76.00% |

Best model within the First Comparison: <b> Adam Optimizer </b> <br><br>

### Second Comparision: "Unfrozen" VGG16 model except Dense Layers

| | Training Accuracy | Validation Accuracy|
| --- | --- | --- |
| | |
| Adam | <b>99.66%</b> | 79.00% | 
| RMSProp | 99.09% | 66.00% |
| SGD | 98.86% | 76.00% |

Best model within the Second Comparison: <b> Adam Optimizer </b> <br><br>

### First vs Second Comparisons:

Looking at Training Accuracy, there is only about 2-3% differences. Hence, I will not use Training Accuracy as the comparison, but use Validation Accuracy instead. 

The best model with highest Validation Accuracy is the Trainable VGG16 Model (Weights/Biases not frozen). <br><br>

## Model Accuracy using Test Accuracy Metric

### First Comparison: Untrainable/Frozen Model

Below is the table summary of the Model Test/Evaluation for Untrainable/Frozen Model VGG16 Model:
    
| | Test Accuracy | 
| --- | --- |
| | 
| Adam | 60.00% | 
| RMSProp | 60.00% |
| SGD | <b>68.00%</b> | 

<br>

### Second Comparison: Trainable/Unfrozen Model

Below is the table summary of the Model Test/Evaluation forTrainable/Unfrozen VGG16 Model:

| | Test Accuracy | 
| --- | --- |
| | 
| Adam | <b>84.00%</b> | 
| RMSProp | 56.00% |
| SGD | 72.00% | 

<br>

### Test Accuracy: First vs Second Comparison

Best model is the Trainable Model using Adam Optimizer

# Final Remarks

After performing the above comparisons, the best model is the Trainable/Unfrozen Model using Adam Optimizer using a small learning rate. 