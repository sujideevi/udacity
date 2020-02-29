# **Finding Lane Lines on the Road**

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report
Identifying the Lane lines on the road would be a very common and basic requirement of a self-driving car. This can be achieved by using the computer vision techniques. Udacity has provided sample images of 960x540 pixels to desing the code for lane identification. Later images frames from video clips of same resolution has been processed using this algorithm.

**Pipeline**

Pipeline for identifying the lane lines are mentioned below.

*The test image has been converted to gray scale image for simpler processing.
*The resulted gray scale image has been "Gaussian Blur"red in order to smoothen the edges.
*Edges in the resulted image has been extracted using the Canny Edge detector operator.
*Unnecessary region in resulted image with edges has been masked.
*Lane lines in the masked image has been identified and highligted drawing the hough line transform.
*The resulted line image has been stacked over the orginal image which show the highlighted lane lines.

In order to mark the lane lines in a video, the image frames of the test video is fed to the above pipeline for processing.

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale in order to minimize the complexity of the processing data. This grayscale conversion reduces the number of channel from 3 to 1 which makes further processing simpler.

[image1]: test_images_output/grayscale.jpg "Grayscale"
 
Then, I smoothen the grayscale image by using Gaussian smoothen technique. This helps in achieving desired degree of blurness on the sharp edges of the image. The intensity of blurness can be controlled by 'Kernel_size' which takes odd number(1,3,5,7...) as input

[image2]: test_images_output/Gaussianblur_img.jpg "Gaussian Blur"

Later, I applied the Canny edge detection technique to identify the edges in the image. The Canny edge detector is an edge detection operator that uses a multi-stage algorithm to detect a wide range of edges in images. The intensity of edge detection can be controlled by low_threshold and high_threshold parameters.

[image3]: test_images_output/cannyEdge_img.jpg "Canny Edge Detection"

then I applied the mask apart for the region of interest on the resulted edge image in above step.

[image4]: test_images_output/Masked_edge_img.jpg "Masked Edge Detection"

Then, I have used Hough line transform technique to draw a line on identified lane lines.The Hough transform is a feature extraction technique used in image analysis, computer vision, and digital image processing. The purpose of the technique is to find imperfect instances of objects within a certain class of shapes by a voting procedure.

Later I extrapolate the 'long dash' or 'dot dash' lines identified in canny edge image to continuous line with the help of linear regression technique in machine learning. Linear regression are often fitted with 'least square' approach. I applied below pipeline to extrapolate long dash lines on lane.

 *I split left and right lines on identified lane lines based on the positive and negative slope.
 *Then I applied the linear regression techinique on the coordinates indivdually on left and right lanes of the hough image.
 
[image5]: test_images_output/Hough_line_img.jpg "Extrapolated Hough Line Image"


### 2. Potential shortcomings with your current pipeline


One potential shortcoming with the above pipeline would be the incompatiblity with varying image frame size. In above pipeline, the vertices for 'region mask' is hard coded for image frame - 540x960 with real coordinates of the area of interest. This makes this pipeline incompatible with videos of different frame size.

Another shortcoming could be the inefficiency of above pipeline to identify the lane line accurately in curved roads.

### 3. Possible improvements to your pipeline

A possible improvement would be to configure the vertices of interested region with respect to image size instead of hard coding the coodinates.
