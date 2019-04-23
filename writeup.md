# **Finding Lane Lines on the Road** 

## Writeup ouline

### 1. Project rubric
### 2. Reflection (my pipline)
### 3. Future work

---

### **1. Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road 
  - Does the pipeline for line identification take road images from a video as input and return an annotated video stream as output? (CHECK)
  - Has a pipeline been implemented that uses the helper functions and / or other code to roughly identify the left and right lane lines with either line segments or solid lines? (example solution included in the repository output: raw-lines-example.mp4) (CHECK)
  - Have detected line segments been filtered / averaged / extrapolated to map out the full extent of the left and right lane boundaries? (example solution included in the repository: P1_example.mp4) (CHECK)


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### **2. Reflection**

#### 1. My pipeline and understandings

Generate pipline can be described as: Input(RGB) -> Gray scale image -> Blur(denoise) -> Edge(binary) detection -> Region of interest -> Hough transform -> Draw lines 

Input(RGB) -> Gray scale image:
  - This part is easy to understand, instead of dealing with color image, dealing with only one channel image can save time
  
Gray scale image -> Blur(denoise):
  - Using Gaussian filter with kernel size 5. 
  
Blur(denoise) -> Edge(binary) detection
  - Using Canny detector (uint8 type result is need for Hough transform, Canny provides binary result)
  - Canny detection includes: ([OpenCV Document](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_canny/py_canny.html))
    - Smooth (did)
    - Compute gradient of using any of the gradient operators Sobel or Prewitt
    - Extract edge points: Non-maximum suppression. Looking for local maximum based on gradient magnitude and direcyion
    - Hysteresis Thresholding (gradient value): non-edge if < low_threshold, sure-edge if > high_threshold, pixels with gradient in between check if directly connect to edge

Edge(binary) detection -> Region of interest:
  - Put this step here is to decrease the computational cost for Hough transform. 
  - Draw ROI in image is helpful to visulaize the selected area
  
Region of interest -> Hough transform:
  - trade off between speed and resolution (angle resolution and rho resolution)
  - trade off between finding more edges and preserve main edge (min_length, min_votes, max_gap...)
  
Hough transform -> Draw lines:
  - Just draw it!


![alt text][image1]

#### 2. As part of the description, explain how you modified the draw_lines() function.


#### 3. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...

---

### **3. Future work**

A possible improvement would be to ...

Another potential improvement could be to ...
