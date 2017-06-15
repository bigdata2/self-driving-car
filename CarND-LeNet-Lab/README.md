# LeNet-Lab
This lab was cloned from Udacity's github. The objective of this lab is to create convolution and pooling layers followed by a fully connected network similar to LeNet model shown in the Jupyter notebook.

Since the jupyter notbook is self explanatory, I will only list the learning points that were new to me and that improved the accuracy and reduce training time.

1) Use GPU if you want to tinker with the model and run it rapidly. On my macbook pro each epoch took over 30 seconds. Compare that with Nvidia 1080 TI where 15 epochs took less 30 seconds (increasing the batch size from 128 to 256 also contributed to faster turnaround). The reduced run-time on GPU allowed me to change parameters quickly and get an intuition of the training results.
2) I started by creating convolution kernels with random weights, which was giving me accuracy of beteen .90 to .92. I then constrained the random weights to have 0 mean and have thrm bound within a specified standard deviation. Zero mean helps gradient descent converge faster and elevated the accuracy between .94 to .95
3) For Maxpooling, initially I used a stride of 1x1 which resulted in a larger  kernel size -- 15x15. In MNIST dataset most of the numbers are contained within 15x15 pixel window. So a 15x15 maxpooling was dropping a lot of information resulting in reduced accuracy. I then reduced the kernel size to 2x2 with analogous increase in stride size -- 2x2. This increased the accurancy to .99. 
4) TODO: Both validation and test accuracy increase to .992 if I increase the training epochs. However, I noticed that the accuracy fluctuates between .98 to .992. I have to yet to analyze why that happens and if I can use tensorflow early termination to get the maximum accuracy.  

### Dependencies
This lab requires:

* [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit)

The lab enviroment can be created with CarND Term1 Starter Kit. Click [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) for the details.
