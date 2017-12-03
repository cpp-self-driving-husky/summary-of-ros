# summary-of-ros
## Introduction
This document is meant to be a quick reference guide to using ROS. It gives definitions and uses for many tools in ROS and is a summary of the information in the [ROS Tutorials](http://wiki.ros.org/ROS/Tutorials) and [ROS Concepts](http://wiki.ros.org/ROS/Concepts) pages.

## What is ROS?
ROS is an open-source, meta-operating system for robots, that provides the services that you would expect from an operating system. Some of these include but are not limited to hardware abstraction, message-passing between processes, and package management. ROS also provides tools and libraries for the use of code across multiple computers. It runs on Unix-based platforms (Uduntu 14.04 on the Husky A200) and has many different distributions (ROS Indigo on the Husky A200).

## ROS Filesystem
* **Packages:** The main software organization unit of ROS Code. They can contain libraries, nodes, scripts, and any other artifacts
* **Manifests:** Provide information about a package. Serves to define dependenies between packages and to capture meta information about the package like version, maintainer, license, exported packages, etc.
* **Message Types:** Define the message structures that are sent in ROS
* **Service Types:** Define the service structures of the request and response data in ROS
### ROS Filesystem Tools
* **rospack:** Allows the user to get information about packages
    * Options for rospack
        * **find:** Returns the path to a package
            * Usage: rospack find [package_name]
        * **depends1:** Returns the first-order dependencies of a package
            * Usage: rospack depends1 [package_name]
        * **depends:** Recursively returns all nested dependencies
            * Usage: rospack depends1 [package_name]
* **roscd:** Chagnes directories directly to the package based on the name of the package that is given
    * Usage: roscd [locationname[/subdir]]
    * Options for roscd
        * **log:** Takes you to the directory where ROS stores log files (If there are any log files present)
* **rosls:** ls directly in a package by the name rather than the absolute path
    * Usage: rosls [locationname[/subdir]]

## ROS Computation Graph Level
The peer-to-peer network of ROS processes that are processing data together is known as the Computation Graph. Data can be provided through the basic concepts of nodes, Master, Parameter Server, messages, services, topics and bags.
* **Nodes:** An executable that performs calculations and communicates with other nodes
    * Written with the use of a ROS Client Library
        * **Client Library:** Allow nodes that are written in different languages to communicate
            * rospy = Python client libraries
            * roscpp = C++ client libraries
* **Master:** Allows for nodes to be able to communicate with each other. Nodes could not find each other, exchange messages, or invoke services without the use of Master.
* **Parameter Server:** Data is stored in a central location by a key and is currently part of Master.
* **Messages:** Messages are data structures (much like C structs) that are used by nodes to communicate. Messages ccan consist of primitive types and arrays of primitive types. Nodes use messages to subscribe and publish to topics.
* **Topics:** Topics are used so that nodes can communicate data. Nodes send data by publishing to topics and then receive data by subscribing to topics. Topics are given a name and this name is used to identify the type of data that the topic containes. There can be multiple concurrent nodes subscribed to and publishing to the same topic, and a single node can be subcribed to or publishing to multiple different topics.
* **Services:** Services allow for request/reply interactions to be completed. One node can offer a service with a given name and then a client node can use the service by sending a request message to the service andwaiting for a reply message.
* **Bags:** Saing and playing back ROS message data can be done through the use of bags. They are an important mechanism for storing data and make storing sensor data for developing and testing algorithms easier.
* **rosout:** This is the ROS equivilant to stdout and stderr.
* **roscore:** This is the Master + rosout + Parameter Server all in one.

## rosnode
rosnode is used to get information about nodes in ROS
* Options for rosnode
    * **list:** List shows the current nodes that are active
        * Usage: rosnode list
    * **info:** Returns information about a specific node like the publications, subscriptions, and services
        * Usage: rosnode info [node_name]
    * **ping:** Returns information indicating that the node is running
        * Usage: rosnode ping [node_name]
    
## rosrun
rosrun is used to run a node within a package through the use of the package name
* Usage: rosrun [package_name] [node_name]

## rostopic
rostopic is used to get information about topics in ROS
* Options for rostopic
    * **-h:** Shows the available sub-commands for rostopic
    * **echo:** Shows the data published on a topic
        * Usage: rostopic echo [topic]
    * **list:** Shows all topics subscribed to currently
        * Usage: rostopic list
    * **type:** Returns teh message type of the topic being published
        * Usage: rostopic type [topic]
    * **pub:** Used to publish data to a topic
        * Usage: rostopic pub [topic] [msg_type] [args]
    * **hz:** Returns the rate at which the data is published
        * Usage: rostopic hz [topic]
    
## rosmsg
rosmsg shows the details of a message in ROS
* Options for rosmsg
    * **show:** Shows the details of the message
        * Usage: rosmsg show [msg_type]
    
## rosservice
rosservice allows nodes to send a request and receive a response from another node
* Options for rosservice
    * **list:** Shows infromation about the active services
        * Usage: rosservice list
    * **call:** Call the service with the provided args
        * Usage: rosservice call [service] [args]
    * **type:** Returns the type of the service
        * Usage: rosservice type [service]
    * **find:** Find services by the service type
        * Usage: rosservice find [type]
    * **uri:** Print the service ROSPC uri
        * Usage: rosservice uri
    
## rosparam
rosparam stores and manipulates data on the ROS Parameter Server using YAML markup language for its syntax. Data can be integer(1), float(1.0), string(one), boolean(true), list([1, 2, 3]), and dictionaries({a:b, c:d}).
* Options for rosparam
    * **set:** Set parameters
        * Usage: rosparam set [param_name]
    * **get:** Get parameters
        * Usage: rosparam get [param_name]
    * **load:** Loads parameters from file
        * Usage: rosparam load [file_name] [namespace]
    * **dump:** Dump parameters to a file
        * Usage: rosparam dump [file_name] [namespace]
    * **delete:** Delete the parameters
        * Usage: rosparam delete
    * **list:** List the parameter names
        * Usage: rosparam list
    
## roslaunch
rosluanch starts nodes as defined in a launch file
* Usage: roslaunch [package] [filename.launch]

## Catkin Packages
Catkin pakages must contain the following:
* A Catkin compliant package.xml file that contains meta information about the package
* A CMakeList.txt file which uses Catkin
* It must have its own folder
### catkin_make
catkin_make combines the calls cmake and make when working in a standard CMake workfloa. It it will build any catkin projects in the current directory and it will create several new direcctories (build, devel, and src)
* Usage: catkin_make [make_target] [-DCMAKE_VARIABLES=...]
