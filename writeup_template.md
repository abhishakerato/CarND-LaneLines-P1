# **Finding Lane Lines on the Road**

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/rawImage1.jpg "Raw Image"
[image2]: ./test_images_output/grayscale1.jpg "Grayscale"
[image3]: ./test_images_output/guassian1.jpg "Gaussian Smoothened Grayscale"
[image4]: ./test_images_output/canny1.jpg "Canny applied grayScale"
[image5]: ./test_images_output/region1.jpg "Region selected Canny"
[image6]: ./test_images_output/hough1.jpg "Hough transformed"
[image7]: ./test_images_output/final1.jpg "Original with Hough overlay"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 5 steps. The first step was to convert the raw image that was read in to grayscale to extract a single colour channel. I then performed gaussian smoothening, which is equivalent to passing the image through a low pass filter. The third step was to apply the Canny Edge Detection (transform) on the single-channel grayscale image. The thresholds for edge detection were chosen based on trial and error, with the goal of ensuring that the lanes edges are detected clearly. I then defined a region of interest - a fixed quadrilateral area of the image that encompasses the lane markings. The rest of the image is ignored and the pixels are set to black. I attempted to simplify the definition of the vertices of the region of interest using a function quadVertices(). The final step was to apply the Hough Transform on this region-selected image and overlay the identified lane markings on the original image. The Hough Transform parameters were also chosen by trial and error, applying the pipeline on all the test images and selecting the average.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by identifying that the left and right lane lines have opposing slopes. I expanded the draw_lines() function to first, classify all the detected lines from the Hough Transform into positive and negative slopes. Second, I applied the constraint that the lane lines must start at the base of the image. Third was to use the line equation (y = Ax + B) to identify the x and y coordinates of the end points of the line.

The images shown below give an overview on the 5 steps of the pipeline:
![alt text][image1]

#### Step 1:
![alt text][image2]

#### Step 2:
![alt text][image3]

#### Step 3:
![alt text][image4]

#### Step 4:
![alt text][image5]

#### Step 5:
![alt text][image6]

#### Final Output:
![alt text][image7]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road has a higher degree of curvature. The current pipeline fails to detect the lanes when applied to the optional challenge video.  

Another shortcoming could be when there is traffic. If, for example, there are cars within the region of interest, then the pipeline would fail.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to vary the region of interest based on curvature of the road.

Another potential improvement would be to improve the draw_lines() function in that that it currently draws only "lines" and not curves. Therefore, to be able to detect and draw lane lines on curvy roads, the function would have to be improved.
