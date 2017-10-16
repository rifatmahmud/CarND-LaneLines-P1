###1. Identifying the correct lanes

At first the image is grayscaled and gaussian blur is applied to it. Then canny edge is applied to it. The given helper functions do a great job in finding edges. But to find the proper lane lines from all the edges is a challenge. So, I restricted the region of interest to a trapezoid coming from the base of the photo. The pipeline tries to find lines only on the edges inside that trapezoid. The trapezoid is marked by pixels- [40, 539], [460, 324], [500, 324], [920, 539]. This keeps out most of the noises out. Then lines are searched for in the region of interest and the lines are drawn in the original image.

###2. Getting the composite lane line markers

These lines are very segmented and sometimes have huge gaps. So, we need to extrapolate the whole lanes from these segmented lines. The lines are classified bases on sign of the slopes, as the each of the lane lines in the pair will have opposite signs. A check is put to exclude any lines parallell to x or y axis. Slopes in each of the groups are averaged and the average value is used for the composite lane lines. A pixel in the group is taken and the line equation is derived from the average slope. Then two pixels are calculated where they intersect the two parallerl lines of the trapezoid. Then a line is drawn between those two intersection points for each of the group with a high thickness. That is how we get the composite lane lines.

###3. Shortcomings of the pipelines:
	- It doesn't take into account for a scenario where the car's nose is moved away from the direction in an incident and it has to get back on the lane.
	- In case of traffic jam where too many cars around it might have a hard time finding the lane lines.
	- Very sharp 90 degree turns or u turns cannot handled by this pipeline as on those cases lane lines might be out of field of view of the camera for certain time.
	- It might have difficulties where lanes are marked by physical barriers rather than lines

###4. Possible impovements

	- Having a variable region of region of interest, if it falses to find lanes lines it looks in other possible regions.
	- Having a handling mechanism for sharp turns where lane lines might appear exactly in front of the camera.
	- In absence of a lane marker, detecting physical boundaries of the road.








