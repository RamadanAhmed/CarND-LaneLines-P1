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
6. Split lines to be left lines and right lines according to the their location from position from 1/2 the width
7. Compute coefficient (slope and intercept) for left lines and right lines
8. smooth coefficient by using prior frames(10) coefficient to reduce lane shakiness
9. extrapolate the lines using region of interest vertices
10. if slope computing is not possible use previous frames
11. create images with extrapolated lines   
1. Overlay extrapolated lines from step 5 on the original image.

- In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
1. Split lines to be left lines and right lines according to the their location from position from 1/2 the width
2. Compute coefficient (slope and intercept) for left lines and right lines
3. smooth coefficient by using prior frames(10) coefficient
4. extrapolate the lines using region of interest vertices
5. if slope computing is not possible use previous frames
6. create images with extrapolated lines   
7. Overlay extrapolated lines from step 5 on the original image.


### 2. Identify potential shortcomings with your current pipeline


The algorithm works well in most scenarios but fails in the following conditions (If you apply the algorithm to the optional video you'll see the algorithm failing when it encounters such conditions):

- Shadow on roads
- Curved Lanes
- Reduced visibility in case of unfavourable weather conditions

### 3. Suggest possible improvements to your pipeline

- Only accept lines that have slops within acceptable range and reject other lines.
- You'll get to see a glimpse of this later but you can try playing around with different Color Spaces that might be able to handle shadows on road.
- You could try implementing a Spline Model for complex lane detection as described here
