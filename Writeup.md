1# **Finding Lane Lines on the Road** 

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
1. separating left and right line segments by theirs lope ((y2-y1)/(x2-x1)):
```
lines_L = [line for line in lines.squeeze() if (line[3]-line[1])/(line[2]-line[0]) < -0.5]
```
1. collecting x and y as 1d array
```
xL = []
yL = []
for x1,y1,x2,y2 in lines_L:
    xL.append(x1)
    xL.append(x2)
    yL.append(y1)
    yL.append(y2)
```
1. extrapolating the line to the top and bottom of the lane
```
poly_L = np.polyfit(yL,xL,1)
cv2.line(img, (int(poly_L[0]*img.shape[0]+poly_L[1]), img.shape[0]), \
         (int(poly_L[0]*img.shape[0]*0.612+poly_L[1]), int(img.shape[0]*0.612)), color, thickness)
```


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
