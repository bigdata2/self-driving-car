# **Finding Lane Lines on the Road** 


---

**Goals**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to HSV color space, then I create a mask to filter
yellow and white colors from HSV image. I then extract combined yellow and white colors from the original image.
Second, I apply Guassian bluring with a kernel size of 15 and canny edge detection on the image form the previous step.
Third, I create a four sided polygon to mask lanes and apply hough transform to canny lane edges.
Fourth, I extrapolate line segements from hough transform to create a solid line covering lane from bottom to middle
of the frame. extrapolation is done by filtering near vertical and horizontal lines first, then averaging other
parameters of the line.
Fifth, I draw actual lines on the original image. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
