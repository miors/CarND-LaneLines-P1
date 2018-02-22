# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road.
* Reflect on your work in a written report

---
### Note
All challenges were attempted including the 'Optional' challenge

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 9 steps. 
1. First, I masked the white colour
<img src="pipeline/output_mask_white.jpg" alt="White Mask" width="512">

2. After that I masked the yellow colour
<img src="pipeline/output_mask_yellow.jpg" alt="Yellow Mask" width="512">

3. Combined white and yellow mask
<img src="pipeline/output_masked_combined.jpg" alt="Combined Mask" width="512">

4. Then I applied the combined mask to the images
<img src="pipeline/output_masked_image.jpg" alt="Combined Mask" width="512">

5. The images were converted to grayscale
<img src="pipeline/output_gray.jpg" alt="Grayscale" width="512">

6. I applied Gaussian smoothing
<img src="pipeline/output_gaussian.jpg" alt="Gaussian" width="512">

7. I subsequently applied Canny Edge Detection to detect edges
<img src="pipeline/output_edges.jpg" alt="Canny" width="512">

8. Then I created region of interest of the left and right lines that I was interested in (+ their top and bottom boundaries)
<img src="pipeline/output_target.jpg" alt="Region Of Interest" width="512">

9. Later on I calculated a list of lines using Hough Transform and extrapolated/thickened the lines accordingly. In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:<br />
  
  * Iterating each line
  * Calculating its slope
  * Finding the center x, y position of the line
  * If the calculated slope fell within the specific boundary values, calculated values of both slope and position were added into separate lists
  * Then I calculated average slope and average center position
  * Using the average slope and center positions and knowing the top and bottom y positions that I wanted, I calculated the top and bottom x positions using y-y1 = m(x-x1) formula
  * Subsequently, I called cv2.line method passing the original image, coordinates of both points, color and thickness of the line to be drawn
<img src="pipeline/output_lines.jpg" alt="Hough Lines" width="512">

9. Finally I blended the lines and the original image
<img src="pipeline/output_result.jpg" alt="Result" width="512">

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is no line on the road as the algorithm heavily depends on the ability to detect presence of line 

Another shortcoming could be shadows, light and darkness could potentially affect the algorithm as it heavily relies on presence/ absence of colours


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to instead of using RGB channel, we could use HSV channel and target saturation or value (brightness) channels instead

Another potential improvement could be to reduce the range of values the calculated slopes could have as this would reduce the jerkiness of the drawn red lines on the right and left lanes.
