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

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I used the gaussian_blur function with a kernel size of 5. The third step consisted of using the canny edge detection helper function on the blurred image. After that the vertices that are going to be used for my region of interest mask were found by using the image size and limits established in the preivous lessons. Once the vertices were found, the mask was applied. The fifth step was to apply the hough transform to detect the lines based on a parameter set again from the previously lessons. The final step was to apply the weighted img function to draw the weighted lines on the image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function which is called within the hough_lines function above by first determining if the hough points were from the left or right line based on their slope, positive slope means they are from the right line and negative means they are from the left. Once all of the points are classified l or r, the avg of each set is taken so that the average slope of the line that contains all the points for each side can be determined. From this slope, the y-intercept can be found to complete the eq of the line for each side, on avg. With this equation, the line can be extended by evaluating the this function at the extents of our region of interest.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]: ./solidWhiteCurve_weighted_lines.jpg "Weighted Lines"


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when we violate our assumption that the lane lines a in a straight line of the from y=mx+b. If they have any curvature to them, they will not fit the assumed form.

Another shortcoming could be if the lines fall out of our region of interest, or if there are no lines present. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to fit the left/right hough line points to another quadratic equation to take into accound some line curvature. This could then be compared to the linear assumption and whatever equation has a better fit to the points should be used.

