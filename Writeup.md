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

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by
1. separating left and right line segments by theirs lope ((y2-y1)/(x2-x1)):
```python
lines_L = [line for line in lines.squeeze() if (line[3]-line[1])/(line[2]-line[0]) < -0.5]
```
2. collecting x and y as 1d arraies:
```python
xL = []
yL = []
for x1,y1,x2,y2 in lines_L:
    xL.append(x1)
    xL.append(x2)
    yL.append(y1)
    yL.append(y2)
```
3. extrapolating the line to the top and bottom of the lane:
```python
poly_L = np.polyfit(yL,xL,1)
cv2.line(img, (int(poly_L[0]*img.shape[0]+poly_L[1]), img.shape[0]), \
         (int(poly_L[0]*img.shape[0]*0.612+poly_L[1]), int(img.shape[0]*0.612)), color, thickness)
```

In order to make the pipeline more robust for the challenge, I modified the pipeline by adding a white-yellow color filter before step 1:
```python
def color_filter(img, rgb_threshold):
    color_select = np.copy(img)
    thresholds = (img[:,:,0] < rgb_threshold[0]) \
                | (img[:,:,1] < rgb_threshold[1]) \
                | (img[:,:,2] < rgb_threshold[2])
    color_select[thresholds] = [0,0,0]
    return color_select
    
rgb_threshold = [210, 150, 0]
color_select = color_filter(image, rgb_threshold)
```

### 2. Potential shortcomings with the current pipeline


One potential shortcoming would be the white-yellow color filter may fail to work at different light conditions.

Another shortcoming could be a linear lane model may not work well when there is a sharp turn.


### 3. Possible improvements to the pipeline

A possible improvement would be to make `rgb_threshold` adaptive to the light conditions. 

Another potential improvement could be to switch to a quadratic lane model if the previous slopes exceed some thresholds.
