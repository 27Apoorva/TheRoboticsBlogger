---
title: "How To Install ROS 2 in Ubuntu 22.04 On M1 Mac"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard

excerpt_separator: <!--more-->

---

  <h1 style="text-align: center;margin-top:20px;margin-bottom-20px;" >How To Install ROS 2 in Ubuntu 22.04 On M1/M2 Mac</h1>

<!--excerpt.start-->
  <p style=" margin: 20px 3rem;">Congratulations on taking the first step into the fascinating realm of robotics!<br> 
  In this tutorial, I will walk you through the in-depth steps to install Ubuntu 22.04 with ROS 2 on the Macbook M1/M2 chip using <a href="https://docs.getutm.app/"> UTM Virtualization software.</a> </p>
<!--excerpt.end-->





  <p style=" margin: 20px 3rem;">ROS 2 is supported in MacOS using the Homebrew installation process. Although, in my 7 years as a Roboticist, I have hardly seen anyone using MacOS for Robotics. What I have seen is the use of Virtual Desktops and Dockers with Ubuntu extensively. One of the primary reasons for configuring your development environment in this manner is because robotics software works on ARM-based development kits like <a href="https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-agx-xavier/">Nvidia’s Jetson AGX series</a>. When utilizing Virtual Desktops on Mac M1, you effectively have the same development environment as your robot's runtime environment while keeping the M1 chip's inherent speed performance.</p>
  <p style="margin: 20px 3rem;"> We now understand why and what we are doing. Let’s dive right in.
    <ol style=" margin: 20px 3rem;">
      <li> The first step is more of a reminder. The Macbooks with M1/M2 Chip are ARM-based platforms compared to older MacBooks and Windows which are AMD/Intel x86-based platforms.</li>
      <li>Different virtual desktops are available like Parallels Desktop, Oracle’s Virtual Box, and UTM each having its pros and cons. I would recommend the <a href="https://www.parallels.com/products/desktop/">Parallels Desktop paid version</a> if you are a professional developer. For students or anyone looking for free software, I would recommend <a href="https://www.virtualbox.org/">Virtual Box</a> for Windows and <a href="https://docs.getutm.app/">UTM</a> for Macbooks. </li>
      <li>In this article, we will use free UTM virtualization software. UTM is a full-featured system emulator and virtual machine host for iOS and macOS. It is based on QEMU. In short, it allows you to run Windows, Linux, and more on your Mac, iPhone, and iPad. UTM allows Ubuntu to run with OpenGL, Hardware acceleration providing a highly efficient with near-native speed performance.</li>
      <li> I am using Macbook Pro with M1 Chip with MacOS 13. You will need about 50GB of free space for your new operating system.
      </li>
      <li>
        Go to <a href="https://mac.getutm.app/">https://mac.getutm.app/</a>  and click the <code style='color:orange'> Download</code> button. A UTM.dmg file will start downloading.
        <img src="/assets/simg1.png" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>        
      </li>
      <li>Go to <a href="https://cdimage.ubuntu.com/jammy/daily-live/current/"> https://cdimage.ubuntu.com/jammy/daily-live/current/</a> and Download <a href="https://cdimage.ubuntu.com/jammy/daily-live/current/jammy-desktop-arm64.iso">64-bit ARM (ARMv8/AArch64) desktop image</a>. A ".iso" desktop image will start downloading. Make sure you use the <code style='color:orange'>ARM</code> image for a Macbook with M1/M2 chip and not an <code style='color:orange'>AMD</code> image.
      This step might take time depending on your internet speed.
          <img src="/assets/simg2.png" alt="article image 2" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Double-click on the <code style='color:orange'>UTM.dmg</code> file and drag the icon to the Applications folder. 
          <img src="/assets/simg3.png" alt="article image 3" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Search for UTM and Open the UTM app from Launchpad.
          <img src="/assets/simg4.png" alt="article image 4" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Once the app is launched, click <code style='color:orange'>Create a new Virtual Machine</code>. 
          <img src="/assets/simg5.png" alt="article image 5" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Use the <code style='color:orange'>Virtualize</code> option to simulate the bare metal performance.
          <img src="/assets/simg6.png" alt="article image 6" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Select <code style='color:orange'>Linux</code> and on the next screen, you will see Boot options. Click <code style='color:orange'>Browse</code> and select the <code style='color:orange'>.iso</code> image for Ubuntu 22.04 that you download in the above step.
          <img src="/assets/simg7.png" alt="article image 7" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
          <br>
          <img src="/assets/point_11.png" alt="article image 8" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>              
      </li>
     <li>Keep pressing the <code style='color:orange'>Continue</code> button with default settings till you reach the summary screen.</li> 
     <li>Tap on the big Play button to boot Ubuntu 22.04
          <img src="/assets/simg9.png" alt="article image 9" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Select <code style='color:orange'>Try to Install Ubuntu</code>. This takes a minute and you will see a blank screen. 
          <img src="/assets/simg11.png" alt="article image 11" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Once you see the Ubuntu 22.04 screen, type in <code style='color:orange'>ubuntu</code> to login. 
          <img src="/assets/simg12.png" alt="article image 12" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>The system will boot with the live image. On the right side, you will see <code style='color:orange'>Install Ubuntu</code>. Continue with the standard installation process.  
          <img src="/assets/simg13.png" alt="article image 13" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>            
     <li>Select <code style='color:orange'>Install Third Party Software</code> in the following screen. 
          <img src="/assets/simg14.png" alt="article image 14" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Select <code style='color:orange'>Erase Ubuntu and reinstall</code> or if you are doing it for the first time, the third option <code style='color:orange'>Erase disk and install Ubuntu</code> will be your first one. Choose that. 
          <img src="/assets/simg15.png" alt="article image 15" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Save the username and password. You will need this later for login. 
          <img src="/assets/simg16.png" alt="article image 16" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Continue with installation. This will take time. 
          <img src="/assets/simg17.png" alt="article image 17" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Once Installation is done, You will see an option to restart the screen. Close the dialog box and Power Off the system. 
          <img src="/assets/simg18.png" alt="article image 18" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
          <br>
          <img src="/assets/simg19.png" alt="article image 19" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>              
      </li>
     <li>Now using the virtual machine Navigation bar, choose Drive Image Options and eject the image file.
          <img src="/assets/simg20.png" alt="article image 20" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
          <br>
          <img src="/assets/simg21.png" alt="article image 21" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>              
      </li>
     <li>You can restart the VM now by tapping on the Play Button. Now you will wait for 10 seconds to see the login screen of Ubuntu. 
          <img src="/assets/simg22.png" alt="article image 22" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>Congratulations! You have Ubuntu 22.04 running on your Macbook. You can log in now using your password.
      </li>                                             

    </ol>
  </p>

  <h2 style="text-align: center;margin-top:20px;margin-bottom-20px;" >How To Install ROS 2 in Ubuntu 22.04 On M1 Mac</h2>

<!-- 
  <p style="text-align: center; margin: auto 3rem;">Image Source: <a href="https://spectrum.ieee.org/interview-turtlebot-inventors-tell-us-everything-about-the-robot">IEEE Spectrum</a></p> -->


  <p style=" margin: 20px 3rem;">Now that we have Ubuntu 22.04 running on our Macbook with M1/M2 Chip, we can install the <a href="https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html">ROS 2 HUMBLE version</a> by following the steps for Linux Distribution.</p>
  <ol style=" margin: 20px 3rem;">
     <li>Open Terminal. 
          <img src="/assets/simg23.png" alt="article image 23" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>   
      </li>
     <li>To be able to copy and paste between your Ubuntu and Mac, run the following command in your terminal
           <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt install spice-webdavd spice-vdagent</code> 
      </li>
     <li>Set locale <br>
        Make sure you have a locale that supports UTF-8.<br>
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ locale  # check for UTF-8 skip this step if locale is utf-8 already
$ sudo apt update && sudo apt install locales
$ sudo locale-gen en_US en_US.UTF-8
$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
$ export LANG=en_US.UTF-8
$ locale  # verify settings</code>
      </li>
     <li>Setup resources
<code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt install software-properties-common
$ sudo add-apt-repository universe</code>
      </li>
     <li>ROS 2 GPG key with apt.
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt update && sudo apt install curl -y
$ sudo curl -sSL </code>
        https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
      </li>  
     <li>Add the repository to your sources list.
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo$UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null</code>

      </li>  
     <li>Update and Upgrade your packages
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt update
$ sudo apt upgrade</code>        
      </li>
     <li>Install Desktop Full
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt install ros-humble-desktop-full</code>
      </li>  
     <li>Setup environment:
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ source /opt/ros/humble/setup.bash</code>
      </li>  
     <li>Add this to your bashrc script so that you don’t have to re-run the command every time you open a new terminal.
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ echo “source /opt/ros/indigo/setup.bash” >> ~/.bashrc</code>
      </li>
     <li>To check the installation:
           <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ ros2 run demo_nodes_cpp talker</code>
      </li>
      <h3>Another important thing to learn is how to build new ros packages:
      </h3>

     <li>Go to <br> <a href="https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html">https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html.</a> <br> We need to install the `colcon` build tool.

            <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt install python3-colcon-common-extensions</code>
      </li>
      <li>Welcome to creating your first ros workspace.
      <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ mkdir -p ~/ros2_ws/src
$ cd ~/ros2_ws</code>
      </li> 
      <li>Since we are doing a clone, we need git also, So install git using
            <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ sudo apt install git</code>
      </li>
      <li>Run all the below commands from the ros2_ws folder.
              <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ git clone https://github.com/ros2/examples src/examples -b humble</code>
      </li>
      <li>After cloning, you should have the entire code inside your src folder for examples in ros2.
      </li>
      <li>Now we will build examples of the ros package. In the root of the workspace, run
              <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$colcon build</code>
      </li>
      <li>You should have build, install, and log folders.
      </li>
      <li>You need to source before being able to launch the node. So run
              <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ . install/setup.bash</code>
      </li>
      <li>Try a demo<br>
        With the environment sourced, we can run executables built by colcon. Let’s run a subscriber node from the examples:
              <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ ros2 run examples_rclcpp_minimal_subscriber subscriber_member_function</code>
            <br>
        In another terminal, let’s run a publisher node (don’t forget to source the setup script):
              <code style="display: block;
            width: 90%;
            min-height: 3em;
            overflow-y: auto;
            overflow-x: hidden;
            font-family: monospace;
            border: 1px solid #bbb;
            padding: 0.5em;
            white-space:pre-wrap;">$ ros2 run examples_rclcpp_minimal_publisher publisher_member_function</code>
            <br>
        You should see messages from the publisher and subscriber with numbers incrementing.<br>
          <img src="/assets/simg24.png" alt="article image 24" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
        <br>
        Voila!! You have ROS 2 Humble Running on Ubuntu 22.04 inside a Virtual Machine on Macbook.
      </li>                                             
  </ol>

<p style=" margin: 20px 3rem;">References:</p>
 <ul style=" margin: 20px 3rem;">
 <li>
 <a href="https://www.nvidia.com/">
 https://www.nvidia.com/
 </a>
 </li>
  <li>
  <a href="https://docs.ros.org/en/humble/index.html">
https://docs.ros.org/en/humble/index.html
</a>
 </li>
  <li>
  <a href="https://mac.getutm.app/">
https://mac.getutm.app/
</a>
 </li>
  <li>
  <a href="https://www.parallels.com/">
 https://www.parallels.com/</a>
 </li>
  <li>
 <a href="https://www.virtualbox.org/">https://www.virtualbox.org/</a>
 </li>
 </ul>




 


