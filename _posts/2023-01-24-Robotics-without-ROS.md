---
title: "Robotics without ROS"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard
---


  On the first day at my first job fresh out of grad school, I was informed that “This vacuum bot doesn’t use ROS” and my mind was blown. This revelation was not so much shocking as it was enlightening. During my time in graduate school studying Robotics Engineering, I was heavily encouraged or even pressurized to learn ROS. However, this experience showed me that not all companies and projects rely on it.

  Robot Operating System (ROS) is a popular open-source framework for robotics software development. It provides a set of tools and libraries for building, deploying, and running robots, and has become a standard in the robotics community. However, ROS is not the only option for building robotics systems. 

In this blog post, we will explore some alternative options for robotics development that do not rely on ROS.

1. Python-based frameworks: Python is a popular programming language for robotics, and there are several frameworks available for building robots without ROS. Some examples include:
    - PyRobot: PyRobot is a lightweight, open-source framework for building robots using Python. It provides a set of tools for controlling robots, including a robot simulator and a control library.
    - RobotPy: RobotPy is a Python-based framework for building robots for the FIRST Robotics Competition. It provides a set of libraries for controlling motors, sensors, and other hardware.
    - pyControl: pyControl is a framework for building robots using Python and the Raspberry Pi. It provides a set of libraries for controlling motors, sensors, and other hardware.
2. Hardware-specific frameworks: Some robot manufacturers provide their own frameworks for building robots without ROS. These frameworks are often specific to the manufacturer's hardware and may not be compatible with other robots. Examples include
    - Lego Mindstorms EV3: The Lego Mindstorms EV3 is a popular robotics kit for building robots, and it comes with its own software for programming the robots.
    - Arduino: Arduino is an open-source microcontroller platform that can be used for building robots without ROS. It provides a set of libraries for controlling motors, sensors, and other hardware.
3. Middleware frameworks: Middleware frameworks provide a layer of abstraction between the robot's hardware and the software that controls it. These frameworks can be used to build robots without ROS. Examples include:
  - YARP: The Yet Another Robot Platform (YARP) is an open-source middleware framework for building robots. It provides a set of libraries for controlling motors, sensors, and other hardware, and it can be used with a variety of programming languages.
  - OROCOS: The Open Real-time Control System (OROCOS) is an open-source middleware framework for building robots. It provides a set of libraries for controlling motors, sensors, and other hardware, and it can be used with a variety of programming languages.

<p>Most of the alternative options mentioned are open source libraries. Interestingly, there still exists one more, the most basic way to build robots. With some experience in path planning, sensor fusion, control systems and some low-level firmware communication with robot’s hardware, we can create a robot that can navigate in a dynamic environment avoiding obstacles. By not using ROS, a project can have more control over the specific functionality it uses and can be tailored to the specific needs of the application. I recently heard about a company called Mujin that has succeeded worldwide without using ROS. Even though I use ROS extensively, the possibility of Robotics without ROS is not just based on theory, but rather rooted in practicality.</p>

<!--more-->
