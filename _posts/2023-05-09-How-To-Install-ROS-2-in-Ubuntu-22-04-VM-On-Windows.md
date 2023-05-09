---
title: "How to Install ROS 2 in Ubuntu 22.04 on Windows using Virtual Box"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard

excerpt_separator: <!--more-->

---

  <h1 style="text-align: center;margin-top:20px;margin-bottom-20px;" >How to Install ROS 2 in Ubuntu 22.04 on Windows using Virtual Box</h1>

<!--excerpt.start-->
<p style="margin: 20px 3rem;"> Congratulations on taking the first step into the fascinating realm of robotics!<br> In this tutorial, I will walk you through the in-depth process to install Ubuntu 22.04 with ROS 2 on a Windows 10/11 system using the free <a href="https://www.virtualbox.org/wiki/Downloads">Oracle VirtualBox software</a>. 
<!--excerpt.end-->


  <h2 style="text-align: left;margin: 20px 3rem;">Pre Requisites</h2>
  <p style="margin: 20px 3rem;">Make sure you satisfy the below prerequisites before installing Ubuntu 22.04 Virtual Machine and ROS 2 Humble on your Windows system.</p>
   <ul style="margin: 20px 3rem;">
    <li>A computer running Windows 10 or 11. This guide uses Windows 10 64-bit. 
      Note: VirtualBox should work fine on any recent version of Windows 10 or 11.</li>
    <li>Ubuntu: Desktop 22.04 ISO Image</li>
    <li>Oracle VirtualBox 7.1 software</li>
    <li>Minimum 50 GB of Storage memory</li>
    <li>Minimum of 8 GB of RAM</li>
  </ul> 

  <p style="text-align: left;margin: 20px 3rem;">Let’s dive right into the process to set up Ubuntu 22.04 Virtual machine to start working with ROS 2.</p>
    <h3 style="text-align: left;margin: 20px 3rem;">Download Ubuntu 22.04 ISO Image</h3>
    <ol style=" margin: 20px 3rem;">
      <li> This section will walk you through the process of downloading and installing the latest LTS version of the Ubuntu distribution of Linux, i.e., <code style='color:orange'>Ubuntu 22.04 Jammy Jellyfish</code>.</li>
      <li>Go to <a href="https://cdimage.ubuntu.com/jammy/daily-live/current/">Ubuntu 22.04 Download Page</a> and Download the <a href="https://cdimage.ubuntu.com/jammy/daily-live/current/jammy-desktop-amd64.iso">64-bit PC (AMD64) desktop image</a>. A <code style='color:orange'>.iso</code> desktop image will start downloading. <br>
      <img src="/assets/article2/ubuntu_install.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>  
      NOTE : Windows 10/11 systems are based on the <code style='color:orange'>AMD64/Intel-64</code> architecture. Make sure you use the <code style='color:orange'>AMD</code> image for a Windows 10/11 system and not an <code style='color:orange'>ARMv8</code>  image. This step might take time depending on your internet speed. </li>
    </ol>
    <h3 style="text-align: left;margin: 20px 3rem;">Download and Install VirtualBox</h3>
    <ol style=" margin: 20px 3rem;">
      <li>In this section, you will use the Oracle VirtualBox software. VirtualBox is a free general-purpose virtualizer available across Linux, Mac OS, and Windows.</li>
      <li> Go to the VirtualBox Downloads page <a href="https://www.virtualbox.org/wiki/Downloads">Oracle VM VirtualBox Downloads page</a> and click on the <b>Windows hosts</b> link to download the VirtualBox software. It will download a “.exe” installer file into your Downloads folder.
      <img src="/assets/article2/virtualbox1.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>  
      </li>
      <li>Locate and double-click the VirtualBox installer file from the <code style='color:orange'>Downloads</code> folder in your File Explorer and it will launch the VirtualBox 7.0.8 Setup wizard.</li>
      <li>Click <b>Next</b> on the welcome screen in the Setup Wizard to begin the process.
      <img src="/assets/article2/virtualbox2.JPG" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>  
      </li>
      <li>
        On the <b>Custom Setup</b> screen, you can leave the default selections for now so that the installer can set up Wizard to install the features. You can change the installation location by clicking on <b>Browse</b> or else leave the default location. Click <b>Next</b> when ready to continue.
        <img src="/assets/article2/virtualbox3.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        The next screen will show a Warning about the network interfaces. The Setup Wizard will install a virtual network adapter that may reset and temporarily disconnect the network connection. Click on <b>Yes</b> to process the installation.
        <img src="/assets/article2/virtualbox4.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        The next screen will ask you to confirm the installation. Click on <b>Install</b> to begin the installation of VirtualBox 7.0.8. The installation process will begin and it might take several minutes.
        <img src="/assets/article2/virtualbox5.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        Once the installation is done, click on the <b>Finish</b> button to exit the Setup Wizard.
        <img src="/assets/article2/virtualbox7.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        Launch the VirtualBox Manager from the <b><code style='color:orange'>Start</code></b> Menu. 
        <img src="/assets/article2/virtualbox8.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
    </ol>
    <h3 style="text-align: left;margin: 20px 3rem;">Creating Virtual Machine</h3>
    <p style="text-align: left; margin: 20px 3rem;">Once the VirtualBox Software is installed properly, you can begin creating your Virtual Machine.</p>
    <ol style=" margin: 20px 3rem;">
      <li>
        Click the <b>New</b> button from the top Menu on the <b>VirtualBox Manager</b> window. This will open the <b>Create Virtual Machine</b> wizard which will let you create and configure your new Virtual Machine with the desired settings.
        <img src="/assets/article2/createvm1.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        On the <b>Virtual Machine Name and Operating System</b> section, fill in the name, Folder (location to store the Virtual machine files), and select the <b><code style='color:orange'>Ubuntu 22.04 ISO Image</code></b> (downloaded in the previous section) in the ISO Image option. <br>Click on the <b>Next</b> button to process.
        <img src="/assets/article2/createvm2.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>On the <b>Unattended Guest OS Install Setup</b> section, you need to enter your <code style='color:orange'>username</code> and <code style='color:orange'>password</code> in addition to your machine name so that it can be configured automatically during the first boot.</li>
      <li>
        Also, check the <b>Guest Additions</b> box to install the default Guest Additions ISO that is downloaded as part of VirtualBox.
        <img src="/assets/article2/createvm3.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        In the next <b>Hardware</b> section, specify how much of your host machine’s RAM and processors the virtual machine can use. Change the slider position to allocate the correct values. <br> <b>NOTE:</b> For using ROS 2 application, it is recommended to use a minimum of <code style='color:orange'>8 GB RAM</code> and at least <code style='color:orange'>6 CPUs</code>. 
        <img src="/assets/article2/createvm4.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        Next in the <b>Virtual Hard Disk section</b>, specify the size of the hard disk for the virtual machine. For ROS 2, it is recommended around <code style='color:orange'>50 GB</code> as a minimum.
        <img src="/assets/article2/createvm5.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        Click <b>Next</b> to continue and view a summary of your virtual machine setting. After this click <b>Finish</b> to initialize the machine.
        <img src="/assets/article2/createvm6.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>        
      </li>
      <li>
        You will see a message saying <code style='color:orange'>Powering VM up …</code> in the VirtualBox manager and a new desktop Window will appear for your Ubuntu 22.04 Virtual machine’s first boot.
        <img src="/assets/article2/createvm7.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 40%;"/>       
          <br>
        <img src="/assets/article2/createvm8.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35%;"/>  
      </li>
      <li>
        On the first boot, it will begin the unattended installation.
        <img src="/assets/article2/vm1.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35%;"/>        
      </li>
      <li>
        Once the installation completes, the machine will automatically reboot to complete the installation.
        <img src="/assets/article2/vm2.JPG" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35%;"/>        
      </li>
      <li>
        Finally, you will be greeted with the Ubuntu <b>log-in screen</b> where you can enter your <code style='color:orange'>username</code> and <code style='color:orange'>password</code> defined during the previous setup.
        <img src="/assets/article2/vm3.png" alt="article image 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35%;"/>        
      </li>
    </ol>
    <h3 style="text-align: left;margin: 20px 3rem;">Install ROS 2 Humble Hawksbill</h3>
    <p style="text-align: left; margin: 20px 3rem;">Hang in there!! <br>
      You are one step away from becoming a ROS 2 developer with your Ubuntu 22.04 VirtualBox Machine setup. <br><br>
      To install the latest LTS version of ROS 2, i.e., Humble Hawksbill, follow the steps <a href="https://www.theroboticsspace.com/blog/How-To-Install-ROS-2-in-Ubuntu-22-04-On-M1-Mac/#rosinstallation">here</a>.
      <br>
      Voila!! I hope you have ROS 2 Humble Running on Ubuntu 22.04 inside a Virtual Machine on Windows Laptop.
    </p>
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

  <p style=" margin: 20px 3rem;">Currently, I am reading <a href="https://www.amazon.in/dp/0241621240?&linkCode=ll1&tag=sarthakgupta0-21&linkId=414822d32ae70a18c28556fa851f4f32&language=en_IN&ref_=as_li_ss_tl">The Light We Carry</a> by Michelle Obama. </p>



  <p style=" margin: 20px 3rem;">References:</p>
  <ul style=" margin: 20px 3rem;">
    <li>
      <a href="https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview">https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox</a>
    </li>
    <li>
      <a href="https://trendoceans.com/install-ubuntu-on-virtualbox/">https://trendoceans.com/install-ubuntu-on-virtualbox/</a>
    </li>
    <li>
      <a href="https://adamtheautomator.com/install-virtualbox-on-windows-10/">https://adamtheautomator.com/install-virtualbox-on-windows-10/</a>
    </li>
    <li>
      <a href="https://docs.ros.org/en/humble/index.html">https://docs.ros.org/en/humble/index.html</a>
    </li>
  </ul>
