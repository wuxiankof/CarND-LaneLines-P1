# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:

- Step 1: converted the original image to grayscale. 
- Step 2: applied Gaussian smoothing to the grayscale image with the kernel size 5.
- Step 3: applied Canny function to show the edges only, with low threshold 50 and high threshold 150.
- Step 4: created a mask to filter out the edges of interest, with the vertices of a quadrilateral defined.
- Step 5: applied Hough transform to identify lines of lanes and drew them in a black image.
- Step 6: drew the lines image on the original image using the "weighted_img" function.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by the following steps: 
- Step 1: separate line segments by their slopes $(y_2-y_1)/(x_2-x_1)$ into two lists: list_left and list_right respectively.
- Step 2: for each side (left or right), calculated an "average line" of which the coordinates $(x_1, y_1, x_2, y_2)$ took the average of the coordinates of all line segments from that side.
- Step 3: for each side (left or right), calculated the slope and intercept of the "average line" and extrapolated it to the top and bottom of the quadrilateral defined previously. 
- Step 4: drew both left and right single lines on the image space.


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming is when running the video, I noticed that the single straight lines drawn may not be parallel exactly with the actual lane lines, especially when the lane lines are thick yellow/white lines.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to identify both edges of a thick lane line and calculate the "middle line" to represent this thick lane line for the following calculations. 