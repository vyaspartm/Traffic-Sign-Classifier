# **Traffic Sign Recognition** 

# Overview

This work is Part of Udacity nanodegree: Self Driving ar Engineer. This this project I have developed a Traffic Sign Classifier using Deep learning and convolutional neural networks.It is advisable to use AWS, Udacity Classroom for using GPU instances but I have worked on my local machine that has NVIDIA 1080 GPU. The model is trained using  German Traffic Sign Dataset and I have tested 5 random images from internet

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

[//]: # (Image References)

[dataset_visualization]: ./output_img/dataset_visualization.png "Visualization"
[training_images]: ./output_img/training_images.png "Training Samples"
[image4]: ./test_img/image1.png "Traffic Sign 1"
[image5]: ./test_img/image2.png "Traffic Sign 2"
[image6]: ./test_img/image3.png "Traffic Sign 3"
[image7]: ./test_img/image4.png "Traffic Sign 4"
[image8]: ./test_img/image5.png "Traffic Sign 5"

Here is a link to my [project code on GitHub](https://github.com/vyaspartm/Traffic-Sign-Classifier/blob/master/Traffic-Sign-Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Basic summary of the dataset:

I used the pandas library to calculate summary statistics of the traffic signs data set:

* The number of training examples: 34799
* The number of validation examples: 4410
* The number of testing examples: 12630
* The shape of a traffic sign image is 32*32*3
* The number of unique classes/labels in the data set is 43

#### 2. Exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing count for each traffic sign.

![alt text][dataset_visualization]

Below are the samples images from training data set for each class:

![alt text][training_images]

### Design and Test a Model Architecture

#### 1. Preprocessing the image data.


I normalized the image data so that the data has mean zero and equal variance.


#### 2. Final model architecture

The final model consists of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, VALID padding, output = 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, VALID padding, output = 14x14x6	|
| Convolution 5x5	    | 1x1 stride, VALID padding, output = 10x10x16	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, VALID padding, output = 5x5x16	|
| Flatten				| output = 400									|
| Fully connected		| input = 400, output = 120						|
| RELU					|												|
| Fully connected		| input = 120, output = 84						|
| RELU					|												|
| Fully connected		| input = 84, output = 10						|
| Softmax				|												|
 


#### 3. Training the model.

To train the model, I used following parameters:

| Optimizer				|		AdamOptimizer			|
| Batch Size			|		128						|
| Epochs				|		20						|
| Learning rate			|		0.001					|

#### 4. Approach

I choose two convolutional layers and two hidden fully connected neural network layers for optimized accuracy.
I have used convolutional kernel filters of size 5*5 .
I used AdamOptimizer instead of GradientDescent optimizer. The downside is it takes more computation time for training but I believe it to be better in terms of accuracy.
I have used dropout technique to minimize over-fitting problem and thus improve the accuracy. The value of keep_probability I have used is 0.90.

Number of EPOCHs required for training: I am storing last three values of validation accuracy value and for each iteration, I am comparing new validation accuracy with the average of last three stored values. If new values is less than the average of last three consecutively two times, I am stopping the learning process to avoid over-fitting.

My final model results were:

* training set accuracy of 0.984
* validation set accuracy of 0.958
* test set accuracy of 0.877


### Test a Model on New Images

#### 1. Five German traffic signs taken from the web for testing:

Here are five German traffic signs that I found on the web:

Image1: 80 km/h traffic sign
Description: In this image, outer white ring for the traffic sign is missing from the image.
![alt text][image1]

Image2: No Entry Traffic sign
Description: This image contains street view in the background
![alt text][image2] 

Image3: Turn Left Ahead Traffic sign
Description: This image contains traffic sign with street view behind and very less outer white ring.
![alt text][image3] 

Image4: 50 km/h Traffic sign
Description: This image contains traffic sign with trees in background and a few scratches.
![alt text][image4] 

Image5: Stop sign
Description: This image contains street view in the background and also image has few blue marks also.
![alt text][image5]


#### 2. Model's predictions :

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 80 km/h      			| 30 km/h  										| 
| No Entry     			| No Entry 										|
| Turn left ahead		| Turn left ahead								|
| 50 km/h	      		| 30 km/h						 				|
| Stop Sign				| Stop Sign   					 				|


The model was able to correctly guess 3 of the 5 traffic signs, which gives an accuracy of 60%. For image 1, prediction might have been failed as out white ring for the traffic sign is missing from the image. 

#### 3. softmax probabilities for each image along with the sign type of each probability:

image1.png:
Keep right: 60.06%
Speed limit (50km/h): 39.64%
Speed limit (30km/h): 0.27%
Roundabout mandatory: 0.03%
Turn right ahead: 0.00%

image2.png:
No entry: 100.00%
Traffic signals: 0.00%
End of all speed and passing limits: 0.00%
Stop: 0.00%
Right-of-way at the next intersection: 0.00%

image3.jpg:
Turn left ahead: 100.00%
Speed limit (20km/h): 0.00%
Speed limit (30km/h): 0.00%
Speed limit (50km/h): 0.00%
Speed limit (60km/h): 0.00%

image4.png:
Speed limit (30km/h): 98.59%
Speed limit (50km/h): 1.41%
Speed limit (80km/h): 0.00%
Speed limit (70km/h): 0.00%
Speed limit (100km/h): 0.00%

image5.png:
Stop: 70.57%
Bicycles crossing: 29.43%
No entry: 0.00%
Road work: 0.00%
Speed limit (80km/h): 0.00%

This project was made possible with help of [Udacity's delfdriving car engineer nanodegree](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013) and very detailed explaination by [Vivek Sharma](https://github.com/vivekmsit/CarND-Traffic-Sign-Classifier-Project)


