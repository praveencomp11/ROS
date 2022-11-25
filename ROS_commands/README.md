# All ROS Commands

**ALL ROS Commands are enlisted below**

**Execution Steps:**
-------------------

**ROS1**


  **To Start new ROS Engine**

```
    roscore
```

  **To Start talker**
  (Syntax: rosrun    package_name     executable_name     arg_list)
```
     rosrun roscpp_tutorials talker
```

  **To Start listener**
  (Syntax: rosrun package_name executable_name arg_list)
```
     rosrun roscpp_tutorials listener
```

**ROS2**

 **No need to start ROS Engine i.e. roscore**

```
    NA
```

  **To Start talker**
  (Syntax: ros2 run package_name executable_name arg_list)
```
     ros2 run demo_nodes_cpp talker
```

  **To Start listener**
  (Syntax: ros2 run package_name executable_name arg_list)
```
     ros2 run demo_nodes_cpp listener
```


**To Start Turtlesim:**
-------------------

**ROS1**


  **To Start new ROS Engine Terminal1**

```
    roscore
```
 **Terminal 2**

```
    rosrun turtlesim turtlesim_node 
```
 **Terminal 3**

```
    rosrun turtlesim turtle_teleop_key 
```
![image](https://user-images.githubusercontent.com/10526517/204032974-106d9694-18a6-4a7e-9619-8ed2122cbb62.png)
		Node

![image](https://user-images.githubusercontent.com/10526517/204033034-3deca0a4-198b-45cb-ba42-74fc523ddebd.png)    ------> Node
![image](https://user-images.githubusercontent.com/10526517/204033081-1cb7a96a-d403-436a-8d18-af98bb6696be.png)    ------> Topic


**Setup Workspace:**
-------------------

**ROS1**
  
  To create workspace: Inside home_directory create catkin_ws folder
  
 ```
mkdir catkin_ws
cd catkin_ws
mkdir src
catkin_make

```
after this you can find two more folders (devel and build)  inside catkin_ws

**ROS2**
  
  To create workspace: Inside home_directory create ros2_ws folder
  
 ```
mkdir ros2_ws
cd ros2_ws
mkdir src
colcon build
```


**Create ROS package:**
-------------------

**ROS1**
  
  To create a package inside our workspace catckin_ws: Inside catkin_ws/src
  (driver -one package   navigation- one package) and different nodes for each package.
   one package is subpart of your application.  

Inside catkin_ws/src/  folder

```
catkin_create_pkg my_robot_controller rospy turtlesim roscpp std_msgs
```


**ROS2**
  
  Inside ros2_ws/src folder
 ```
ros2 pkg create ros2_app_py –build-type ament_python –dependencies rclpy std_msgs
```
**Create Ros services  red color represents addition of that name**
-------------------------------

**ROS1**
  To create a ros service inside our workspace catckin_ws: Inside catkin_ws/src
  Create a package name assignment_service 
  Inside catkin_ws/src/ assignment_service
  ```
catckin_create_pkg  assignment_service rospy roscpp std_msgs
cd assignment_service
mkdir srv
rm -rf include/ src/

``` 


**Inside assignment_service open packagae.xml**
``` 
<build_depend>  message_generation </build_depend>
<exec_depend> message_runtime <exec_depend>
``` 
**Inside assignment_service open CMakelists.txt**


add message_generation
``` 
find_package(Catkin REQUIRED COMPONENT
 message_generation
)
``` 

**Uncomment complete generate_message following **
``` 
generate_messages(
) 
``` 

**Uncomment one line and add message runtime **
``` 
catkin_package (
    uncomment CATKIN_DEPENDS roscpp rospy std message_runtime
)

``` 

**Then add srv folder**

catkin_ws/src/ assignment_service> mkdir srv
inside catkin_ws/src/ assignment_service/srv folder 

gedit MultiplyService.srv 


```
int64 a
int64 b
---
int64 sum

```

**Create Server (CPP file)**

Create package to write server and client inside catkin_ws/src/
catkin_ws/src/ >  catckin_create_pkg  multiplication_assignment rospy roscpp std_msgs
catkin_ws/src/ > cd multiplication_assignment/src
catkin_ws/src/ multiplication_assignment/src> gedit multiply_two_int.cpp

Inside catkin_ws/src/ multiplication_assignment/Cmakelist.txt


find_package(catkin REQUIRED PACKAGE
   assignment_service
)
add_executable(node_name     src/multiply_two_int.cpp)
target_link_libraries(node_name     ${catkin_libraries})





**Commands to debug**
``` 
rosrun
rosrun ping name_of_node
rosrun info name_of_node

``` 

**ROS2 Commands**
``` 
ros2 interface list
ros2 node list
ros2 topic list
ros2 topic echo /chatter

``` 
**ROS1 commands**

``` 
rosnode list
rostopic list

``` 







  
