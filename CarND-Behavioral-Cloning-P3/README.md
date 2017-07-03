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

#### Initial Results
5M parameters -- image input to the model is 75x320
[![Track1](https://img.youtube.com/vi/sySmG0PEE14/0.jpg)](https://www.youtube.com/watch?v=sySmG0PEE14&t=2s)
[![Track2](https://img.youtube.com/vi/Zhd47unbbEc/0.jpg)](https://www.youtube.com/watch?v=Zhd47unbbEc&t=73s)

#### Results for optimized model
- 280K parameters -- a 25 times decrease in model parameters without losing image accuracy i.e. the image input to the model is still 75x320. 
- The car is able to complete both track 1 and the challenge track within the constraints. 
- A 2 times decrease in training time and over 1.5 times decrease in training loss compared to baseline.

- Videos coming soon.

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
- The model requires a few libraries including [tensorflow-gpu](https://www.tensorflow.org/install/install_linux#gpu_support), [keras](https://github.com/fchollet/keras), [opencv](http://opencv.org/), [numpy](http://www.numpy.org/), all of which can be easily setup using miniconda, instructions [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md)
- Nvidia GPU (optional) 


### How to run the model
- Clone the repo
- Download simulator from the above link
- Open simulator by executing ./linux_sim.x86_64
- Execute the model using the following command: python drive.py  model.json


### Hardware
 - [Dell PowerEdge 710](https://www.dell.com/downloads/global/products/pedge/en/server-poweredge-r710-tech-guidebook.pdf) with 64 GB DRAM
 - A [x16 PCI riser card](https://www.serversupply.com/ACCESSORIES/RISER%20CARD/POWEREDGE/DELL/GP347.htm) for R710
 - [PCI riser cable](https://www.newegg.com/Product/Product.aspx?Item=N82E16812183020&ignorebbr=1&nm_mc=KNC-GoogleAdwords-PC&cm_mmc=KNC-GoogleAdwords-PC-_-pla-_-Cables+-+Internal+Power+Cables-_-N82E16812183020&gclid=CN_UmtTt6dQCFYZffgodSIAImw&gclsrc=aw.ds) to connect GPU which sits externally on the top cover of R710
 - A 750 Watt external power supply and an [ATX Power Supply Terminator](http://www.frys.com/product/6489932) to power the GPU
 - Nvidia 1080 TI GPU
 - A lot of patience. Yes, it took me a while to put all the pieces together and make them work with the correct software configuration.

### Future/Current work
I am working on a different model to use LSTM after the (3d?) convolution layers. This should enhance the accuracy on curved roads where it can start correcting the steering angle early on and provide a smooth turn. Second, I will include speed as an ouput in addition to angle so that the car can slow down at curves and speed up at straight roads. 
