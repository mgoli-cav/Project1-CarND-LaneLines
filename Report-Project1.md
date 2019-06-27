 # **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Reflection
### 1. Introduction.

My pipeline consisted of several steps. First, I worked on one single image so that I can detect the lanes. For that I performed the following steps:

- Reading the image using imread function. 
- Converting the RGB image to grayscale image.
- Removing the noise by applying Gaussian filter
- Applying an edge detector to detect the edges of the objects in the image.
- Applying a mask to select a region of interest
- Detecting the lanes using Hough transform
- Drawing lines on the line segments
- Applying the algorithm on a series of images.

### 2. Methods
In this section I go into more details on the different methods that I implemented to detect lanes in images and the video.

### 2.1 Obtaining line segments

To obtain the line segments, a Hough transform was applied to a section of image which was produced by canny edge detection routine. 
Hough transform 
First, I smoothed the image using Gaussian filter so noise are removed, and then I performed a Canny edge detection on the image. Doing so, will give me a binary image with ages of objects. Then I chose a region of interest by applying a mask to the image defined by a polygon formed from vertices. The rest of the image is set to black. Then I use the Hough transform to detect the lines using a set of parameters. 
Hough transform makes a grid of lines passed through the image and counts the number of pixels that overlaps with those lines. We should create a threshold for the number of votes a line gets before being counted as a line. Other parameters could also be set using trial and error to evaluate the quality or length of the lines. 

### 2.2 Drawing lane lines

The next task is to connect the detected lines segments on lanes and draw a solid line on those segments. For this purpose, we first categorize the lines with respect to their slopes to assigned them to the left or right lane lines. 
Then we average the line segments slops so that we could draw a one segment line that fits closely all the line segments in each lane line. 
In order to draw a single line on the left and right lanes, I modified the draw_lines() function. 

### 3 Video Pipeline

To find the lane lines on a video, the image pipeline is applied on video stream. With some tuning of the parameters the results look satisfactory

### 4. Identify potential shortcomings with your current pipeline

There are several shortcomings for this method of detecting lines. For example, if the lane curves as in the challenge video, this approach fails to produce accurate lane marking. Second, the method does not seem to be robust to color, disturbances such as undesired parallel lines, outside of the ROI lines, etc..
Another shortcoming could be how we select the ROI. It should be calibrated for different videos and this is not desirable.
### 3. Suggest possible improvements to your pipeline
A possible improvement would be to use colors as an additional feature to detect lines. 
Another potential improvement could be applying the Hough transform to the whole image so that we won't need to choose a ROI a Priory.

