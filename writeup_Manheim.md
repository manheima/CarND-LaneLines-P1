# **Finding Lane Lines on the Road**

*Aaron Manheim* 4/22/2019

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image0]: ./test_images/solidYellowCurve2.jpg "Original Image"
[image1]: ./test_images_output/CannyOutput.png "Canny Edge Detection"
[image2]: ./test_images_output/RegionMaskedCannyOutput.png "Region Masked Canny"
[image3]: ./test_images_output/RegionMask.png "Region Mask"
[image4]: ./test_images_output/HoughLineDetection_RawLines.png "Hough Line Detection Raw"
[image5]: ./test_images_output/WeightedHoughLineDetection_RawLines.png "Weighted Hough Line Detection Raw"
[image6]: ./test_images_output/HoughLineDetection.png "Weighted Hough Line Detection"
[image7]: ./test_images_output/WeightedHoughLineDetection.png "Weighted Hough Line Detection"
---

### Reflection

### 1. Description of Pipeline

My pipeline started by taking in an image of the road.
![alt text][image0]

The pipeline consisted of 4 steps. First, I converted the image to grayscale and ran a Canny Edge detection algorithm. This resulted in only keeping the sharp edges:
![alt text][image1]

Next, I masked only othe region of interest:
![alt text][image3] 
![alt text][image2]

After that, I ran a Hough Transform to extract lines from the pixels forming the lane lines:
![alt text][image4]
![alt text][image5]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by classifying lines as left vs right lane lines by checking position in x and also if slope was greater than or less than 0. I then took a weighted average (weighted by the length of the line) of the slopes and intercepts to get a signle line for each lane:
![alt text][image6]
![alt text][image7]


### 2. Ptotential shortcomings with the current pipeline


One potential shortcoming would be if the  Hough algorithm resulted in a line which was perfectly vertical. This relults in a "divide by zero" scenario and would crash the program when I take the weighted averages of the lines.

Another shortcoming could be dealing with roads with more exagerted turns. If this was the case, then both the left and right lane lines could have slopes > 0  and my algorithm would not be able to determine which side was which.


### 3. Possible improvements to the pipeline

A possible improvement would be to make the algorithm robust to vertical lines.

Another potential improvement could be to improve the classification for whether a lane is on the left or right side.
