# \<ros-rviz\>
[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/jstnhuang/ros-rviz)

A Polymer element for ROS visualization.
Versions 1+ are hybrid elements that support Polymer 1 and Polymer 2.

- [API Documentation](https://www.webcomponents.org/element/jstnhuang/ros-rviz/elements/ros-rviz)
- [User guide](https://github.com/jstnhuang/ros-rviz/wiki/User-guide)
- [Demo](https://www.webcomponents.org/element/jstnhuang/ros-rviz/demo/demo/index.html).
  Note that the demo requires a secure websocket server, since it is served over HTTPS.

To run the demo, run `rosbridge`, `tf2_web_republisher`, and the interactive marker proxy as needed.

## Quick start

1. Install dependencies:

        curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.4/install.sh | bash
        . ~/.bashrc
        nvm install node
        npm install -g bower polymer-cli

1. Clone this repo:

        git clone https://github.com/osrf/polymer-ros-rviz
        cd polymer-ros-rviz

1. Install:

        bower install

1. Serve demos and docs:

        polymer serve --hostname 0.0.0.0

   > The hostname is recommended if you're running from inside docker.

   > By default, it will serve on port 8081

1. View demo:

    http://localhost:8081/components/ros-rviz/demo/index-no-data-binding.html

    > The `no-data-binding` demo is recommended since it works on Firefox, see issue #1

So far, there's nothing running in the backend, so the websocket has nothing to
connect to.

Let's run an example:

1. Install dependencies (assumes you already have core ROS Kinetic packages installed):

        sudo apt install -y \
          ros-kinetic-pr2-gazebo \
          ros-kinetic-rosbridge-server \
          ros-kinetic-tf2-web-republisher

1. Start a Gazebo simulation of a PR2 robot, this will open a Gazebo window with
   a PR2 in an empty world.

        roslaunch pr2_gazebo pr2_empty_world.launch

1. Start the ROSBridge websocket server, which defaults to port 9090:

        roslaunch rosbridge_server rosbridge_websocket.launch

1. Start a TF2 republisher for the web:

        rosrun tf2_web_republisher tf2_web_republisher

1. Now refresh the browser. This time no error should be printed to the console.

1. Click on the `+` and add a "Robot model", the PR2 should show up in the scene.

    > Note that the meshes may show up dark due to issue #3.


## Tests

To run the tests, run the following:

```
roscore
roslaunch rosbridge_server rosbridge_websocket.launch
polymer test
```