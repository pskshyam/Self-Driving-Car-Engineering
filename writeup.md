# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines in the given images
* Apply the same pipeline on a video - a series of images - to draw line segments onto the road
* Optimize the pipeline for averaging/extrapolating the line segments to map out the full extent of lane lines

---

[//]: # (Image References)

[image1]: ./test_images_output/grayscale/output_solidWhiteCurve.jpg "Grayscale"
[image2]: ./test_images_output/canny_edges/output_solidWhiteRight.jpg "Canny Edges"
[image3]: ./test_images_output/masked_edges/output_solidWhiteRight.jpg "Masked Edges"
[image4]: ./test_images_output/images_line_segments/output_solidWhiteRight.jpg "Line Segments"
[image5]: ./examples/line-segments-example.jpg
[image6]: ./examples/laneLines_thirdPass.jpg

### Reflection

### 1. Pipeline Description

My pipeline consisted of the below 5 steps. 
1. Converting the images to grayscale
2. Applying Gaussian Blur to smooth out the images
3. Applying canny edge detection to find edges in the images
4. Defining a region of interest by filtering out unwanted edges in the images
5. Using Hough Transform to find out line segments
6. Drawn lines on the original images

Below are the images resulted out of each step in the pipeline:
![alt text][image1] ![alt text][image2] ![alt text][image3] ![alt text][image4]

A function <b>process_image()</b> is created with the pipeline code which takes an image as input and returns image with line segments drawn. This function is used to modify the images of a video clip by replacing the frame with the function output.

In order to draw a single line on the left and right lines, I modified the <b>draw_lines()</b> function by
1. Finding slope and center of each line in an image and appending them to lists created for right and left slope and center
2. Defining slope threshold between 0.5 and 0.9 for left and right lines to avoid extreme slopes
3. Finding single left and right slop and center by averaging all lines slope and center
4. Derived coordinates of the left and right lines (x1,y1,x2,y2) using formula y-y1 = M(x-x1) where M is the slope of the line, (x,y) is the center of the line and the value of y1 is given as height of the image
4. Drawn left and right lane lines on the image

The result of modified draw_lines() function is below image clip of the video:

![alt text][image6]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are sharp and blind curves.

Another shortcoming could be identifying lines in different conditions like darkness, fog, rain, etc.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to dynamically identifying regions of interest (ROI) in any given image.
