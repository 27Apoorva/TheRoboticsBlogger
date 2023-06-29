---
title: "Unlocking Enhanced Development Experience: Creating Custom Configurations for VSCode Extensions"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard

excerpt_separator: <!--more-->

---

  <h1 style="text-align: center;margin-top:20px;margin-bottom-20px;" >Unlocking Enhanced Development Experience: Creating Custom Configurations for VSCode Extensions</h1>

<!--excerpt.start-->
<p style="margin: 20px 3rem;">  
In the <a href="https://www.theroboticsspace.com/blog/VS-Code-ROS-Extensions/">previous blog</a>, I shared my experience of using VS Code Extensions for ROS development. I also discussed some missing functionalities in the VS Code ROS extension, especially the lack of ROS bags interface and debug configurations for unit tests. Well, I dig deeper and figured out the process of creating custom configurations to perform various tasks, including playing rosbags. 
</p>
<!--excerpt.end-->

<p style="margin: 20px 3rem;">  Foremost, you need to ensure that you have installed the <a href="https://marketplace.visualstudio.com/items?itemName=ms-iot.vscode-ros">ROS Extension for VS Code</a>.  After you have installed the ROS extension, and restarted your VS Code, you will see a <code style='color:orange'>`.vscode`</code> folder in your ROS workspace. This folder primarily consists of the following files:
<img src="/assets/article6/image1.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>

  <ul style="margin: 20px 3rem;">
      <li><i>c_cpp_properties.json</i><br>
      It contains the compiler path, C++ standard, and ROS C++ packages path for Intellisense. This file is created by default.
      </li>
      <li><i>settings.json</i><br>
      It contains project-specific settings like ROS distro, ROS setup script path, and path to ROS Python3 packages for Intellisense. This file is created by default.
      </li>
      <li><i>launch.json </i><br>
        <ul>
          <li>This file is not created by default so, you should create a new file inside <code style='color:orange'>.vscode</code> folder and name it <code style='color:orange'>`launch.json`</code>. The file should have the following content in it: 
          <pre><code class="language-html line-numbers">{
  "version": "0.2.0",
  "configurations": [
    
  ]
}</code></pre>
          You can add your custom launch configurations inside the <code style='color:orange'>`configurations`</code> key, separated by commas.
          </li>
          <li>This file contains debugger settings and helps to specify command-line arguments for debugging. </li>
          <li>We will mostly use this file for executing launch files with the debugger. </li>
          <li>You can use the <code style='color:orange'>"start debugging"</code> play button in the <code style='color:orange'>Run and Debug</code> section to run the debugging tasks. </li>
        </ul>
      </li>
      <li><i>tasks.json</i><br>
        <ul>
          <li>It helps to specify custom build commands and also arbitrary (non-build related) tasks. It can contain multiple tasks separated by (<code style='color:orange'>{ }</code>) curly brackets. Each task has various key-value pairs inside it that include details about running the task and also the arguments. 
          </li>
          <li>This file is not created by default so, you should create a new file inside the <code style='color:orange'>.vscode</code> folder and name it <code style='color:orange'>`tasks.json`</code>. The file should have the following content in it:
          <pre><code class="language-html line-numbers" >{
  "version": "2.0.0",
  "tasks": [

  ]
}
</code></pre>
          You can add your custom task configurations inside the <code style='color:orange'>`tasks`</code> key, separated by commas.
          </li>
          <li>To run tasks specified inside the <code style='color:orange'>`tasks.json`</code> file in VS Code, use <code style='color:orange'>(CTRL + Shift + P)</code> , select <code style='color:orange'>Tasks: Run Task</code> and then select the value of the <code style='color:orange'>`label`</code> key to search that particular task and then press <code style='color:orange'>`Enter`</code> to run it.
          </li>
        </ul>
      </li>
  </ul>
</p>

<p style="margin: 20px 3rem;">  
Now that you have understood the file system, the following Table of Content provides you with a list of custom configurations. You can copy-paste the configuration inside the specified <code style='color:orange'>`tasks.json`</code> or <code style='color:orange'>`launch.json`</code> files. 
</p>

<p style="margin: 20px 3rem;">  
For ease of understanding, I am going to demonstrate each configuration using an example of a workspace. I am also providing a <a href="https://github.com/27Apoorva/ros_vscode_config">GitHub repository</a> containing the example for you to clone and try out various custom functionalities. 
</p>

  <h2 style="text-align: left;margin: 20px 3rem;">TABLE OF CONTENT</h2>
  <ul style=" margin: 20px 3rem;">
    <li>ENVIRONMENT SETUP CONFIGURATIONS<br>
      <ul style="list-style-type: square;">
        <li>CREATE, BUILD, AND SOURCE ROS 2 PACKAGES
        </li>
      </ul>
    </li>
    <li>ROS 2 BAGS PLAYBACK</li>
    <li>BUILD CONFIGURATIONS</li>
    <li>DEBUG TEST CONFIGURATIONS<br>
      <ul style="list-style-type: square;">
        <li>Debugging Single ROS Node using Launch file ( Supports C++ and Python nodes)</li>
        <li>Debugging Multiple ROS Nodes using Launch files (Supports C++ and Python nodes)</li>
      </ul>
    </li>
    <li>UNIT TESTS CONFIGURATIONS</li>
  </ul>

<h2 style="text-align: left;margin: 20px 3rem;">ROS 2 Workspace in VS Code</h2>
<p style="text-align: left;margin: 20px 3rem;">
When you create a new ROS 2 workspace with the name <code style='color:orange'>`vscode_ros2_test_ws`</code>, you will only have a <code style='color:orange'>`src`</code> folder inside it where you will create your ROS packages. Once you build the workspace, three new folders <code style='color:orange'>`build`</code>, <code style='color:orange'>`install`</code> and <code style='color:orange'>`log`</code> will be created inside the workspace.
<img src="/assets/article6/image2.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>
</p>

<h2 style="text-align: left;margin: 20px 3rem;">ENVIRONMENT SETUP CONFIGURATIONS</h2>
<h3 style="text-align: left;margin: 20px 3rem;">CREATE, BUILD, AND SOURCE ROS 2 PACKAGES</h3>
<p style="text-align: left;margin: 20px 3rem;">
In ROS 2, you can create packages using two different build types, i.e., <code style='color:orange'>`ament_cmake`</code> and <code style='color:orange'>`ament_python`</code>. You need to specify the build type and also additional dependencies while creating a package. After your package is created, you need to build and source the workspace. Instead of typing a bunch of commands one after another in the terminal, you can save yourself some time by copy-pasting the below configurations inside the <code style='color:orange'>`tasks`</code> key, separated by commas in the <code style='color:orange'>`tasks.json`</code> file.
</p>

<p style="text-align: center; margin: auto 3rem;">
<ul style="margin: 20px 3rem;list-style-type: none;">
  <li>
    <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
    "label": "create-package-cmake",
    "type": "shell",     
    "command": "source /opt/ros/&lt;your_active_ros2_distro&gt;/setup.bash && cd ${workspaceFolder}/src/ && ros2 pkg create &lt;your_new_package_name&gt; --build-type ament_cmake --dependencies rclcpp && cd .. && colcon build --symlink-install && source ${workspaceFolder}/install/setup.bash"
}
</code></pre>
  </li>
</ul>
<div style="text-align: center; margin: auto 3rem;">For a C++ package, the build type is specified as ament_cmake</div></p>

<p style="text-align: center; margin: auto 3rem;">
<ul style="margin: 20px 3rem;list-style-type: none;">
  <li>
    <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
    "label": "create-package-python",
    "type": "shell",
    "command": "source /opt/ros/&lt;your_active_ros2_distro&gt;/setup.bash && cd ${workspaceFolder}/src/ && ros2 pkg create &lt;your_new_package_name&gt; --build-type ament_python --dependencies rclpy && cd .. && colcon build --symlink-install && source ${workspaceFolder}/install/setup.bash"
}
</code></pre>
  </li>
</ul>
<div style="text-align: center; margin: auto 3rem;">For a Python package, the build type is specified as ament_python</div></p>

<p style="text-align: left;margin: 20px 3rem;">
Change the <code style='color:red'>&lt;your_active_ros2_distro&gt;</code> to your active ROS 2 distro while creating your tasks. <br>
Now each time, you want to create a new package, change the <code style='color:red'>&lt;your_new_package_name&gt;</code> to the name of the new package you want to create. <br>
Also, you can add more dependencies like std_msgs after <code style='color:orange'>--dependencies</code> , if required. <br>

To run the tasks for package creation, use <code style='color:orange'>(CTRL + Shift + P)</code>, select <code style='color:orange'>Tasks: Run Task</code> and then select the <code style='color:orange'>task</code> from the labels. This will create a new package inside your src folder and then build and source the workspace.  
<img src="/assets/article6/image3.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>
</p>


<h2 style="text-align: left;margin: 20px 3rem;">ROS 2 BAGS PLAYBACK</h2>
<p style="text-align: left;margin: 20px 3rem;">
One of the major shortcomings of the VS Code extension for ROS is that it does not provide any interface for ROS bag files. Seasoned ROS developer knows how often they need to play ROS bag files to tune their algorithms.<br>
But there is a way out. You can create a task by copy-pasting the below configuration inside the <code style='color:orange'>`tasks`</code> key, in your <code style='color:orange'>`tasks.json`</code> file to play bag files with just a few keystrokes. Just set the path of the bag file at <code style='color:red'>&lt;set-bag-file-path&gt;</code>.
</p>
<ul style="margin: 20px 3rem;list-style-type: none;">
  <li>
    <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
    "label": "ros-bag-play",
    "type": "shell",
    "command": "source /opt/ros/&lt;your_active_ros2_distro&gt;/setup.bash && cd ${workspaceFolder}/src/ && ros2 bag play &lt;set-bag-file-path&gt;"
}
</code></pre>
  </li>
</ul>

<p style="text-align: left;margin: 20px 3rem;">
Change the <code style='color:red'>&lt;your_active_ros2_distro&gt;</code> to your active ROS 2 distro while creating your tasks.<br>
To run the task for playing the bag file, use <code style='color:orange'>(CTRL + Shift + P)</code>, select <code style='color:orange'>Tasks: Run Task</code> and then select the <code style='color:orange'>`ros-bag-play`</code> task. This will start playing the bag file.
<img src="/assets/article6/image4.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 60vmax;"/>
</p>

<h2 style="text-align: left;margin: 20px 3rem;">BUILD CONFIGURATIONS</h2>
<p style="text-align: left;margin: 20px 3rem;">
While building a ROS 2 workspace using <code style='color:orange'>`colcon build`</code>, you might be  using a combinations of arguments. You can add the most commonly used <code style='color:orange'>`colcon build`</code> commands as configurations inside the <code style='color:orange'>`tasks`</code> key in your <code style='color:orange'>`tasks.json`</code> file and execute the build using VS Code.

<ul style=" margin: 20px 3rem;">
      <li>colcon build<br>
        This will build the workspace using colcon build.
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
      "build",
  ],
  "problemMatcher": [
      "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon build"
}</code></pre>
          </li>
        </ul>
      </li>
      <li>colcon build –symlink-install<br>
        This creates symlink of the executables instead of copying files from the source and build directories where possible. This is especially useful for Python nodes. 
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
      "build",
      "--symlink-install",
  ],
  "problemMatcher": [
      "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon build --symlink-install"
}</code></pre>
          </li>
        </ul>
      </li>
      <li>colcon build --merge-install<br>
        Use <code style='color:orange'>${workspace}/install</code> as a prefix for all packages instead of a package specific subdirectory in the install base.
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
      "build",
      "--merge--install",
  ],
  "problemMatcher": [
      "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon build --merge--install"
}</code></pre>
          </li>
        </ul>
      </li>
      <li>colcon build --packages-select <br>
        You can build a selected number of packages inside your workspace by specifying the packages (separated by space)  name after the <code style='color:orange'>--packages-select</code> argument. 
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
    "build",
    "--packages-select",
    "&lt;specify_packages_name_here&gt;",
  ],
  "problemMatcher": [
    "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon build --packages-select"
}</code></pre>
          </li>
        </ul>
      </li>
      <li>colcon build (multiple arguments)<br>
        You can use multiple arguments with <code style='color:orange'>`colcon build`</code> by specifying the arguments inside the <code style='color:orange'>`args`</code> key in the configuration. <br>
        In the below configuration, you can execute two arguments together that will build a selected number of packages inside your workspace by specifying the packages names (separated by space) after the <code style='color:orange'>--packages-select</code> argument and also create symlinks. 
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
    "build",
    "--symlink-install",
    "--packages-select",
    "&lt;specify_packages_name_here&gt;",
  ],
  "problemMatcher": [
    "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon build custom 1"
}</code></pre>
          </li>
        </ul>
        The below configuration builds the workspace by creating symlinks and aborts the build process after it gets the first package with any errors.
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
    "build",
    "--symlink-install",
    "--abort-on-error",
  ],
  "problemMatcher": [
    "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon build custom 2"
}</code></pre>
          </li>
        </ul>
      </li>
  </ul>
</p>

<p style="text-align: left;margin: 20px 3rem;">
To run the different colcon build tasks, use <code style='color:orange'>(CTRL + Shift + P)</code>, select <code style='color:orange'>Tasks: Run Task</code> and then select the <code style='color:orange'>build task</code> from the available options.
<img src="/assets/article6/image5.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 60vmax;"/>
</p>


<h2 style="text-align: left;margin: 20px 3rem;">DEBUG TEST CONFIGURATIONS </h2>
<p style="text-align: left;margin: 20px 3rem;">
Debugging the code you have written is one of the toughest places to be especially when there is a segmentation fault. While the initial stage of debugging will begin with using <code style='color:orange'>ROS Loggers</code> and <code style='color:orange'>RViz</code>, using a debugger like <code style='color:orange'>GDB</code> is essential during code crashes or while dealing with an unknown.<br>
By using the GDB debugger, you can control the flow of execution line by line and have a peek at variables of interest.  
  <ul style=" margin: 20px 3rem;">
    <li><b>Debugging single ROS node using Launch file (Supports C++ and Python nodes)</b>
      <ul>
        <li>The following is an example of a launch file for package name <code style='color:orange'>`ros2_cpp_pkg`</code> that launches a single C++ node called <code style='color:orange'>`publisher`</code>. The executables in the launch file can be either C++ or Python.
        <img src="/assets/article6/image6.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
        </li>
        <li>Go to the <code style='color:orange'>Run and Debug Tab</code> on the left sidebar of VS Code and then click on <code style='color:orange'>create a launch.json file</code> -> <code style='color:orange'>ROS</code> -> <code style='color:orange'>ROS: Launch</code> -> <code style='color:orange'>Choose a ROS package</code> -> <code style='color:orange'>Choose a ROS launch file</code> created in the previous step. This step will add the location of the launch file from inside the <code style='color:orange'>install</code> folder in your workspace. 
        <img src="/assets/article6/image7.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50vmax;"/>
        </li>
        <li>A new <code style='color:orange'>.vscode/launch.json</code> file will be created containing the configuration for the launch file as a target. If you created a <code style='color:orange'>launch.json</code> file before, you can add the following launch configuration in the <code style='color:orange'>`configurations’</code> key. Add the name and location of the launch file from inside the <code style='color:orange'>install</code> folder in your workspace at <code style='color:red'>&lt;launch_file/location/inside/install/folder&gt;</code>.
        </li>
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style="margin-right: 20px 3rem;">{ 
  "name": "ROS: Launch",
  "request": "launch",
  "target": "&lt;launch_file_location_inside_install_folder&gt;",
  "launch": ["rviz", "gz","gzclient","gzserver"],
  "type": "ros"
}</code></pre>
          </li>
        </ul>
        <li>Go to the C++/Python code for the executable specified in the launch file and place a <code style='color:orange'>breakpoint</code> in the file.
        <img src="/assets/article6/image8.gif" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>
        </li>
        <li>Now go to the <code style='color:orange'>Run and Debug Tab</code> on the left sidebar of VS Code , select the launch configuration from the top drop down menu and click the <code style='color:orange'>Play</code> button to begin debugging.
        <img src="/assets/article6/image9.gif" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>
        </li>
      </ul>
    </li>
    <li><b>Debugging Multiple ROS Nodes using Launch files (Supports C++ and Python nodes)</b>
      <ul>
        <li>The following is an example of a launch file that consists of two nodes named <code style='color:orange'>`talker_node`</code> and <code style='color:orange'>`listener`</code> node. The launch file can have either C++ and/or Python nodes.
        <img src="/assets/article6/image10.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
        </li>
        <li>Add the following configuration in the <code style='color:orange'>`configurations’</code> key to your <code style='color:orange'>`launch.json`</code> file. Add the name and location of the launch file from inside the <code style='color:orange'>install</code> folder in your workspace at <code style='color:red'>&lt;launch_file/location/inside/install/folder&gt;</code>.
        <ul style="list-style-type: none;">
          <li>
            <pre><code class="language-html line-numbers"  style="margin-right: 20px 3rem;">{
  "name": "ROS: Launch Multiple",
  "request": "launch",
  "target": "&lt;launch_file_location_inside_install_folder&gt;",
  "launch": ["rviz", "gz","gzclient","gzserver"],
  "type": "ros"
}
</code></pre>
          </li>
        </ul>
        </li>
        <li>Go to the C++/Python code for the executables specified in the launch file and place a <code style='color:orange'>breakpoint</code> in the required files.
        <img src="/assets/article6/image11.gif" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>
        </li>
        <li>Now go to the <code style='color:orange'>Run and Debug Tab</code> on the left sidebar of VS Code , select the launch configuration from the top drop-down menu and click the <code style='color:orange'>Play</code> button to begin debugging.
        <img src="/assets/article6/image12.gif" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>
        </li>
        <li>You can switch between different executables from the <code style='color:orange'>debugger menu</code>.
        <img src="/assets/article6/image13.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 30vmax;"/>
        </li>
      </ul>
    </li>
  </ul>
</p>



<h3 style="text-align: left;margin: 20px 3rem;">UNIT TEST CONFIGURATIONS </h3>
<p style="text-align: left;margin: 20px 3rem;">
I can’t stress enough on the <a href="https://docs.ros.org/en/iron/Tutorials/Intermediate/Testing/Testing-Main.html">importance of unit testing</a> for a stable software release process and code maintenance. <br>
ROS 2 provides <a href="https://docs.ros.org/en/humble/Tutorials/Intermediate/Testing/Cpp.html">gtest</a> for testing C++ nodes and <a href="https://docs.ros.org/en/humble/Tutorials/Intermediate/Testing/Python.html">pytest</a> for testing Python nodes. colcon provides macros for test-aware compilation and verbs dedicated to testing the project in its entirety. You can execute <code style='color:orange'>`colcon test`</code> to run your unit tests. The test files are generally stored inside a <code style='color:orange'>`tests`</code> folder.<br>
To execute the unit tests for a particular package using <code style='color:orange'>`colcon test`</code> command, give the <code style='color:orange'>`tests`</code> folder name and the name of the package at <code style='color:red'>&lt;specify_package_name_here&gt;</code> after <code style='color:orange'>`--packages-select`</code> argument. <br>
<ul style="margin: 20px 3rem;list-style-type: none;">
  <li>
    <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
    "test",
    "--ctest-args",
    “tests”,
    "--packages-select",
    “&lt;specify_package_name_here&gt;”,
  ],
  "problemMatcher": [
    "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon_test"
}
</code></pre>
  </li>
</ul>
</p>
<p style="text-align: left;margin: 20px 3rem;">
Testing with pytest framework, you can specify the name of the test function at <code style='color:red'>&lt;specify-name-of-specific-test-function&gt;</code>  you created with the <code style='color:orange'>`colcon test`</code> command to test for that specific test function after <code style='color:orange'>`--pytest-args`</code> argument. 
<ul style="margin: 20px 3rem;list-style-type: none;">
  <li>
    <pre><code class="language-html line-numbers"  style=" margin-right: 20px 3rem;">{
  "type": "colcon",
  "args": [
    "test",
    "--packages-select",
    “&lt;specify_packages_name_here&gt;”,
    "--pytest-args",
    "-k",
    "&lt;specify-name-of-specific-test-function&gt;",
  ],
  "problemMatcher": [
    "$catkin-gcc"
  ],
  "group": "build",
  "label": "colcon_pytest"
}
</code></pre>
  </li>
</ul>
</p>


<p style="text-align: left;margin: 20px 3rem;">
To run the different colcon test tasks, use <code style='color:orange'>(CTRL + Shift + P)</code>, select <code style='color:orange'>Tasks: Run Task</code> and then select the <code style='color:orange'>test task</code> from the available options.
<img src="/assets/article6/image14.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 45vmax;"/>
</p>




<h3 style="text-align: left;margin: 20px 3rem;">Conclusion</h3>
<p style="text-align: left;margin: 20px 3rem;">
By leveraging the power of VS Code and ROS extensions, developers can streamline their coding process, improve productivity, and gain more control over their ROS projects. Whether it's setting up a ROS workspace, configuring build tasks, or utilizing ROS-specific features, understanding these configurations opens up new possibilities for efficient and effective ROS development. <br>
As mentioned previously, you can find the entire configurations from my <a href="https://github.com/27Apoorva/ros_vscode_config">GitHub repository</a>. <br>
If you want to create a custom configuration, feel free to open a pull request in the <a href="https://github.com/27Apoorva/ros_vscode_config">GitHub repository</a>. You can also create a Feature Request if you want me to implement your ideas. <br>
Embracing these configurations will undoubtedly empower ROS developers to unleash their full potential and embark on successful robotics projects using the VS Code ecosystem.
</p>




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