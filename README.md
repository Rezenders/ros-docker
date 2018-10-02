# ros-docker
Integrating ROS with docker

# Usage

#### Install Docker:

  - [Mac](https://docs.docker.com/docker-for-mac/install/#install-and-run-docker-for-mac)

  - [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

#### Build docker image:

```$ docker build --tag ros-docker . ```

#### Run image:

```$ docker run -it ros-docker```

# Run Demo Application

The demo application consist in an executable that publishes keys strokes pressed (key_publisher.py) and another executable that reads those published keys (keys_to_twist.py) and transform them into velocity commands.

First a docker network must be created, run:

```$ docker network create ros_net```

Next, roscore must be initialized, run:

```$ docker run -it --rm --net ros_net  --name master --env ROS_HOSTNAME=master ros:melodic roscore ```

Now, the desired applications can be run as following:

Key publisher:

```$ docker run -it --rm  --net ros_net  --name key_publisher --env ROS_HOSTNAME=key_publisher --env ROS_MASTER_URI=http://master:11311 ros-docker  rosrun keyboard_driver key_publisher.py ```

Key to twist:

```$ docker run -it --rm --net ros_net --name keys_to_twist --env ROS_HOSTNAME=keys_to_twist --env ROS_MASTER_URI=http://master:11311 ros-docker  rosrun keyboard_driver keys_to_twist.py ```

If you want to inspect the data being exchange by ros you can run another container without running any commands, as follows:

```$ docker run -it --rm --net ros_net  --name echo --env ROS_HOSTNAME=echo --env ROS_MASTER_URI=http://master:11311 ros:melodic```

Then run rostopic, rosmsg etc.



# Customize

Run a package that is located in you computer in the ros container

#### Copy your own package
```
RUN catkin_create_pkg YOUR_PACKAGE_NAME
COPY PACKAGE_LOCATION_ON_YOUR_COMPUTER /catkin_ws/src/YOUR_PACKAGE_NAME
```

#### Run your package

```
$ docker run -it ros-docker rosrun YOUR_PACKAGE_NAME EXECUTABLE
```

More information about running: https://hub.docker.com/r/library/ros/
