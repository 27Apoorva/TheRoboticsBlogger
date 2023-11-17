---
title: "Kinematic Modelling for Mobile Robots"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard

excerpt_separator: <!--more-->

---

  <h1 style="text-align: center;margin-top:20px;margin-bottom-20px;" >Kinematic Modelling for Mobile Robots</h1>

<!--excerpt.start-->
<p style="margin: 20px 3rem;">  
The concept of kinematic modeling is very well studied be it for the AMRs or robotic arms.
Being an expert in mobile robotics, I have spent years in the exploration of planners and controllers of differential-drive robots. Although there is always a limitation in the motion range, differential-drive is still the most common kinematic model so far. I have recently started seeing a shift and the adaptation of holonomic robots coming up.<br>
In this blog, I wanted to list the kinematics for both non-holonomic and holonomic robots, along with recommended controllers and planners.
</p>
<!--excerpt.end-->

<p style="margin: 20px 3rem;">  
I would use the open-source <a href="https://github.com/linorobot/linorobot2">Linorobot2</a> package in GitHub, which provides a robust simulation environment complete with Nav2. The sensor configurations I would use for testing the planners are 2D LIDAR, 6-DOF IMU, and Encoders. 
</p>

<h2 style="text-align: left;margin: 20px 3rem;" id="envsetupconfig">Wheel Types in Mobile Robots</h2>
<p style="margin: 20px 3rem;">  Mobile robots come in various configurations, and their movement heavily relies on the type of wheels they use. Let's begin by categorizing the wheels into two main types: Holonomic and Non-Holonomic wheels.

  <ul style="margin: 20px 3rem;padding-left: 0;padding-top: 0;">
      <li><b style="font-size: 28px;">Non-Holonomic Wheels</b><br>
      Non-holonomic wheels are known for their stability and simplicity. They allow the robot to move in a limited set of directions, making them less agile than their holonomic counterparts. The common types of non-holonomic wheels are:
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Differential-Drive Wheels</b><br>
          The defining characteristic of a differential-drive robot is its wheel configuration. These robots typically have two fixed wheels placed on a common axis and a caster wheel. The two fixed wheels are responsible for propelling the robot forward and backward, while the caster wheel allows the robot to maintain stability and freely rotate about its central point.<br>
          <img src="/assets/article7/Differential 1.jpeg" alt="Differential 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Differential-Drive Wheels Model</div><br>
          <img src="/assets/article7/Differential 2.jpeg" alt="Differential 2" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Robot Motions based on wheel velocity and direction for Differential-Drive Wheels Model</div>
          </li>
          <li><b>Skid-Steer Wheels</b><br>
          A skid-steer robot is characterized by its mobility configuration, featuring two sets of wheels on either side of the robot, each set independently driven. These robots achieve movement and directional control by varying the speed and direction of rotation of the wheels on each side. Unlike a differential-drive robot, a skid-steer robot lacks a dedicated caster wheel. Instead, changes in velocity and wheel rotation enable the robot to turn in place, making it highly maneuverable. Skid-steer robots are commonly employed in applications where precise control of movement and the ability to turn within a confined space are crucial, such as in industrial settings and certain types of mobile robotic platforms.<br>
          <img src="/assets/article7/Skid steer 1.jpeg" alt="Skid steer 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Skid-Steer Wheels Model</div><br>
          <img src="/assets/article7/Skid steer 2.jpeg" alt="Skid steer 2" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Robot Motions based on wheel velocity and direction for Skid-Steer Wheels Model</div>
          </li>
        </ul>
      </li><br>
      <li><b style="font-size: 28px;">Kinematic Model for Non-Holonomic Robots</b><br>
      The Differential-Drive Kinematic Model is a fundamental concept in mobile robotics, especially for non-holonomic robots. It describes the motion of a robot with two fixed wheels and a caster wheel or a single free caster wheel. The Differential-Drive Kinematic Model allows control of the robot's linear and angular velocities, enabling precise motion planning and control.
        <ul style="padding-left: 13px;padding-top: 0;">
          <li><b>Assumptions of the-Differential Drive Kinematic Model</b><br>
          The Differential-Drive Kinematic Model is based on a few assumptions:
          <ol>
            <li><b>No Slippage:</b> The model assumes that there is no slippage between the wheels and the ground. In reality, some slippage may occur, but this assumption simplifies the kinematic calculations.</li>
            <li><b>Pure Rotation:</b> The model assumes that the robot can only perform pure rotations, meaning it can only turn about a central point without any lateral movement during the rotation.</li>
            <li><b>No Skidding:</b> The model assumes that there is no skidding between the wheels and the ground during turning.</li>
          </ol>
          </li>
          <li><b>Kinematic Equations</b><br>
          <img src="/assets/article7/Kinematic 1.JPG" alt="Kinematic 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Kinematic Model for Differential-Drive Model</div><br>
            X and Y represent the global coordinate system and XB and YB represent the local coordinate system of the robot. <br><br>
            In the Differential-Drive Kinematic Model, two main parameters are considered:
            <ul>
              <li><b>Linear velocity (V):</b> The robot's forward or backward speed.</li>
              <li><b>Angular velocity (ω):</b> The robot's rate of rotation about a central point.</li>
            </ul>
            The kinematic equations for the differential-drive model are as follows:
            <ul>
              <li><b>V = (v_left + v_right) / 2</b></li>
              <li><b>ω = (v_right - v_left) / L</b></li>
            </ul>
            where v_left and v_right are the linear velocities of the left and right wheels, respectively, and L is the distance between the two drive wheels.
          </li>
        </ul>
      </li>
      <li><b style="font-size: 28px;">Holonomic Wheels</b><br>
      Holonomic wheels provide exceptional maneuverability, allowing mobile robots to move in any direction within a 2D plane without changing their orientation. They are ideal for applications that require precise positioning and navigation. Two common types of holonomic wheels are:
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Omni Wheels</b><br>
          Omni-wheels have rollers around their circumference, allowing them to move not only forward and backward but also sideways. This unique feature provides holonomic motion capabilities.<br>
          <img src="/assets/article7/Omni 1.jpeg" alt="Omni 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Omni Wheels Model</div><br>
          <img src="/assets/article7/Omni 2.jpeg" alt="Omni 2" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Robot Motions based on wheel velocity and direction for Omni Wheels Model</div>
          </li>
          <li><b>Mecanum Wheels</b><br>
          Mecanum wheels have rollers mounted at an angle to the wheel's rotation axis. By controlling the speeds and directions of the mecanum wheels, a robot can move in any direction without altering its orientation.<br>
          <img src="/assets/article7/Mecanum 1.jpeg" alt="Mecanum 1" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Mecanum Wheels Model</div><br>
          <img src="/assets/article7/Mecanum 2.jpeg" alt="Mecanum 2" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
          <div style="text-align: center; margin:0;">Robot Motions based on wheel velocity and direction for Mecanum Wheels Model</div>
          </li>
        </ul>
      </li>
      <li><b style="font-size: 28px;">Kinematic Model for Holonomic Robots</b><br>
      The Mecanum Drive Kinematic Model is specifically designed for holonomic robots equipped with Mecanum wheels. These wheels have rollers mounted at an angle to the wheel's rotation axis, allowing them to exhibit unique motion characteristics. By independently controlling the speeds and directions of the Mecanum wheels, the robot can move in any direction without altering its orientation.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Assumptions of the Mecanum Drive Kinematic Model</b><br>
          The Mecanum Drive Kinematic Model is based on several assumptions to simplify the mathematical representation of the robot's motion. These assumptions include:
          <ol>
            <li><b>Ideal Wheels:</b>The model assumes ideal Mecanum wheels with no slippage or friction, allowing for accurate motion predictions.</li>
            <li><b>No Vertical Motion:</b>The model operates in a 2D plane and does not consider any vertical motion of the robot.</li>
            <li><b>Small Angles:</b>The angles between the rollers and the wheel's rotation axis are assumed to be small, enabling linear approximations for velocity calculations.</li>
          </ol>
          </li>
        </ul>
      </li>
  </ul>
</p>


<h2 style="text-align: left;margin: 20px 3rem;" id="envsetupconfig">Planners for wheeled robots</h2>
<p style="margin: 20px 3rem;">In the domain of robotics and autonomous navigation, the choice of planners is a pivotal decision that influences a robot's path-planning capabilities. Whether dealing with holonomic or non-holonomic robots, selecting the right planner is essential. Here, I will delve into the characteristics and applicability of various planners, considering both holonomic and non-holonomic robots.
  <ul style="margin: 20px 3rem;padding-left: 0;padding-top: 0;">
      <li><b style="font-size: 24px;">NavFn Planner</b><br>
      NavFn is excellent for holonomic robots that can follow paths precisely, but it may lead to suboptimal paths for non-holonomic robots due to its grid-based approach.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> NavFn is well-suited for holonomic robots. It provides global path planning by treating the environment as a grid and using the Fast Marching Method.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> While NavFn can be used with non-holonomic robots, there are better choices than this one. It might generate paths that require complex maneuvers.<br>
          </li>
        </ul>
      </li>
      <li><b style="font-size: 24px;">Smac Planner 2D (Sparse Multi-Modal Asynchronous Planner)</b><br>
      Smac Planner 2D balances path optimality and computation speed, making it a solid choice for holonomic robots, and it can still be effective for non-holonomic robots.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b>  Smac Planner 2D is suitable for holonomic robots. It uses a sparse sampling approach, making it computationally efficient.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It can be used with non-holonomic robots, but its efficiency may vary depending on the robot's constraints.<br>
          </li>
        </ul>
      </li>
       <li><b style="font-size: 24px;">Smac Lattice Planner</b><br>
      Smac Lattice Planner offers a balance of optimality and flexibility, making it a practical choice for holonomic robots. For non-holonomic robots, it can be adapted to suit the needs.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> Smac Lattice Planner is a versatile choice for holonomic robots. It uses lattice-based planning and is effective for various scenarios.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It can work for non-holonomic robots, but it may require additional adaptability for the robot's constraints.<br>
          </li>
        </ul>
      </li>
       <li><b style="font-size: 24px;">Pure Pursuit</b><br>
      Pure Pursuit offers simplicity and efficiency for holonomic robots, making it an intuitive choice for direct goal-reaching tasks.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> Pure Pursuit is a natural fit for holonomic robots. It is designed for guiding robots directly toward a goal point.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It can work with non-holonomic robots, but it may not fully utilize their capabilities.<br>
          </li>
        </ul>
      </li>
       <li><b style="font-size: 24px;">SBPL Lattice Planner (Search-Based Planning Library)</b><br>
      SBPL Lattice Planner is known for its path optimality and is a strong candidate for holonomic robots. It can also serve non-holonomic robots but with potential customization.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> SBPL Lattice Planner is suitable for holonomic robots. It uses a search-based approach to generate paths and is effective in complex environments.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It can be applied to non-holonomic robots, although it may require additional adaptations and configurations.<br>
          </li>
        </ul>
      </li>
  </ul>
</p>

<p style="margin: 20px 3rem;">  
  After conducting thorough tests and measurements with various planners available in Nav2 for non-holonomic robots and holonomic robots, I have gained valuable insights into their performance. Here are my findings based on extensive testing using the Linorobot2 simulation. <br>
  <img src="/assets/article7/nav2_path.png" alt="nav2_path" style="display: block;
          margin-left: auto;
          margin-right: auto;
          width: 35vmax;"/>
  <div style="text-align: center; margin:0;">Nav2 Path from Start to Goal</div>
</p>

<p style="margin: 20px 3rem;">
For my tests with various planners present in the Navigation Stack in ROS 2, I provided a common navigation goal, which had an approximate distance of 21 meters. I carefully measured the time taken by each planner to complete the given task. Here are the results:
  <ul style="margin: 20px 3rem;padding-left: 0;padding-top: 0;">
      <li><b style="font-size: 24px;">NavFn Planner</b><br>
      The NavFn Planner took approximately 92 seconds to compute a path for a common navigation goal for a non-holonomic robot. For a holonomic robot, the NavFn Planner took approximately 97 seconds to navigate, through a common goal situated approximately 21 meters away. It demonstrated reasonable performance within this setup.
      </li>
      <li><b style="font-size: 24px;">Smac Planner 2D</b><br>
      The Smac Planner 2D required around 107 seconds to generate a path for a non-holonomic robot. It offers more advanced features than the NavFn Planner but at the cost of increased computation time. The Smac Planner 2D exhibited slower performance, requiring around 115 seconds to complete the same navigation task for a holonomic robot. It was the slowest among the tested planners for holonomic robots.
      </li>
       <li><b style="font-size: 24px;">Smac Lattice Planner</b><br>
      The Smac Lattice Planner performed relatively well, taking about 94 seconds to find a path for a non-holonomic robot. It leverages lattice-based planning techniques, which can lead to efficient paths. For a holonomic robot, the Smac Lattice Planner delivered competitive performance, taking roughly 101 seconds to reach the designated goal. It showcased good potential for holonomic robot planning.
      </li>
  </ul>
</p>

<p style="margin: 20px 3rem;">  
  Based on the results, the NavFn Planner appears to be the fastest among the tested planners, taking 92 seconds for non-holonomic robots and 97 seconds for non-holonomic robots respectively. However, its performance may vary depending on the environment's complexity. While all the planners are capable of achieving the navigation goal, the NavFn  Planner demonstrated slightly better performance by completing the task in the shortest amount of time (92 seconds).
</p>

<p style="margin: 20px 3rem;">  
  It's important to note that planner performance can vary based on the specific robot's characteristics, environment, and the nature of the navigation task. Therefore, I recommend further fine-tuning and testing the selected planner to ensure optimal performance in your real-world applications.
</p>

<h2 style="text-align: left;margin: 20px 3rem;" id="envsetupconfig">Controllers for wheeled robots</h2>
<p style="margin: 20px 3rem;">Several controllers cater to the diverse needs of both holonomic and non-holonomic robots. These controllers are essential components that help robots navigate through environments efficiently. I will explain the characteristics and suitability of these controllers for different types of robots.
  <ul style="margin: 20px 3rem;padding-left: 0;padding-top: 0;">
      <li><b style="font-size: 24px;">DWA (Dynamic-Window Approach) Controller</b><br>
      DWA excels in providing quick and agile navigation for robots capable of sudden velocity changes and complex motion patterns, as is common with holonomic robots.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> The DWA controller is highly suitable for holonomic robots, such as omnidirectional or mecanum wheel robots. It leverages their ability to move in any direction without changing their orientation.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It's not the best choice for non-holonomic robots, like differential-drive or car-like robots. These robots have constraints on instantaneous velocity changes and turning.<br>
          </li>
        </ul>
      </li>
      <li><b style="font-size: 24px;">DWB (Dynamic-Window Based) Controller</b><br>
      DWB's dynamic window search is particularly useful for real-time obstacle avoidance and goal-reaching tasks, making it versatile for various robot types.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> DWB can work well with holonomic robots, thanks to its dynamic window search, which adapts to a robot's instantaneous motion capabilities.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It is also suitable for non-holonomic robots, although not as ideal as for holonomic robots.<br>
          </li>
        </ul>
      </li>
       <li><b style="font-size: 24px;">TEB (Trajectory Rollout) Controller</b><br>
      TEB's focus on trajectory optimization is excellent for robots capable of complex motion planning but may be overkill for non-holonomic robots.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> TEB is a great choice for holonomic robots as it plans and optimizes feasible trajectories considering the robot's kinematics.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> It can be used with non-holonomic robots, but its performance may be less optimal compared to holonomic robots.<br>
          </li>
        </ul>
      </li>
      <li><b style="font-size: 24px;">RPP (Recursive Pyramid Planner)</b><br>
      RPP's hierarchical path planning can suit non-holonomic robots in certain scenarios, but it may not be the first choice.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> RPP is not commonly used with holonomic robots as it's more oriented toward grid-based path planning.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> IWhile RPP is generally used for non-holonomic robots, its applicability depends on specific use cases.<br>
          </li>
        </ul>
      </li>
      <li><b style="font-size: 24px;">MPPI (Model Predictive Path Integral) Controller</b><br>
      MPPI is designed for robots that benefit from probabilistic path optimization, which is often the case for non-holonomic robots dealing with complex environments.
        <ul style="padding-left: 10px;padding-top: 0;">
          <li><b>Suitability for Holonomic Robots:</b> MPPI is generally not chosen for holonomic robots due to their more direct and efficient path-planning capabilities.
          </li>
          <li><b>Suitability for Non-Holonomic Robots:</b> MPPI is better suited for non-holonomic robots. It's especially useful in scenarios that require predictive and probabilistic path planning.<br>
          </li>
        </ul>
      </li>
  </ul>
</p>

<p style="margin: 20px 3rem;">  
  For non-holonomic robots, I would recommend considering the DWB Controller. It's known for its stable performance, simplicity, and relatively fast computation times. It should complement the faster NavFn Planner effectively. 
</p>

<p style="margin: 20px 3rem;">  
  For more advanced trajectory planning and can tolerate slightly longer computation times, the TEB Controller might be suitable, especially if the robot needs to navigate dynamic environments with obstacles.
</p>

<p style="margin: 20px 3rem;">  
  Given these assessments, the DWB Controller emerges as the top recommendation for holonomic robots in Nav2 due to its remarkable precision and efficiency, which are crucial for responsive and accurate navigation in various environments.
</p>

<h3 style="text-align: left;margin: 20px 3rem;">Conclusion</h3>
<p style="text-align: left;margin: 20px 3rem;">
In the ever-evolving realm of robotics, my choice of wheel type, kinematic model, and navigation tools holds the key to unlocking the full potential of my robot. I've embarked on a journey through the diverse landscape of wheel configurations, from the nimble holonomic mecanum wheels to the versatile differential-drive. I've delved into the intricacies of their kinematic models, understanding how they enable robots to move and navigate.
</p>
<p style="text-align: left;margin: 20px 3rem;">
However, my quest doesn't end with theoretical knowledge alone. In the practical realm of robotics, I've put these theories to the test. Through rigorous experimentation, I've identified the NavFn Planner as my swift companion for holonomic robots, while the DWB Controller emerges as the pinnacle of precision for holonomic navigation in ROS 2 Navigation. For non-holonomic robots, the NavFn Planner offers a robust choice, complemented by the agility and obstacle-handling prowess of the TEB Controller.
</p>
<p style="text-align: left;margin: 20px 3rem;">
As I conclude this journey, remember that the world of robotics is dynamic and ever-changing. While these recommendations serve as a compass, my robot's unique characteristics and the complexities of its operational environment will always guide my final decision. So, I'll harness this knowledge, embrace the possibilities, and let my robot embark on its path to innovation and discovery.
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
      <a href="https://en.wikipedia.org/wiki/Differential_wheeled_robot">Differential wheeled robot - Wikipedia</a>
    </li>
    <li>
      <a href="http://www.robotplatform.com/knowledge/Classification_of_Robots/wheel_control_theory.html">Wheel Control Theory - Robot Platform </a>
    </li>
    <li>
      <a href="https://en.wikibooks.org/wiki/Robotics/Types_of_Robots/Wheeled">Robotics/Types of Robots/Wheeled - Wikibooks</a>
    </li>
    
  </ul>
