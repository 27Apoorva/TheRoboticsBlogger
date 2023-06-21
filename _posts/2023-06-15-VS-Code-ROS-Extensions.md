---
title: "Exploration of VS Code Extensions for a ROS Developer"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard

excerpt_separator: <!--more-->

---

  <h1 style="text-align: center;margin-top:20px;margin-bottom-20px;" >Exploration of VS Code extensions for a ROS Developer</h1>

<!--excerpt.start-->
<p style="margin: 20px 3rem;">  
In the developers' community, there will always be an ongoing debate about the best IDE (Integrated Development Environment) out there, be it <a href="https://www.jetbrains.com/idea/">IntelliJ</a>, <a href="https://developer.apple.com/xcode/">Xcode</a>, <a href="https://www.eclipse.org/ide/">Eclipse</a>, <a href="https://atom.en.softonic.com/">Atom</a>, <a href="https://www.sublimetext.com/">Sublime Text</a>, or <a href="https://code.visualstudio.com/">Visual Studios</a>. But this blog isn’t about choosing the best IDE. I personally love to code in VS Code as a Robotics (ROS) developer. Being a ROS developer is way different than let’s say being a Web developer, especially in terms of the infrastructure available to make development easier.
When I first started coding, my VS Code setup was very minimal and the only extensions I used were specific to writing C++/Python code.  
Until now, I had been utilizing the command-line interface (CLI) to execute various functionalities within ROS.
</p>
<!--excerpt.end-->

<p style="text-align: left;margin: 20px 3rem;">This is my experience of exploring the extensions available for ROS development and comprehension of the missing functionalities. <br>
While doing research for this blog, the first thing I did was simply type ROS in the search bar for extensions in VS Code.</p>


<p style="text-align: left;margin: 20px 3rem;">
<img src="/assets/article5/image1.png" alt="article image 1" style="display: block;
        margin-left: auto;
        margin-right: auto;
        width: 50vmax;"/>  
The very first <a href="https://marketplace.visualstudio.com/items?itemName=ms-iot.vscode-ros">Visual Studio Code extension for ROS was by Microsoft</a> which provides ROS developers with a long list of features and functionalities like information about the ROS status and active topics, creating a ROS environment with sourced terminal, running ROS executables and launch files, and much more. This extension is readily available in the VS Code extensions marketplace and can be installed with a single click. 
</p>

<p style="text-align: left;margin: 20px 3rem;">Some cool functionalities that you can enjoy after installing this extension are:
</p>

<ul style=" margin: 20px 3rem;">
    <li><i>URDF Previewer</i><br>
    Developing a robot’s URDF in ROS is tedious as you need to write the URDF file as well as a launch file for the robot state publisher, joint state publisher, and RViz to then visualize the robot model. Every time you make changes to the URDF code, you need to execute the launch file and review it in RViz. This process is time-consuming, repetitive and adds frustration for the developer. ROS VS Code extension is there to make this process easier by providing a URDF previewer. URDF previewer functionality enables the visualization of the robot model alongside the .urdf file as shown below. You can make the edits to the URDF file and automatically see the live update of the robot model making development much faster.
    <img src="/assets/article5/image2.png" alt="article image 1" style="display: block;
        padding: 10px;
        margin-left: auto;
        margin-right: auto;
        width: 50vmax;"/>  
    </li>
    <li><i>Multiple ROS Nodes Execution</i><br>
    Traditionally, ROS developers have to open a new terminal tab to run multiple ROS nodes separately or even for running multiple ROS launch files. This also requires you to know the package name, executable names, etc. I have generally ended up trying to do tab completion to find the correct name of the node. The ROS VS Code extension makes this so much easier by automatically detecting and running the selected ROS packages via the executables or launch files. It will also take care of sourcing terminals with the correct path for successful execution.
      <img src="/assets/article5/image3.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>  
      <!-- <div align="center">Select a ROS command;&nbsp;&nbsp;&nbsp;Select a ROS package;&nbsp;&nbsp;&nbsp;Select a exectuable or launch file</div> -->
      </li>
      <li><i>Build Configurations</i><br>
      Say goodbye to the days when you needed to type the <code style='color:orange'>colcon build</code> command for building ROS workspace along with numerous arguments over and over again. ROS VS Code plugin provides a smoother process to build ROS workspaces. By specifying catkin/colcon commands and arguments inside the <code style='color:orange'>.vscode/tasks.json</code> file, you can simply run the <code style='color:orange'>colcon: build</code> command to build the workspace.
      <img src="/assets/article5/image42.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>  
      </li>
      <li><i>Debug Configurations</i><br>
      Finding bugs in the codebase is always much more painful than actually writing a new node. But with ROS VS Code extension, setting up a working debugging session is pretty straightforward. All you need to do is add a launch configuration <code style='color:orange'>(launch.json)</code> to the <code style='color:orange'>.vscode</code> folder in the ROS workspace then you can set a breakpoint for the node you want to debug. This extension also works with attaching the debugger to multiple nodes as <code style='color:orange'>launch.json</code> can take an array of nodes.
      <img src="/assets/article5/image55.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>  
      </li>
      <li><i>System Status</i><br>
      The ROS Status page functionality provides information about the ROS Core/ROS 2 Deamon, active nodes, topics, and services.
      <img src="/assets/article5/image6.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>  
      </li>
      <li><i>IntelliSense</i><br>
      The ROS VS Code extension provides IntelliSense syntax highlighting and code completion for URDF/Xacro files, .msg files, .srv files, and almost all other ROS-related file types.
      <img src="/assets/article5/image7.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>  
      </li>
</ul>

<p style="text-align: left;margin: 20px 3rem;">Another plugin that I found useful was <a href="https://marketplace.visualstudio.com/items?itemName=twxs.cmake">CMake by twxs</a>: 
<img src="/assets/article5/image8.png" alt="article image 1" style="display: block;
        padding: 10px;
        margin-left: auto;
        margin-right: auto;
        width: 50vmax;"/> 
</p>

<ul style=" margin: 20px 3rem;">
    <li><i>Syntax Formatting</i><br>
    You can use this CMake extension in VS Code to get syntax highlighting and code completion for your <code style='color:orange'>CMakeLists.txt</code> files.</li>
    <img src="/assets/article5/image9.png" alt="article image 1" style="display: block;
        padding: 10px;
        margin-left: auto;
        margin-right: auto;
        width: 50vmax;"/>  
</ul>

<p style="text-align: left;margin: 20px 3rem;">Although the current extensions for VS Code for Robotics provide tons of features for a faster, better development process, as an experienced and active ROS developer, I find some essential features still missing.</p>

<ul style=" margin: 20px 3rem;">
    <li><i>ROS Bag interface</i><br>
    Even for the most basic use case of let’s say tuning Slam Toolbox, I would look at the rosbag and play it several times to tune the algorithm to my satisfaction. ROS Bags are an essential block for any robotics system. There is only <a href="https://marketplace.visualstudio.com/items?itemName=lochbrunner.vscode-rosbag">one plugin</a> currently available for ROS 1 that can list the timestamps and the topics of the messages stored in the rosbag file. And the output of <code style='color:orange'>rosbag info filename</code>. For starters, I would like to at least have the ability to play rosbag using a click-on Play Button from the VS Code menu bar itself.
    </li>
    <li><i>Parameters in System Status</i><br>
    The change in the robot’s environment might create the need to update a few ROS parameters or maybe the customer wants the robots to operate at maximum speed compared to another customer. Maintaining and managing ROS Parameters can quickly become very painful. Although the ROS system status functionality can display active nodes, topics, and services, it does not show any information on active parameters in the computation graph.
    </li>
    <li><i>Joint Visualisation in URDF Previewer</i><br>
    While setting up the robot’s URDF, I generally try to test out the movement of each joint specifically the direction and axes of rotation. The current URDF previewer should also support Joint Visualisation for ease of debugging and verification of the robot model.
    </li>
    <li><i>Interactive ROS Graph Visualisation</i><br>
    I would love to have an extension that visualizes the ROS graph, displaying nodes, topics like tf, and connections in an interactive graph view.
    </li>
    <li><i>ROS Documentation Integration</i><br>
    Another cool to have extension could be a ROS Documentation Integrator. This extension can integrate ROS documentation directly into VS Code. It can allow you to quickly search and access ROS API documentation, tutorials, and examples without leaving the editor.
    </li>
    <li><i>Unit & Integration Tests</i><br>
    This is the one I most desperately need. An extension that can enable running and managing unit tests/integration tests (both Google tests and rostest) directly from VS Code. It can provide an intuitive interface for executing tests, viewing test results, and generating test reports.
    </li>
</ul>




<p style="text-align: left;margin: 20px 3rem;">I am really grateful to have installed the plugins available for ROS. If I have to put an estimate on the percentage of the time these plugins have saved, I would say it is about a 40% reduction in the overall development time especially for writing and executing ROS nodes. The ROS plugins aren’t perfectly developed yet as witnessed especially due to the unique challenges of visualization and data formats of ROS. As the robotics community is continuously growing, I have high hopes that the development environments would also improve over time. As of today, I highly recommend using the existing plugins to save time, especially for startups who struggle with maintaining one development process across the organization.</p>


  <p style=" margin: 20px 3rem;">If you liked the article, please buy me a <a style="
                    text-decoration:none;
                    display: inline-block;
                    outline: 0;
                    cursor: pointer;
                    text-align: center;
                    border: 0;
                    padding: 7px 16px;
                    min-height: 36px;
                    min-width: 36px;
                    color: #ffffff;
                    background: #11999e;
                    border-radius: 4px;
                    font-weight: 500;
                    font-size: 18px;
                    box-shadow: rgba(0, 0, 0, 0.05) 0px 1px 0px 0px, rgba(0, 0, 0, 0.2) 0px -1px 0px 0px inset;
                    :hover {
                        background: #006e52;
                    }
                " href="https://www.buymeacoffee.com/roboticsspace">☕️ coffee</a></p>





  <h3 style=" margin: 20px 3rem;">Resources:</h3>
  <ul style=" margin: 20px 3rem;">
    <li>
      <a href="https://hiro-group.ronc.one/vscode_urdf_previewer.html">https://hiro-group.ronc.one/vscode_urdf_previewer.html</a>
    </li>
    <li>
      <a href="https://github.com/ms-iot/vscode-ros/blob/master/doc/debug-support.md">https://github.com/ms-iot/vscode-ros/blob/master/doc/debug-support.md</a>
    </li>
    <li>
      <a href="https://github.com/lzptr/VS_Code_ROS">https://github.com/lzptr/VS_Code_ROS</a>
    </li>
    <li>
      <a href="https://docs.ros.org/en/foxy/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html">https://docs.ros.org/en/foxy/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html</a>
    </li>
  </ul>
