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

My pipeline consisted of 5 steps.

1) convert the images to grayscale
2) blur
3) edges using canny
4) mask a ROI
5) edges to lines using hough space
6) Average the lines and extrapolate

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


Potential shortcoming would be what would happen when ... 

extreme corner to left or right, causing lines to be outside of ROI
Different lighting or shadowy conditions could mean lines aren't found in the canny edges step
Ditto for road surface: wet, snow, changing tarmac to concrete etc
no line markings present on road surface


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to deal with any of the above shortcomings, for example:
adjust for lighting conditions
adjust for changes in road surace
adjust ROI when the horizon is changing
deal with roads that aren't straight (i.e. extrapolate to curves rather than straight lines)
