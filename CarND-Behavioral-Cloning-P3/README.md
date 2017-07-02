# **Behavioral Cloning** 


---

**Goals**

The goals of this project are:
- Design and train a neural network model so that it can drive on a track on which it was trained on.
- Drive using the trained model on a challenge track, the images/frames of which have never been seen the trained model.
- Keep the car on the road at all times and avoid collisions with objects in the simulation.
- Finish one lap (drive back to the starting point) of both the tracks by observing the aforementioned constrains.
- Use RNN (LSTM) to compare the accuracy of the two models (goal not yet met).

These goals were set by me and are not part of Uadcity's self-driving project as I am not enrolled in that program.

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Results

[![Track1](https://img.youtube.com/vi/sySmG0PEE14/0.jpg)](https://www.youtube.com/watch?v=sySmG0PEE14&t=2s)
[![Track2](https://img.youtube.com/vi/Zhd47unbbEc/0.jpg)](https://www.youtube.com/watch?v=Zhd47unbbEc&t=73s)


### Data

### Description
Coming soon

![alt text](https://github.com/bigdata2/self-driving-car/blob/master/CarND-Behavioral-Cloning-P3/images/nvidia_model.png "Nvidia Model")

### Details
This is a work in progress, I will add more details as I get time.

The model was trained on track1 exclusively, i.e. the during training the model was not provided with any frames other than those that belonged to track1. The car as you can see in the video is able to drive on challenge track -- the track it never saw before. One interesting observation is that since the model never say two roads in parallel (like the ones toward the end of challenge track), and since it trained to drive in the middle of the road, the car drives from one road to another avoiding the center divider. I think it was very cool that the model was able to drive on very curvy roads of the challange track and that it was able to avoid the obstructions to correctly positions itself on the (wrong) side of the road. With some training of parallel roads it can easily avoid situations like those.

### Dependencies
I have built and tested this model on Linux (Ubuntu 16.04). The model has the following dependencies:
- Udacity's simulator which can be found [here](https://d17h27t6h515a5.cloudfront.net/topher/2017/February/58983558_beta-simulator-linux/beta-simulator-linux.zip)
- The model requires a few libraries all of which can be easily setup using miniconda, instructions [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md)
- Nvidia GPU (optional) 


### How to run the model
- Clone the repo
- Download simulator from the above link
- Open simulator by executing ./linux_sim.x86_64
- Execute the model using the following command: python drive.py  model.json


### Hardware

### Future/Current work
I am working on a different model to use LSTM after the (3d?) convolution layers. This should enhance the accuracy on curved roads where it can start correcting the steering angle early on and provide a smooth turn. Second, I will include speed as an ouput in addition to angle so that the car can slow down at curves and speed up at straight roads. 
