# ROS Library

**ROS Program Tree strcuture **<br />

my_cpp_library<br />
  |<br />
  |-include<br />
  |&emsp; &emsp;   |- my_cpp_library<br />
  |&emsp; &emsp;    &emsp;&emsp;   |  <br />
  | &emsp; &emsp;    &emsp;&emsp;  |- library_header.h<br />
  |-src<br />
  |&emsp;&emsp;    |- main.cpp<br />
  |&emsp; &emsp;   |- my_cpp_library.cpp  <br />   
  |<br />
  

**CMakeLists.txt**
-----------------------------------------------------------------------------------------------------

Changes in CMakeLists.txt

-----------------------------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.5)
project(my_cpp_library)

if(CMAKe version)
   |<br/>
   |<br/>
   |<br/>
   |<br/>
find_package(ament_cmake REQUIRED)


include_directories(include/my_cpp_library)
set(HEADER_FILES include/my_cpp_library/library_header.h)
add_library(my_lib src/my_cpp_library.cpp ${HEADER_FILES})

add_executable(main src/main.cpp)
target_link_libraries(main PUBLIC my_lib)

#install the executable in the lib folder to be seen by setup.bash 
install(TARGETS
   main
   DESTINATION lib/${PROJECT_NAME}/
)

#export the traget in our case it is a library
ament_export_targets(my_lib HAS_LIBRARY_TARGET)

#install  include/my_cpp_library to install/ include/my_cpp_library
intsall(
   DIRECTORY include/my_cpp_library
   DESTINATION include
)


#install the target
install(
   TARGETS my_lib
   EXPORT my_lib
   LIBRARY DESTINATION lib
   ARCHIEVE DESTINATION LIB
   RUNTIME DESTINATION bin
   INCLUDES DESTINATION include
)

ament_package()





**1. Testing **

Create a new folder tests inside my_package
```
cd ros2_ws/src/my_node
mkdir test

```
Then create main.cpp inside test folder
```
#include "gtest/gtest.h"
int main(int argc, char **argv)
{
  ::testing::InitGoogleTest(argc,argv);
  return RUN_ALL_TESTS();
}
```

Create another file in test/saving_account_test.cpp

Write the following code inside it
```
#include "gtest/gtest.h"
TEST(MyFirstTestSuite, MyFirstTest)
{
  EXPECT_TRUE(true);
}

```
  TEST is a Macro and takes 2 parameters   1. MyFirstTestSuite test suite and
  EXPECT_TRUE   is assertion and adding always true or successful. The test is going to fail
  and update CMakeLists.txt

```
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  find_package(ament_cmake_gtest REQUIRED)
  
  set(TESTFILES
     test/main.cpp
     test/saving_account_test.cpp
     )
     
   ament_add_gtest(${PROJECT_NAME}_test ${TESTFILES})
   target_link_libraries(${PROJECT_NAME}_test my_lib)
   
   install(TARGETS
      ${PROJECT_NAME}_test
      DESTINATION lib/${PROJECT_NAME}/
      )
      
      
     
     

endif()
```
-----------------------------------------------------------------------------------------------------

**2. Run Tests**

First compile 

```
cd ros2_ws
colcon build
```

Then test it for all workspace or for selected packages

```
colcon test
or
colcon test --packages-select my_cpp_library
```

to check whether the tests are successful or failed 
```
colcon test
or
colcon test --packages-select my_cpp_library
```

-----------------------------------------------------------------------------------------------------
**3. Install the ROS 2 Packages**

Update the apt repository cache.

```
sudo apt update
```

Install the Desktop version of ROS 2.
```
sudo apt install ros-foxy-desktop
```
-----------------------------------------------------------------------------------------------------
**4. Set up the Environment Variables **

Add foxy to your bash file.

```
echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
```

To check if it was added, type the following command, and scroll all the way to the bottom.:
```
gedit ~/.bashrc
```

To check ROS version 
```
printenv ROS_DISTRO 

  or
  
  env |grep ROS
```
-----------------------------------------------------------------------------------------------------
**5. Install few other tools**
```
sudo apt install -y python3-pip
pip3 install -U argcomplete
sudo apt install python3-argcomplete

```
** Install Colcon**
```
sudo apt install python3-colcon-common-extensions
```

** For autocomplte**
```
echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc
```

**For workspace realted setup**

```
echo "source ~/ros1_ws/install/setup.bash" >> ~/.bashrc
```
-----------------------------------------------------------------------------------------------------

**6. Test your Installation**

First Terminal 

```
ros2 run demo_nodes_cpp talker
```

Second Terminal 

```
ros2 run demo_nodes_py listener
```





