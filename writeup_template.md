# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

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

- My pipeline consisted of 6 steps for each frame in the video:
1. Convert image to grayscale
2. Apply gaussian filter on grayscale image
3. Compute edges using canny edge detector on image from step 2
4. Compute region of interest that contain the lane on image from step 3
5. Apply hough lines to detect lines in image from step 4
6. Overlay detected lines from step 5 on the original image.

- In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
1. Initialize Ymin = Ymax = height of image
2. Initialize right_lane_m, left_lane_m, right_lane_b, left_lane_b with empty lists
3. for each detected line: 
    1. Compute slope & intercept
    2. Update Ymin to be the minimum between Ymin, y of point 1, y of point 2
    3. if slope is negtive 
        1. current line in the right lane 
        2. append slope, intercept to right_lane_m and right_lane_b respectively 
    4. else 
        1. current line in the left lane 
        2. append slope, intercept to left_lane_m and left_lane_b respectively 
4. Compute mean of right_lane_m, left_lane_m, right_lane_b, left_lane_b
5. for each lane :
    1. Compute upper_corner for using (y-b/m) by substitute y = Ymin, b = mean_b, m = mean_m
    2. Compute lower_corner for using (y-b/m) by substitute y = Ymax, b = mean_b, m = mean_m
    3. Draw line between upper and lower corner


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the hood of the car is appearing in the image causing lines to apear on the image
and it will be hard to draw lines since most of the lines are in lower part of the image.

Another shortcoming could be when there are shadows on the road causing false postive lines, also it make it hard to detect lines covered by the shadow.

Another shortcoming will be parameter tuning for all image/video resolution


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to try to compensated for the hood of the car by updating the parameters for region of interest to correctly detect lanes

Another potential improvement could be to tune the parameter of the hough lines and battle test the solution on different datasets

Another potential improvement could be to use standard resolution for all videos or resize videos that doesn't agree with our standard before processing
