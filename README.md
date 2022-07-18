# ECE 6460 Homework #5

The purpose of this assignment is to enhance the student's understanding of the subsystems covered in lecture and homework assignments 2, 3, and 4. Additionally, this assignment provides a hands-on example of configuring the runtime configuration of an autonomous vehicle software system using ROS launch files.

## Due Date
This assignment is due on Sunday, December 15th at 12:00pm. The grade for this assignment will be based on the latest commit on GitHub at this time, or it will be zero if there are no commits.

## Provided Files
- Initial `homework5.launch` that must be modified to complete the assignment
- Initial `homework5.rviz` that must be configured in Rviz to display the required visualization elements

## Requirements
### 1. Configure Runtime System [75 / 100]
The initial state of `homework5.launch` brings a Gazebo simulation of the Dataspeed car with the following:

- LIDAR sensor on the front bumper
- Monocular camera in the windshield
- GPS route that generates the target trajectory for the vehicle
- Adaptive cruise control program that sends the final speed and steering commands to the simulator.

Your task is to add the following nodes to the `homework5.launch` file:

- [5 / 75] Your Homework 2 node to follow the target trajectory
- [5 / 75] Your Homework 3 node to segment LIDAR data to detect the traffic vehicles
- [5 / 75] Your Homework 4 node to filter the detected traffic vehicles and estimate their relative velocity
- [10 / 75] The monocular vision example node to detect the lane markings and project them onto the ground plane

Once set up properly, launching `homework5.launch` should make the vehicle successfully accomplish the following:

- [15 / 75] Follow the GPS route as it did in Homework 2
- [15 / 75] Avoid crashing into the traffic vehicles by detecting them and adjusting speed accordingly
- [20 / 75] Detect the lane markings on the road and project them onto the ground plane for visualization in Rviz

In addition to modifying `homework5.launch`, you can make changes to your homework nodes to fulfill the above objectives.

### 2. Set up Rviz Configuration [25 / 100]
Launching `homework5.launch` opens Rviz and loads the Rviz configuration file `homework5.rviz`. Your task is to add the following visualization components to the display:

- [3 / 25] TF frames
- [3 / 25] Raw point cloud from the simulated LIDAR (`sensor_msgs/PointCloud2` topic)
- [3 / 25] Raw image from the simulated camera (`sensor_msgs/Image` topic)
- [3 / 25] Detected object bounding boxes from your Homework 3 node (`avs_lecture_msgs/TrackedObjectArray` topic)
- [3 / 25] Kalman filter tracking markers from your Homework 4 node (`avs_lecture_msgs/TrackedObjectArray` topic)
- [3 / 25] Detected lane markers from the monocular vision example node (`visualization_msgs/MarkerArray` topic)
- [7 / 25] Configure Rviz to use the vehicle's footprint frame as its fixed reference frame.

Finally, save the Rviz configuration settings to update `homework5.rviz`.

### 3. Submitting the Assignment
Before committing your changes to submit the homework, be sure to:

- Test the system thoroughly by launching `homework5.launch` and make sure the system behaves properly according to the specifications in Section 1.
- Double-check your additions to the Rviz display and make sure they appear correctly while the simulation is running.
- If you make any changes to your software for Homework 2, 3, or 4, make sure you commit those changes to the corresponding repository.
- Commit your changes to both `homework5.launch` and `homework5.rviz` to your Homework 5 repository.

## Hints

### Modify Homework 3
The simulated LIDAR point cloud is much less dense than the point cloud from the real sensor used in Homework 3. You can account for this by reducing the number of neighboring points to search during the normal vector computation procedure. Change the argument of `setKSearch` from 50 to 20. This will result in better performance.

### Use the Tools!
Make use of the tools built into ROS to help see what is happening in the system and to debug topic disconnects or TF frame lookup problems. For example:

- Use `rqt_graph` to see how nodes and topics interact with each other.
- Use the TF tree viewer `rosrun rqt_tf_tree rqt_tf_tree` to see the structure of the TF frames of the system.
- Take advantage of the `<remap>` capability in launch files to change the names of topics that nodes subscribe or publish to without having to change or compile any code.
- Use `<param>` in launch files to pass parameters to nodes. This could be useful if someone were to change the name of a camera and a node needs to know what that name is... :wink:

### Slides
Slide 4 of the System Design Overview lecture slides might be a helpful reference.
