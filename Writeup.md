# **Finding Lane Lines on the Road** 

## Writeup Report

### Reflection

### 1. Description of the pipeline.

My pipeline consisted of 5 steps:
1. Convert the image to grayscale;
1. Gaussian smoothing / blurring;
1. Canny edge detection;
1. Apply an image mask;
1. Hough transform.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
