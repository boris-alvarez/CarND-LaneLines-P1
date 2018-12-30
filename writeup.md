# **Finding Lane Lines on the Road** 



### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a Gaussian smoothing to filter image noise.
Following step is to detect edges on the image, using Canny edge detection. We filter the edges detected with a region of interest, where only edges within this region would be kept for future processing. Finally we use the Hough transform to detect lines of interest within the image. Most of them should be part of left and right lanes.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by partitioning the lines into 2 sets: left and right lanes. A positive slope hints a right lane while a negative slope hints a left lane. Then I average the centers of the lanes for each set, and used curve fitting to extrapolate a single straight lane. Finally, I draw the right and left lanes over the original image, using y-coordinate from the region of interest, and computing the corresponding x-coordinate.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![output example][test_images_output/solidWhiteCurve.jpg]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the slope is infinite. In this case, I exclude the slope which result in a loss of information when trying to infer a lane (there might be cases where we want to draw a line with infinite slope). 

Another shortcoming could be the lane detection is too dependent on the region of interest. When noise (like other cars, other lanes) is within the region of interest, it strongly affect the results.




### 3. Suggest possible improvements to your pipeline

A possible improvement would be to average lane finding in time (keep some history), to be less affected by noise within the region of interest and get better context for lane finding.

Another potential improvement could be to improve or make the region of interest more adaptative. For example, if we are driving right behind a car, we might rely more on very short region of interest and strong history, and possibly follow the car in front of us.
