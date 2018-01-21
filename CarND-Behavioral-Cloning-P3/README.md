# **Behavioral Cloning** 


---

**Goals**

The goals of this project were:
- Design and train a neural network model so that it can drive on a track on which it was trained on.
- Drive using the trained model on a challenge track, the images/frames of which have never been seen by the trained model.
- Keep the car on the road at all times and avoid collisions with objects in the simulation.
- Finish one lap (drive back to the starting point) of both the tracks by observing the aforementioned constrains.
- Create a model using RNN (LSTM).

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
- 280K parameters -- a 25 times decrease in model parameters without losing image accuracy i.e. the image input to the model is still 75x320. The total number of parameters for this model are at par with Nvidia's model (250K), yet the image input to the model is of higher resolution 75x320 vs. 66x200.
- The car is able to complete both track 1 and the challenge track within the constraints. 
- A 2 times decrease in training time and over 1.5 times decrease in training loss compared to baseline.

[![Track1_1](https://img.youtube.com/vi/I_JYEPtcm5Q/0.jpg)](https://www.youtube.com/watch?v=I_JYEPtcm5Q&t=2s)
[![Track2_1](https://img.youtube.com/vi/tLaOe8gNrFY/0.jpg)](https://www.youtube.com/watch?v=tLaOe8gNrFY&t=73s)


### Data
Udacity's github contained a link to the initial training data, which was used to train all the models. The data is somewhat skewed, that is a large percentage of frames have zero steering angle, see e.g. data_summary.ipynb. Also, there are more frames with negative than positive steering angle. The data was augmented before training to include frames from the left and right cameras after adjusting their respective steering angles to normalize it.

### Description
The architecture is described in [this](https://arxiv.org/abs/1604.07316) paper.

![alt text](https://github.com/bigdata2/self-driving-car/blob/master/CarND-Behavioral-Cloning-P3/images/nvidia_model.png "Nvidia Model")

### Details

The model was trained on track1 exclusively, i.e. the during training the model was not provided with any frames other than those that belonged to track1. The car, as you can see in the video, is able to drive on challenge track -- the track it never saw before. One interesting observation is that since the model was never trained on a frame with two roads in parallel (like the ones toward the end of challenge track) and since it was trained to drive in the middle of the road, the car drives from one side of the road to another avoiding the center divider. I think it was very cool that the model was able to drive on very curvy roads of the challange track and that it was able to avoid the obstructions to correctly positions itself on the (wrong) side of the road. With more training that includes frames with parallel roads, it can easily avoid situations like those.

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

### Additional work
I implemented a Recurrent Neural Network model with convolution layers and Long Short Term Memory (LSTM). With LSTM model, the car is able to drive on the track much more smoothly compared to covnet model. However, it goes off track towards the end of the track. The reason is that the training data from Udacity is not one continuous sequence of frames but multiple sequences starting from different locations on the track and I did not preprocess data to remove discontinuities.
