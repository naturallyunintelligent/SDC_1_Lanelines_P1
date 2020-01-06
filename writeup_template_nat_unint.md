# **Finding Lane Lines on the Road** 
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.

1) Convert the images to grayscale: <br/>
    `gray = grayscale(image)`<br/>
    
    [//]: # (Image References)
    [image1]: ./outputs/gray_output.jpg "gray"
    ![alt text][image1]

2) Blur the gray image: <br/>
    `kernel_size = 15` <br/>
    `blur_gray = gaussian_blur(gray, kernel_size)`
    
    [//]: # (Image References)
    [image2]: ./outputs/blur_output.jpg "blur"
    ![alt text][image2]

3) Detect edges using the opencv canny function: <br/>
    `low_threshold = 75` <br/>
    `high_threshold = 90` <br/>
    `edges = canny(blur_gray, low_threshold, high_threshold)`
    
    [//]: # (Image References)
    [image3]: ./outputs/edges_output.jpg "canny edges"
    ![alt text][image3]
    
4) Mask a ROI, using some chosen vertices: <br/>
    `vertices = np.array([[(0,image.shape[0]),(image.shape[1]/2,image.shape[0]/1.7), (image.shape[1]/2, image.shape[0]/1.7), (image.shape[1],image.shape[0])]], dtype=np.int32)` <br/>
    `masked = region_of_interest(edges, vertices)`
    
    [//]: # (Image References)
    [image4]: ./outputs/masked_output.jpg "masked"
    ![alt text][image4]
    
5) Convert edges to lines using hough space: <br/>
    `lines = hough_lines(masked, rho, theta, threshold, min_line_len, max_line_gap)`
    
    [//]: # (Image References)
    [image5]: ./outputs/lines_output.jpg "lines"
    ![alt text][image5]
    
6) Average the lines and extrapolate: <br/>
    In order to draw a single line on the left and right lanes, I modified the draw_lines() function to:<br/>
     - Calculate the gradient of each individual line identified<br/>
     - Group positive and negative lines together<br/>
     - Create arrays of line gradient, y-intercept and equivalent intercept at the frame of the picture<br/>
     - Calculate the mean of the gradients and intercepts to calculate a single start point and end point to draw a straight line over each detected lane lines.
  
    [//]: # (Image References)
    [image5]: ./outputs/lines_output.jpg "lines"
    ![alt text][image5]
    
    [//]: # (Image References)
    [image6]: ./outputs/weighty_output.jpg "lines"
    ![alt text][image6] 



### 2. Identify potential shortcomings with your current pipeline

A clear shortcoming is my "beginnerish" code in the modified draw lines function which I'm certain could be written more efficiently.

The challenge video demonstrates an issue right now where the lines plot in crazy positions, despite working on the other videos, so there is some debugging to do there!

Other potential shortcomings would be what would happen if/when ... 

 - Extreme corner to left or right, causing lines to be outside of ROI
 - Different lighting or shadowy conditions could mean lines aren't found in the canny edges step
 - Ditto for road surface: wet, snow, changing tarmac to concrete etc
 - No line markings present on road surface


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to deal with any of the above shortcomings, for example:
 - Refactor the code in the draw lines function
 - Adjust for lighting conditions
 - Adjust for changes in road surface
 - Adjust ROI when the horizon is changing
 - Deal with roads that aren't straight (i.e. extrapolate to curves rather than straight lines)
