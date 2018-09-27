# ros-docker
Integrating ROS with docker

# Usage

#### Install Docker:

  - [Mac](https://docs.docker.com/docker-for-mac/install/#install-and-run-docker-for-mac)

  - [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

#### Build docker image:

```docker build --tag ros-docker . ```

#### Run image:

```docker run -it ros-docker```

# Customize

Run a package that is located in you computer in the ros container

#### Copy your own package
```
RUN catkin_create_pkg YOUR_PACKAGE_NAME
COPY PACKAGE_LOCATION_ON_YOUR_COMPUTER /catkin_ws/src/YOUR_PACKAGE_NAME
```

#### Run your package

```
docker run -it ros-docker rosrun YOUR_PACKAGE_NAME EXECUTABLE
```

More information about running: https://hub.docker.com/r/library/ros/
