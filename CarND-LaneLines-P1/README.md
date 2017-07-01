# **Finding Lane Lines on the Road** 


---

**Goals**

The goal of this project is to make a pipeline that finds lane lines on the road.


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Description

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/bVtMK7KwavY/0.jpg)](https://www.youtube.com/watch?v=bVtMK7KwavY)

The template for the this pipline was taken from Udacity Self-Driving Car Nanodegree. 

My pipeline consisted of 5 steps. First, I converted the images to HSV color space, then I created a mask to filter
yellow and white colors from HSV image. I then extracted combined yellow and white colors from the original image.

Second, I applied Guassian bluring with a kernel size of 15 and canny edge detection on the image form the previous step.

Third, I created a four sided polygon to mask lanes and applied hough transform to canny lane edges.

Fourth, in order to draw a single line on the left and right lanes, I extrapolate line segements from hough transform. Extrapolation was done by filtering near vertical and horizontal lines and then averaging other parameters of the line.

Fifth, I drew actual lines on the original image. Instead of modifying the draw_lines() function, I call extrapolate_line function to provide end coordinates of the line and pass them to draw_lines function to draw the final line. 


### Potential Improvements


One potential shortcoming of this pipeline is to find lane lines on a very curvy road, the straight averaged lane lines may not show correct lanes in that case. 

Another shortcoming is when driving from a dark (black) road patch where lane markings are more pronounced to light (gray cement road) patch where they appear light due to reflection. In one of the frames in the test video the yellow line on the dark road is identified but not on the connecting cement patch.  


A possible improvement would be to mask lanes before HSV transform and amplify intensity of yellow and white lines and/or attenuate intensity of other colors to identify even lightest of lane markings. 

Another potential improvement could be to use linear regression to curve fit the line segments. Instead of drawing a single line draw_lines() function can draw severl connecting lines to cover the lanes.
