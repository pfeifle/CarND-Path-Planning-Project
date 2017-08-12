Path Planning Project

The first thing which was done, was to detect whether there is a car in the own lane of the ego vehicle which is in front of the ego-vehicle and which might lead to a collision.
Thereto, the position of the ego vehicle was determined for the end of the already planned path coming from the last frame. If another vehicle at the point in time when the ego vehicle was at the end of the already computed path was less than 30 meters in front of the ego vehicle, a potential collision was detected.

If no potential collision was detected the speed of the ego car was increased in case it is still below the allowed speed limit.
If a potential collision was detected the speed was reduced and it was decided whether a lane change to a neighboring lane was possible. Whether a lane change is possible was detected in the same was as a collision. The ego vehicle future position was compared with the future position of the cars in the adjacent lanes. Iff no car is within +/- 30 meters of the ego vehicles potential future position in the adjacent lane, a lane change was triggered.

All the above computation was done in the frenet coordinate system. The lane number corresponds to the d-value in this coordinate system whereas the s-value is independent of the lane number.

Based on this behavioral decision which speed and which lane should be used, the new trajectory path is computed. The new path takes the remaining points of the previous path. Then new points are added at the remaining previous path in the following way.
The last two points of the previous path are used to compute the heading of the car. At the beginning the first two points are computed by using the CCP (current car position) and the heading and a "potential" point before is computed. 

Then new points are computed in front of the end of the previous points in distance of 30, 60 and 90 meters (rather roughly). This is done in the frenet coordinate system. These three points are then added in the global coordinate system at the end of the two last points of the previous path.  Next all of these 5 points are transferred to a local car coordinate system in which the first point has coordinates (0,0) and the heading is 0. Then a spine is computed through these five points.

After the spline is computed the remaining points, i.e. 50-(size of previous remaining path) points, are computed based on the spline and the desired velocity.

By reusing the remaining path and the new points coming from the spline it is guaranteed that the car moves smoothly.
 


