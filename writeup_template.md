# **Finding Lane Lines on the Road**

## Writeup Template

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied the Gaussian blur with a 3x3 filter on the output of the grayscale. 
After that I applied canny edge detection method to detect edges. Using Gaussian blur as a pre processing step to the canny method helps remove the unwanted edges(noisy) from the image.
Then I used image masking and extract the region of interest from my image.
Then I applied hough line transform on the resulted masked image to find out the line based on the votes we get for a particular grid in the hough space.

References:
1) https://dsp.stackexchange.com/questions/10057/gaussian-blur-standard-deviation-radius-and-kernel-size
2) https://alyssaq.github.io/2014/understanding-hough-transform/
3) https://medium.com/@esmat.anis/robust-extrapolation-of-lines-in-video-using-linear-hough-transform-edd39d642ddf
4) http://ottonello.gitlab.io/selfdriving/nanodegree/python/line%20detection/2016/12/18/extrapolating_lines.html
5) http://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_houghlines/py_houghlines.html

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by taking the slope of the every line obtanined from the hough_lines() function. Slopes thus obtained can be distinguished based on whether they are positive or negative. Lines belong to the left lane have a positive slope, and the lines belong to the right lane have a negative slope. Hence based on the slope it is easy to differentiate left and right lane lines. Now to extrapolate the line points, I averaged the lane lines and obtained the top and botton line points for each left and right lanes.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the pipeline runs on a video with curved lanes. For instance, the current pipelines is generating poor results on the video in the challeng section.

I think, another shortcoming could be to deal with occlusions(ex: vehicle in front) and illumination changes. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a logic that can detect the change in direction of the curve.

Another potential improvement could be to develop a logic that can detect transient conditions, such as changing lanes.
