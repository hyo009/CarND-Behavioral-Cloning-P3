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
I followed the lectures and tried the models. For my submission, I choose Nvidia model. As explained in the lectures, RELU Layers were provided in terms of activation of Convolutional Layers to introduce non-linearity in the model. I used Cropping2D method from Keras to remove the sky and the small area in front of vehicle to reduce parameters and training time of the model.(model.py line 96)

**cropping YUV images**
![alt text](https://github.com/hyo009/CarND-Behavioral-Cloning-P3/blob/master/images/crop.png?raw=true "cropping YUV images")

#### 2. Attempts to reduce overfitting in the model
I augmented the data to reduce overfitting. I used all three cameras' images (left, center and right). I chose 0.2 as the correction factor of steering angles as discussed in the lectures. Moreover, in the generator, I flip image horizontally in order to augment the data.(model.py line 65,66)

I used sklearn library function shuffle() to randomize training data.(model.py line 73) I also used train_test_split() to create validation data from training data (model.py line 82).

**left, center and right images**
![alt text](https://github.com/hyo009/CarND-Behavioral-Cloning-P3/blob/master/images/lcr.png?raw=true "left, center and right images")


#### 3. Model parameter tuning
My model used adam optimizer, so I did not have to tune any parameters. The model tuned automatically.(model.py line 110)


#### 4. Appropriate training data
Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road. At first, I used center images only. The vehicle cannot come back to the center of the lane at autonomous mode. Then I added left and right images to train the vehicle recover from the left and right sides of the road. I also tried to add more training data by myself. My new data's steering angles were recorded by my keyboard, which is not smooth. When I add my new data into training data, the result of model seems worse. So I only used original data.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach
I tried Lenet model first and trained it with center images. The result is not good. Then I added left and right images. The model still cannot keep the vehicle at the center of lane. Then I read Nvidia's paper. The result of the paper seems great and the number of parameters is pretty small. So I decided to have a try. I kept all the pre-processing techiques and trained Nvidia model. The result was great.

#### 2. Final Model Architecture
The final model architecture Nvidia (model.py lines 88-108) consisted of a convolution neural network with the following layers and layer sizes 24@31x98, 36@14x47, 48@5x22, 64@3x20, 64@1x18. Then it has a flatten layer followed by 3 fully connected layers outputting 100 neurons, 50 neurons and 10 neurons.

** Nvidia model from papar "End to End Learning for Self-Driving Cars"
![alt text](https://github.com/hyo009/CarND-Behavioral-Cloning-P3/blob/master/images/lcr.png?raw=true "left, center and right images")
