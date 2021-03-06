# The Code Model
![image](https://github.com/kangcshin/Path-Planning/blob/master/Screenshot_from_2017-08-15_15-00-37.png)
### Track
The drive track is a loop made of sparse waypoints, so there are places on the track where the waypoints tend to get bunched up which then cause acceleration and jerk issues when the path planning model just uses the regular X,Y track coordinates. 
### Coordinates
Instead of using the regular X,Y coordinates, S,D coordinates, also known as **Frenet coordinates**, is used. 
The S indicates the logitudinal displacement along the road and D indicates the lateral displacement from the yellow middle line. 
### Smoothing movements
To minimize the jerk issues, **spline** is used to smoothly connect the waypoints(usage of anchor points as discussed in the walkthrough), resulting in smooth vehicle path.
### Generating Drive Path
To actually generate the vehicle path, the model uses sensor fusion data. 
The incoming data includes other vehicles and their positions in reference to time. 
Reference velocity of the target vehicle is determined by presence of other vehicles in front of the target vehicle. 

The max speed limit is set to 49 miles per hour but if the target vehicle approaches another vehicle, then the target vehicle slows down (before implementing lane changing).
### Dividing Track into Lanes
The track is made of three four-meter lanes. In terms of Frenet coordinate, D, the lateral displacement from the yellow middle line, 0 < D < 4 is lane 1. 4 < D < 8 is lane 2 and 8 < D < 12 is lane 3. 
### Start the Engine!
The target vehicle starts from lane 2, the middle lane and tries to drive in the same lane untill it approaches a slower vehicle in the same lane. When a slower traffic is encountered, the vehicle first checks the left lane and its front and rear spaces in respect to the target vehicle. If there is not enough space, or the target vehicle is already in the left-most lane, the vehicle looks the right. If front and rear spaces are greater than the space needed for the target vehicle to safely enter into the new lane, change lane flag is triggered, changing the target lane to the new lane. 

The vehicle successfully drives aroud the track without any flag for over 4.32 miles. 

Video: https://youtu.be/9-lzesHC8Uk
