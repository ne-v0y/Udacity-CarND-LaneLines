# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a Gaussain Blur with kernel size of 5 to smooth out sharpe edges. Then I used the Canny edge detection algorithm to find all the edges. With a a pre-defiend polygon that foucses on the bottom part of the image, I applied the Hough Line transformation to find the lanes.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding line segements that have close slope(+/- 0.01 tolerance) and group them as candidates for `left_lane` and `right_lane`. To obtain an approximate threshold for the slope, I ran the test images to narrow down the range. For `right_lane`, the slope range is 0.5 to 10. For `left_lane`, the range is -0.5 to -0.8. I kept the range big in order to accomendate different siutations.

Here is the step by step result:

[grey and smoothed]: ./writeup_img/grey.png "Grey and smoothed"  
[Canny edge detection]: ./writeup_img/edge.png "Canny edge detection"  
[edges in region of interest]: ./writeup_img/roi_edges.png "Edge in region of interest"  
[extrapolation]: ./writeup_img/extrapolation.png "Line extrapolation"  
[final result]: ./writeup_img/result.png "Final result"  

For video processing, I added KCF tracking between frames when a detection failed. The green line in the image is a tracking result while all red lines are detections.
[tracking on left lane when detection failed]: ./writeup/detection_failed_tracking.png "Tracking left lane when detection failed"


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be parameter tuning. The threshold for lane candidates is hard-coded. 

Another shortcoming could be...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add another layer of verification: for example, a color based detection to enhance the results, since Hough Transformation wasn't very error-prone on dash lanes.

Another potential improvement could be to ...
