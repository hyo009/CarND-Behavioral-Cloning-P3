# CarND-Behavioral-Cloning-P3

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py, model.ipynb containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* writeup_report.md or writeup_report.pdf summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed
I followed the lectures and tried the models. For my submission, I choose Nvidia model. As explained in the lectures, RELU Layers were provided in terms of activation of Convolutional Layers to introduce non-linearity in the model. I used Cropping2D method from Keras to remove the sky and the small area in front of vehicle to reduce parameters and training time of the model.

#### 2. Attempts to reduce overfitting in the model
I augmented the data to reduce overfitting. I used all three cameras' images (left, center and right). I chose 0.2 as the correction factor of steering angles as discussed in the lectures. Moreover, in the generator, I set the possibility of 50% to flip image horizontally in order to augment the data.
