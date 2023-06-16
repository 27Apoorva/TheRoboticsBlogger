---
title: "Rust For Robotics"
# excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard

excerpt_separator: <!--more-->

---

  <h1 style="text-align: center;margin-top:20px;margin-bottom-20px;" >Rust For Robotics</h1>

<!--excerpt.start-->
<p style="margin: 20px 3rem;">  
This blog is a written presentation of the talk I gave at ROS Meetup Delhi, India in April 2023. <br>
I was inspired by <a href="https://www.tangramvision.com/">Tangram Vision</a>’s work on Rust for Robotics and the blogs, and talks by <a href="https://www.linkedin.com/in/bminortx/">Brandon Minor, CEO</a>. </p>
<!--excerpt.end-->

<p style="text-align: left;margin: 20px 3rem;">So, I will start with asking a simple question. </p>

<h3 style="text-align: left;margin: 20px 3rem;">Why are Roboticist looking for a new programming language?</h3>

  <p style="text-align: left;margin: 20px 3rem;">As a Roboticist, my preferable coding language is C++ as this is the language that runs on the actual robots. Generally, Python-based ROS nodes suffer performance issues on hardware. Python and in some cases, Matlab are generally used for research and proof of concept purposes. <br>
C++ is well suited for embedded platforms as it can get <b>“Close to the metal”</b>.<br>
But C++ comes with its own set of problems:
  </p>

<ul style=" margin: 20px 3rem;">
      <li> <i>Portability between different platforms and operating systems</i><br>
      In a real-world scenario, my development system and deployment system would be quite different from each other as shown below.
      <img src="/assets/article4/image1.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>  
          The performance of the C++ code gets affected by the number of threads, and different operating systems, and isn’t consistent across different platforms.
      </li>
      <li><i>Slow Compile Time</i><br>
      Based on my experience, for about 20 ROS C++ packages, the code compile time was anywhere between 45 minutes to 1 hour. Of course, you can build only one package at a time during debugging but for verification and sanity checks, you will build the entire codebase with integration tests and if the bug is still present, the compile time adds up quickly to be very painful and could easily become an overhead.
      </li>
      <li><i>Cyclic Dependency</i><br>
      In ROS, Node 1 can depend on Node 2 for a .msg file. Node 2 depends on Node 3. Node 3 depends on Node 1 for a .msg file. This can lead to cyclic dependencies if the developer is not careful. 
      </li>
      <li><i>Manual Memory Management causes leaks and crashes</i><br>
      In C++, a developer needs to figure out when and where to use the mutex to prevent multiple threads from accessing the same data.
      </li>
      <li><i>There is no built-in memory safety</i>
      </li>
</ul>

  <h3 style="text-align: left;margin: 20px 3rem;">Hello, Rust!</h3>
  <p style="text-align: left;margin: 20px 3rem;">Rust is an open Source Systems Programming Language created by Mozilla Research Project.
Fun Fact: It was voted as the most loved language by StackOverflow four years in a row. It is developed with an emphasis on Safety, Speed, and Concurrency. It provides High-Level Abstraction and Low-Level control over system resources.<br><br>
Rust is based on two principles:<br>
<img src="/assets/article4/image2.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>  <br>
But why is there a Rust buzz? It will be quite evident soon how all the problems with C++ are magically taken care of by Rust.
  </p>
  <ul style=" margin: 20px 3rem;">
      <li><i>Portability</i><br>
        Rust is a cross-platform language and performance is consistent across different operating systems.
      </li>
      <li><i>Performance</i><br>
        There is zero cost for abstraction, and move semantics, leading to potentially faster code resolving the problem of slow compile times with C++.
      </li>
      <li><i>Painless Packaging and Dependency Management</i><br>
        Rust provides Cargo and Xargo for package management that can prevent cyclic dependency.
      </li>
      <li><i>Concurrency</i><br>
        Rust prevents data races and deadlocks. There is no need for manual management of mutexes and locks. 
      </li>
      <li><i>Memory Safety </i><br>
        Null pointers and dangling pointers are not allowed to prevent memory leaks.
      </li>
      <li><i>Type Inference and Efficient C Bindings</i><br>
        In short, if a function asks for degrees and you provide radians, Rust can automatically infer that type conversion is needed. And it will use the type conversion function from radians to degrees if it has been defined. How cool is that?
      </li>
      <li><i>Safety</i><br>
       It is very hard to write code with undefined behavior in Rust.
      </li>
      <li><i>Community</i><br>
      The Rust User Forum, internal forum, and chat platforms are heavily active to contribute, develop, and learn Rust. For more information, visit <a href="https://www.rust-lang.org/community">https://www.rust-lang.org/community</a>.
      </li>
</ul>

<p style="text-align: left;margin: 20px 3rem;">Before looking at Rust code, it is important to understand the basic Rust Terminologies.
<img src="/assets/article4/image3.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 55%;"/>  
  </p>

<h3 style="text-align: left;margin: 20px 3rem;">Ready to witness Rust's magic?</h3>
  <p style="text-align: left;margin: 20px 3rem;">In the below code, I have defined a dangling pointer. A dangling pointer is a pointer that doesn’t point to a valid object. 
<img src="/assets/article4/image4.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>  
I declare a mutable raw pointer <code style='color:orange'>p</code> as a null pointer in line 2 and I assign <code style='color:orange'>p</code> to a new pointer <code style='color:orange'>q</code>. 
Then I free the memory allocated to <code style='color:orange'>p</code> using the C free function. <br>
This leaves q as a dangling pointer since it still points to the memory location that was just freed.<br>
Finally, I attempt to print the value at <code style='color:orange'>q</code>, which leads to undefined behavior since the memory location it points to has been freed.<br>
Now, I know nobody would deliberately write such code but dangling pointers can exist under certain unknown circumstances in a fairly large codebase.
  <img src="/assets/article4/image5.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
  
  When I try to compile the code in Rust, the compiler throws an error and will not build the code at all. This will never happen in C++ and mostly, I would have to attach the debugger and spend hours finding the crash. <br>
That is how amazing is the safety provided by Rust. 
  </p>

  <h3 style="text-align: left;margin: 20px 3rem;">ROS and Rust</h3>
  <p style="text-align: left;margin: 20px 3rem;">Let’s take a turn and see how ROS and Rust interact with each other.<br>
Below are the Rust-based ROS packages available to begin development of Robotics code in Rust.</p>

<p style="text-align: center; margin: auto 3rem;">
<img src="/assets/article4/image6.png" alt="article image 1" style="display: block;
          padding: 1px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>  
Links are available in the Resources section.</p>

<p style="text-align: left;margin: 20px 3rem;">The wait is over and now I will show you an example of Rust in Robotics.<br>
I have a simple multi-threading model in ROS 2 shown below. By default, the ROS 2 C++ callbacks are sequential and not parallel. In this example, I have set up two string callbacks in ROS 2 both printing the incoming string from the topic.

  <img src="/assets/article4/image7.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
  
  Furthermore, I have added a 2 seconds wait in callback1. This causes the callback2 to be blocked by callback1 and the rate at which callback should be executed is not maintained as evidenced by the execution of the code. From the timestamp, it is seen that the code execution was; callback1 (16824198<b>71</b>.593) -> wait for 2 seconds -> print the incoming string ‘hey’ (16824198<b>73</b>.593) when callback2’s ‘oy’ message was blocked.

  <img src="/assets/article4/image8.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>

  Now imagine a robot’s camera image callback is blocked by another callback and the robot is operating on an older camera image for object detection. The robot will not have the latest information about the obstacles. Robots operating on delayed and old information can lead to horrible safety-related incidents and collisions.<br>
  ROS 2 does provide a solution that is <b><a href ="https://docs.ros.org/en/humble/Concepts/About-Executors.html">MultiThreadedExecuter</a></b> with callback groups. But it comes with the overhead of deadlocks, manual memory management, race condition, deciding the number of threads, and scheduling execution. All of them being standard problems with C++.
  Fortunately, there is Rust to the rescue. <br>
  The next code is an example of the same use case written in Rust where I have created two threads that can run each callback parallelly without blocking each other. 
  <img src="/assets/article4/image9.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
  From the below result, it is evident from the timestamp that callback1 is published after every 2 seconds while callback2 keeps receiving messages.

  <img src="/assets/article4/image10.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
  This example is for a very basic use case of publishing strings. Generally, I would want to extract data from the callbacks and use it elsewhere in the codebase. <br>

  Now, this is where things start getting complicated as there will be a case where one thread would be updating the data while another wants to access it simultaneously. 

  <img src="/assets/article4/image11.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/>
  In Rust, I can create an <code style='color:orange'>Arc</code> that allows multiple ownership while ensuring thread safety. Overall, in the first line of the example above, a thread-safe shared string is created that can be accessed and modified by multiple threads simultaneously without causing data races. In the second line, I create a clone of data1 since we need to pass it to another thread inside the callback. In this way, I can easily access the data while printing as well as inside the thread without manually managing and figuring out when to lock and unlock the mutex. 
  <br><br>
  Here are some companies already using Rust.
   <img src="/assets/article4/image12.png" alt="article image 1" style="display: block;
          padding: 10px;
          margin-left: auto;
          margin-right: auto;
          width: 50%;"/><br>
  As for Robotics, Rust is ready to be used for UI/Frontend, Webhooks, and systems programming.<br>
  While RUST is safe, efficient, and user-friendly, it is heavily under development, especially for ROS
  Also, C++ has been around for decades whereas Rust has been around only for about 10 years.
  In my opinion, Rust is very promising as witnessed in the blog but it will take time for Rust to become mainstream for Robotics.


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
      <a href="https://github.com/adnanademovic/rosrust">rosrust</a>
    </li>
    <li>
       <a href="https://github.com/ros2-rust/ros2_rust">ros2_rust</a>
    </li>
    <li>
      <a href="https://github.com/Carter12s/roslibrust">roslibrust</a>
    </li>
    <li>
       <a href="https://github.com/sequenceplanner/r2r">r2r</a>
    </li>
    <li>
      <a href="https://github.com/jhelovuo/RustDDS">RustDDS</a>
    </li>
    <li>
       <a href="https://github.com/rclrust/rclrust">rclrust</a>
    </li>
    <li>
      <a href="https://docs.rs/rosbag/latest/rosbag/">rosbag</a>
    </li>
    <li>
      <a href="https://github.com/arjo129/rustros_tf">rustros_tf</a>
    </li>
    <li>
      <a href="https://docs.rs/optimization_engine/latest/optimization_engine/">optimization-engine</a>
    </li>
    <li>
      <a href="https://robotics.rs/">https://robotics.rs/</a>
    </li>
    <li>
      <a href="https://www.tangramvision.com/blog/why-rust-for-robots">https://www.tangramvision.com/blog/why-rust-for-robots</a>
    </li>
    <li>
      <a href="https://medium.com/luos/why-rust-is-the-future-of-robotics-81d7fb68fe37">https://medium.com/luos/why-rust-is-the-future-of-robotics-81d7fb68fe37</a>
    </li>
    <li>
      <a href="https://doc.rust-lang.org/book/ch03-00-common-programming-concepts.html">https://doc.rust-lang.org/book/ch03-00-common-programming-concepts.html</a>
    </li>
    <li>
      <a href="https://roboticsbackend.com/ros-asyncspinner-example/">https://roboticsbackend.com/ros-asyncspinner-example/</a>
    </li>
  </ul>
