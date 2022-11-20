# ROS Foxy Installation on Ubuntu20.04

**ROS Installation Process **

I have added this ROS Installation steps for all the developers to reduce their effor

**Prerequisites**
-----------------------------------------------------------------------------------------------------

Ubuntu 20.04 / Ubuntu in a VirtualBox on Windows 10

-----------------------------------------------------------------------------------------------------

**1. Set the Locale**

To check locale use following command

```
locale
```
Then type the following coomands
```
sudo apt update && sudo apt install locales
```

We may face issue like: Waiting for cache lock: Could not get lock /var/lib/dpkg/lock. It is held by process 3945 In such cases we can kill that process

use follwing syntax
```
sudo kill -9 [process ID]
sudo kill -9 3945
```
```
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale
```
-----------------------------------------------------------------------------------------------------

**2. Add the ROS 2 Repositories**

Try following commands 

```
sudo apt update && sudo apt install curl gnupg2 lsb-release
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

Now let’s add the repository to the source list.

```
sudo sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
```

**3. Install the ROS 2 Packages**

Update the apt repository cache.

```
sudo apt update
```

Install the Desktop version of ROS 2.
```
sudo apt install ros-foxy-desktop
```

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

**5. Install few other tools**
```
sudo apt install -y python3-pip
pip3 install -U argcomplete
sudo apt install python3-argcomplete

```


**6. Test your Installation**

First Terminal 

```
ros2 run demo_nodes_cpp talker
```

Second Terminal 

```
ros2 run demo_nodes_py listener
```





