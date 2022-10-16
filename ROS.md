详细资料：http://www.autolabor.com.cn/book/ROSTutorials/chapter1/11-rosjian-jie-yu-an-zhuang/112rosshe-ji-mu-biao.html

本文档为精简笔记



# ROS概述与环境搭建

### ROS的安装

> csdn
>
> 官网



### ROS是什么

> **ROS全称Robot Operating System(机器人操作系统)**
>
> - ROS是适用于机器人的**开源**元操作系统
> - ROS集成了大量的工具，库，协议，提供类似OS所提供的功能，简化对机器人的控制
> - 还提供了用于在**多台计算机**上获取，构建，编写和运行代码的工具和库，ROS在某些方面类似于“机器人框架”
> - ROS设计者将ROS表述为“ROS = Plumbing + Tools + Capabilities + Ecosystem”，即ROS是通讯机制、工具软件包、机器人高层技能以及机器人生态系统的集合体



> ROS  =  通信机制 + 开发工具 + 应用功能 + 生态系统（目的：提高软件复用率



> 通信机制：松耦合分布式通信
>
> 开发工具：命令行&编译器  TF坐标变换  QT工具箱  Rviz  Gazebo....
>
> 应用功能：Navigation  SLAM  Movelt... 
>
> 生态系统：发行版（Distribution）  软件源 （repository） ROS wiki（论坛）  邮件列表  ROS 			Answers（咨询问题的网站）  博客



### ROS的核心概念

> 节点（Node）——执行单元
>
> - 执行具体任务进程，独立运行的可执行文件
> - 不同节点可使用不同语言，分布式执行在不同电脑
> - 节点在系统中名称必须唯一



> 节点管理器（ROS Master）——控制中心
>
> - 为节点提供命名与注册服务
> - 记录话题、服务通信，辅助节点相互查找、建立连接
> - 提供参数服务器，节点使用此服务器存储和检索运行时的参数



> 话题（Topic）——异步通讯机制
>
> - 节点间传输数据的重要总线
> - 使用发布、订阅模型，数据由发布者传输到订阅者，同一话题的发布者或订阅者不唯一
> - 无反馈机制，有缓冲区，实时性弱，多用于数据传输



> 消息（Message）——话题数据
>
> - 具有一定类型和数据结构，包括ROS提供的标准类型和用户自定义类型
> - 使用编程语言无关的.msg文件定义，编译过程中生成对应的代码文件



> 服务（Service）——同步通信机制
>
> - 使用客户端、服务器模型，客户端发送请求数据，服务器完成处理后返回应答数据
> - 使用编程语言无关的.srv文件定义请求和应答数据结构，编译过程中生成对应的代码文件
> - 有反馈机制，无缓冲区，实时性强，多用于逻辑处理



> 参数（Parameter）——全局共享字典
>
> - 可通过网络访问的共享、多变量字典
> - 节点使用此服务器储存和检索运行时的参数
> - 适合储存静态、绯闻禁止的配置参数，不适合储存动态配置的数据  



> 功能包（Package）
>
> - ROS软件中的基本单元，包含节点源码、配置文件、数据定义等



> 功能包清单（Package manifest）
>
> - 记录功能包的基本信息，包含作者信息、许可信息、依赖选项、编译标志



> 元功能包（Meta Packages）
>
> - 组织多个用于同一目的功能包



### ROS命令行工具的使用

> rostopic rosservice rosnode rosparam rosmsg rossrv
>
> 输入命令行+回车可查看命令



例:小海龟

roscore：

> - 启动ROS Master：roscore
> - 启动小海龟仿真器：rosrun turtlesim(功能包名) turtlesim_node（节点）
> - 启动海龟控制节点：rosrun turtlesim turtle_teleop_key
> - 查看系统运行情况：rqt_graph

rosnode：

> - rosnode list:查看节点列表
> - rosnode info /节点：查看节点情况
> - rosnode ...

rostopic：

> - restopic list：查看话题列表
>
> - restopic pub (-r 10) /turtle1/cmd_vel cmd_vel 
>
>   geometry_msgs/Twist "linear:
>     x: 1.0
>     y: 0.0
>     z: 0.0
>   angular:
>     x: 0.0
>     y: 0.0
>     z: 1.0"  :publish信息给topic

rosmsg：

> - rosmsg show geometry_msgs/Twist  :显示message的含义
> - rosmsg ...

rosservice：

> - rosservice call /spawn "x: 2.0
>   y: 2.0
>   theta: 0.0
>   name: 'turtle2'"   :	call the service with the provided args
> - rosservice .....

话题复现：

> - 话题记录：rosbag record -a -O cmd_record
> - 话题复现：rosbag play cmd_record.bag

### 创建工作空间与功能包

#### 1. 创建工作空间：（类似于一个工程）

> src：代码空间（Source Space）
>
> build：编译空间（Build Space）
>
> devel：开发空间（Development Space）
>
> install：安装空间（Install Space）



> 创建工作空间：mkdir -p ~/catkin_ws(name)/src   (创建文件夹)
>
> ​                           cd~/catkin_ws/src     （切换路径）
>
> ​                            catkin_init_workspace    （创建工作空间）
>
> 编译工作空间：cd~/catkin_ws/  
>
> ​							catkin_make
>
> ​							catkin_make install  （创建install space）
>
> 设置环境变量:source devel/setup.bash（可以添加进`.bashrc`文件，使用上更方便）
>
> 检察环境变量:echo $ROS_PACKAGE_PATH



#### 2. 创建功能包：

> catkin_create_pkg <package_name> [depend1]  [depend2] [depend3]

> 创建：cd~/catkin_ws/src
>
> ​			catkin_create_pkg test_pkg cah	
>
> 编译：cd~/catkin_ws
>
> ​			catkin_make
>
> ​			source~/catkin_ws/devel/setup.bash		
>
> tips：同一个工作空间不能有同名功能包，不同工作空间可以存在同名工作包

### 资源整理

![image-20221016032349616](/home/szf/.config/Typora/typora-user-images/image-20221016032349616.png)

![image-20221016032417105](/home/szf/.config/Typora/typora-user-images/image-20221016032417105.png)

![image-20221016032436549](/home/szf/.config/Typora/typora-user-images/image-20221016032436549.png)





### ROS集成开发环境

#### 1.Terminator 常用快捷键

**第一部份：关于在同一个标签内的操作**

```xml
Alt+Up                          //移动到上面的终端
Alt+Down                        //移动到下面的终端
Alt+Left                        //移动到左边的终端
Alt+Right                       //移动到右边的终端
Ctrl+Shift+O                    //水平分割终端
Ctrl+Shift+E                    //垂直分割终端
Ctrl+Shift+Right                //在垂直分割的终端中将分割条向右移动
Ctrl+Shift+Left                 //在垂直分割的终端中将分割条向左移动
Ctrl+Shift+Up                   //在水平分割的终端中将分割条向上移动
Ctrl+Shift+Down                 //在水平分割的终端中将分割条向下移动
Ctrl+Shift+S                    //隐藏/显示滚动条
Ctrl+Shift+F                    //搜索
Ctrl+Shift+C                    //复制选中的内容到剪贴板
Ctrl+Shift+V                    //粘贴剪贴板的内容到此处
Ctrl+Shift+W                    //关闭当前终端
Ctrl+Shift+Q                    //退出当前窗口，当前窗口的所有终端都将被关闭
Ctrl+Shift+X                    //最大化显示当前终端
Ctrl+Shift+Z                    //最大化显示当前终端并使字体放大
Ctrl+Shift+N or Ctrl+Tab        //移动到下一个终端
Ctrl+Shift+P or Ctrl+Shift+Tab  //Crtl+Shift+Tab 移动到之前的一个终端
```

**有关各个标签之间的操作**

```
F11                             //全屏开关
Ctrl+Shift+T                    //打开一个新的标签
Ctrl+PageDown                   //移动到下一个标签
Ctrl+PageUp                     //移动到上一个标签
Ctrl+Shift+PageDown             //将当前标签与其后一个标签交换位置
Ctrl+Shift+PageUp               //将当前标签与其前一个标签交换位置
Ctrl+Plus (+)                   //增大字体
Ctrl+Minus (-)                  //减小字体
Ctrl+Zero (0)                   //恢复字体到原始大小
Ctrl+Shift+R                    //重置终端状态
Ctrl+Shift+G                    //重置终端状态并clear屏幕
Super+g                         //绑定所有的终端，以便向一个输入能够输入到所有的终端
Super+Shift+G                   //解除绑定
Super+t                         //绑定当前标签的所有终端，向一个终端输入的内容会自动输入到其他终端
Super+Shift+T                   //解除绑定
Ctrl+Shift+I                    //打开一个窗口，新窗口与原来的窗口使用同一个进程
Super+i                         //打开一个新窗口，新窗口与原来的窗口使用
```

#### 2. vscode 使用_基本配置

##### 1 创建 ROS 工作空间

```
mkdir -p xxx_ws/src(必须得有 src)
cd xxx_ws
catkin_make
Copy
```

##### 2 启动 vscode

进入 xxx_ws 启动 vscode

```
cd xxx_ws
code .
Copy
```

##### 3 vscode 中编译 ros

快捷键 ctrl + shift + B 调用编译，选择:`catkin_make:build`

可以点击配置设置为默认，修改.vscode/tasks.json 文件

```json
{
// 有关 tasks.json 格式的文档，请参见
    // https://go.microsoft.com/fwlink/?LinkId=733558
    "version": "2.0.0",
    "tasks": [
        {
            "label": "catkin_make:debug", //代表提示的描述性信息
            "type": "shell",  //可以选择shell或者process,如果是shell代码是在shell里面运行一个命令，如果是process代表作为一个进程来运行
            "command": "catkin_make",//这个是我们需要运行的命令
            "args": [],//如果需要在命令后面加一些后缀，可以写在这里，比如-DCATKIN_WHITELIST_PACKAGES=“pac1;pac2”
            "group": {"kind":"build","isDefault":true},
            "presentation": {
                "reveal": "always"//可选always或者silence，代表是否输出信息
            },
            "problemMatcher": "$msCompile"
        }
    ]
}
Copy
```

##### 4 创建 ROS 功能包

选定 src 右击 ---> create catkin package

**设置包名 添加依赖**（roscpp  rospy  std_msgs ....）



##### 5 C++ 实现

**在功能包的 src 下新建 cpp 文件**

```cpp
/*
    控制台输出 HelloVSCode !!!

*/
#include "ros/ros.h"

int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    //执行节点初始化
    ros::init(argc,argv,"HelloVSCode");

    //输出日志
    ROS_INFO("Hello VSCode!!!哈哈哈哈哈哈哈哈哈哈");
    return 0;
}
Copy
```

**PS1: 如果没有代码提示**

修改 .vscode/c_cpp_properties.json

设置 "cppStandard": "c++17"

**PS2: main 函数的参数不可以被 const 修饰**

**PS3: 当ROS__INFO 终端输出有中文时，会出现乱码**

[INFO](http://www.autolabor.com.cn/book/ROSTutorials/chapter1/14-ros-ji-cheng-kai-fa-huan-jing-da-jian/142-an-zhuang-vscode.html#): ????????????????????????

解决办法：在函数开头加入下面代码的任意一句

```cpp
setlocale(LC_CTYPE, "zh_CN.utf8");
setlocale(LC_ALL, "");
Copy
```

##### 6 python 实现

在 功能包 下新建 scripts 文件夹，添加 python 文件，**并添加可执行权限**

```py
#! /usr/bin/env python
"""
    Python 版本的 HelloVScode，执行在控制台输出 HelloVScode
    实现:
    1.导包
    2.初始化 ROS 节点
    3.日志输出 HelloWorld


"""

import rospy # 1.导包

if __name__ == "__main__":

    rospy.init_node("Hello_Vscode_p")  # 2.初始化 ROS 节点
    rospy.loginfo("Hello VScode, 我是 Python ....")  #3.日志输出 HelloWorld
Copy
```

##### 7 配置 CMakeLists.txt

C++ 配置:

```
add_executable(节点名称
  src/C++源文件名.cpp
)
target_link_libraries(节点名称
  ${catkin_LIBRARIES}
)
Copy
```

Python 配置:

```
catkin_install_python(PROGRAMS scripts/自定义文件名.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
Copy
```

##### 8 编译执行

编译: ctrl + shift + B

执行: 和之前一致，只是可以在 VScode 中添加终端，首先执行:`source ./devel/setup.bash`

PS:

如果不编译直接执行 python 文件，会抛出异常。

1.第一行解释器声明，可以使用绝对路径定位到 python3 的安装路径 #! /usr/bin/python3，但是不建议

2.建议使用 #!/usr/bin/env python 但是会抛出异常 : /usr/bin/env: “python”: 没有那个文件或目录

3.解决1: #!/usr/bin/env python3 直接使用 python3 但存在问题: 不兼容之前的 ROS 相关 python 实现

4.解决2: 创建一个链接符号到 python 命令:`sudo ln -s /usr/bin/python3 /usr/bin/python`

#### 3. launch文件演示

#### 1.需求

> 一个程序中可能需要启动多个节点，比如:ROS 内置的小乌龟案例，如果要控制乌龟运动，要启动多个窗口，分别启动 roscore、乌龟界面节点、键盘控制节点。如果每次都调用 rosrun 逐一启动，显然效率低下，如何优化?

官方给出的优化策略是使用 launch 文件，可以一次性启动多个 ROS 节点。

#### 2.实现

1. 选定功能包右击 ---> 添加 launch 文件夹

2. 选定 launch 文件夹右击 ---> 添加 launch 文件

3. 编辑 launch 文件内容

   ```
   <launch>
       <node pkg="helloworld" type="demo_hello" name="hello" output="screen" />
       <node pkg="turtlesim" type="turtlesim_node" name="t1"/>
       <node pkg="turtlesim" type="turtle_teleop_key" name="key1" />
   </launch>
   ```

   - node ---> 包含的某个节点
   - pkg -----> 功能包
   - type ----> 被运行的节点文件
   - name --> 为节点命名
   - output-> 设置日志的输出目标

4. 运行 launch 文件

   `roslaunch 包名 launch文件名`

5. 运行结果: 一次性启动了多个节点

### ROS架构

接下来，我们要从宏观上来介绍一下ROS的架构设计。

立足不同的角度，对ROS架构的描述也是不同的，一般我们可以从设计者、维护者、系统结构与自身结构4个角度来描述ROS结构:

#### 1.设计者

ROS**设计者**将ROS表述为“ROS = Plumbing + Tools + Capabilities + Ecosystem”

- Plumbing: **通讯机制(实现ROS不同节点之间的交互)**
- Tools :**工具软件包(ROS中的开发和调试工具)**
- Capabilities :机器人高层技能(ROS中某些功能的集合，比如:导航)
- Ecosystem:机器人生态系统(跨地域、跨软件与硬件的ROS联盟)

#### 2.维护者

立足**维护者**的角度: ROS 架构可划分为两大部分

- main：核心部分，主要由Willow Garage 和一些开发者设计、提供以及维护。它提供了一些分布式计算的基本工具，以及整个ROS的核心部分的程序编写。
- universe：全球范围的代码，有不同国家的ROS社区组织开发和维护。一种是库的代码，如OpenCV、PCL等；库的上一层是从功能角度提供的代码，如人脸识别，他们调用下层的库；最上层的代码是应用级的代码，让机器人完成某一确定的功能。

#### 3.系统架构

立足系统架构: ROS 可以划分为三层

- OS 层，也即经典意义的操作系统

  ROS 只是元操作系统，需要依托真正意义的操作系统，目前兼容性最好的是 Linux 的 Ubuntu，Mac、Windows 也支持 ROS 的较新版本

- 中间层

  是 ROS 封装的关于机器人开发的中间件，比如:

  - 基于 TCP/UDP 继续封装的 TCPROS/UDPROS 通信系统
  - 用于进程间通信 Nodelet，为数据的实时性传输提供支持
  - 另外，还提供了大量的机器人开发实现库，如：数据类型定义、坐标变换、运动控制....

- 应用层

  功能包，以及功能包内的节点，比如: master、turtlesim的控制与运动节点...

#### 4.自身结构

就 ROS 自身实现而言: 也可以划分为三层

- 文件系统

  ROS文件系统级指的是在硬盘上面查看的ROS源代码的组织形式

- 计算图

  ROS 分布式系统中不同进程需要进行数据交互，计算图可以以点对点的网络形式表现数据交互过程，计算图中的重要概念: 节点(Node)、消息(message)、通信机制_主题(topic)、通信机制_服务(service)

- 开源社区

  ROS的社区级概念是ROS网络上进行代码发布的一种表现形式

  - 发行版（Distribution）　ROS发行版是可以独立安装、带有版本号的一系列综合功能包。ROS发行版像Linux发行版一样发挥类似的作用。这使得ROS软件安装更加容易，而且能够通过一个软件集合维持一致的版本。
  - 软件库（Repository）　ROS依赖于共享开源代码与软件库的网站或主机服务，在这里不同的机构能够发布和分享各自的机器人软件与程序。
  - ROS维基（ROS Wiki）　ROS Wiki是用于记录有关ROS系统信息的主要论坛。任何人都可以注册账户、贡献自己的文件、提供更正或更新、编写教程以及其他行为。网址是http://wiki.ros.org/。
  - Bug提交系统（Bug Ticket System）如果你发现问题或者想提出一个新功能，ROS提供这个资源去做这些。
  - 邮件列表（Mailing list）　ROS用户邮件列表是关于ROS的主要交流渠道，能够像论坛一样交流从ROS软件更新到ROS软件使用中的各种疑问或信息。网址是http://lists.ros.org/。
  - ROS问答（ROS Answer）用户可以使用这个资源去提问题。网址是https://answers.ros.org/questions/。
  - 博客（Blog）你可以看到定期更新、照片和新闻。网址是https://www.ros.org/news/，不过博客系统已经退休，ROS社区取而代之，网址是https://discourse.ros.org/。

































































# ROS通信机制

## <话题通信模型>

![话题模型](/home/szf/图片/话题模型.png)

### 模型概述

话题通信是ROS中使用频率最高的一种通信模式，话题通信是基于**发布订阅**模式的，也即:一个节点发布消息，另一个节点订阅该消息。话题通信的应用场景也极其广泛，比如下面一个常见场景:

> 机器人在执行导航功能，使用的传感器是激光雷达，机器人会采集激光雷达感知到的信息并计算，然后生成运动控制信息驱动机器人底盘运动。

在上述场景中，就不止一次使用到了话题通信。

- 以激光雷达信息的采集处理为例，在 ROS 中有一个节点需要时时的发布当前雷达采集到的数据，导航模块中也有节点会订阅并解析雷达数据。
- 再以运动消息的发布为例，导航模块会根据传感器采集的数据时时的计算出运动控制信息并发布给底盘，底盘也可以有一个节点订阅运动信息并最终转换成控制电机的脉冲信号。

以此类推，像雷达、摄像头、GPS.... 等等一些传感器数据的采集，也都是使用了话题通信，换言之，话题通信适用于不断更新的数据传输相关的应用场景。



### 发布者publisher的编程实现

创建功能包：

> cd~/catkin_ws/src
>
> catkin_create_pkg learning_topic std_msgs rospy roscpp geometry_msgs turtlesim

创建发布者代码（c++）

> - 初始化ROS节点
> - 向ROS Master注册节点信息，包括话题名和话题中的消息类型
> - 创建消息数据
> - 按一定频率循环发布消息

例程：

```c++
/**
 * 该例程将发布turtle1/cmd_vel话题，消息类型geometry_msgs::Twist
 */

#include <ros/ros.h>
#include <geometry_msgs/Twist.h>

int main(int argc, char **argv)
{
        // ROS节点初始化
        ros::init(argc, argv, "velocity_publisher");

        // 创建节点句柄
        ros::NodeHandle n;

        // 创建一个Publisher，发布名为/turtle1/cmd_vel的topic，消息类型为geometry_msgs::Twist，队列长度10
        ros::Publisher turtle_vel_pub = n.advertise<geometry_msgs::Twist>("/turtle1/cmd_vel", 10);

        // 设置循环的频率
        ros::Rate loop_rate(10);

        int count = 0;
        while (ros::ok())
        {
            // 初始化geometry_msgs::Twist类型的消息
                geometry_msgs::Twist vel_msg;
                vel_msg.linear.x = 0.5;
                vel_msg.angular.z = 0.2;

            // 发布消息
                turtle_vel_pub.publish(vel_msg);
                ROS_INFO("Publsh turtle velocity command[%0.2f m/s, %0.2f rad/s]",
                                vel_msg.linear.x, vel_msg.angular.z);

            // 按照循环频率延时
            loop_rate.sleep();
        }

        return 0;
}      
```

配置发布者代码编译规则：

> 设置需要编译的代码和生成的可执行文 ; 
>
> add_executable(velocity_publisher src/velocity_publisher.cpp)
>
> 设置链接库；
>
> target_link_libraries(velocity_publisher ${catkin_LIBRARIES})
>
> 加入CMakeLists.txt

例程：

```cmake
## Add cmake target dependencies of the executable
## same as for the library above
# add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
# target_link_libraries(${PROJECT_NAME}_node
#   ${catkin_LIBRARIES}
# )

add_executable(velocity_publisher src/velocity_publisher.cpp)
target_link_libraries(velocity_publisher ${catkin_LIBRARIES})
```

编译并运行发布者：

> cd~/catkin_ws/  
>
> catkin_make
>
> source devel/setup.bash

> roscore
>
> rosrun turtlesim turtlesim_node
>
> rosrun learning_topic velocity_publisher

### 订阅者Subscriber的编程实现

创建订阅者代码：

> - 初始化ROS节点；
> - 订阅需要的话题
> - 循环等待话题消息，接收到消息后进入回调函数
> - 在回调函数中完成消息处理

例程：

```c++
/**
 * 该例程将订阅/turtle1/pose话题，消息类型turtlesim::Pose
 */

#include <ros/ros.h>
#include "turtlesim/Pose.h"

// 接收到订阅的消息后，会进入消息回调函数
void poseCallback(const turtlesim::Pose::ConstPtr& msg)
{
    // 将接收到的消息打印出来
    ROS_INFO("Turtle pose: x:%0.6f, y:%0.6f", msg->x, msg->y);
}

int main(int argc, char **argv)
{
    // 初始化ROS节点
    ros::init(argc, argv, "pose_subscriber");

    // 创建节点句柄
    ros::NodeHandle n;

    // 创建一个Subscriber，订阅名为/turtle1/pose的topic，注册回调函数poseCallback
    ros::Subscriber pose_sub = n.subscribe("/turtle1/pose", 10, poseCallback);

    // 循环等待回调函数
    ros::spin();

    return 0;
}

```

配置订阅者代码编译规则：CMakeLists.txt

> - 设置需要编译的代码和生成的可执行文件
> - 设置链接库

例程：

```cmake
## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide
# add_executable(${PROJECT_NAME}_node src/learning_topic_node.cpp)

## Rename C++ executable without prefix
## The above recommended prefix causes long target names, the following renames the
## target back to the shorter version for ease of user use
## e.g. "rosrun someones_pkg node" instead of "rosrun someones_pkg someones_pkg_node"
# set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")

## Add cmake target dependencies of the executable
## same as for the library above
# add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
# target_link_libraries(${PROJECT_NAME}_node
#   ${catkin_LIBRARIES}
# )

add_executable(velocity_publisher src/velocity_publisher.cpp)
target_link_libraries(velocity_publisher ${catkin_LIBRARIES})

add_executable(pose_subscriber src/pose_subscriber.cpp)
target_link_libraries(pose_subscriber ${catkin_LIBRARIES})
```

### 话题消息的定义与使用

如何自定义话题消息：

> 1. 定义msg文件   创建msg文件夹，创建Person.msg文本文件，定义消息
>
>    ```c++
>    string name
>    uint8 sex
>    uint8 age
>    
>    uint8 unknown = 0
>    uint8 male    = 1
>    uint8 female  = 2
>    ```

> 2. 在package.xml中添加功能包依赖
>
>    ​      <build_depend>message_generation</build_depend>
>    ​      <exec_depend>message_runtime</exec_depend>
>
> ```xml
> <?xml version="1.0"?>
> <package format="2">
>   <name>learning_topic</name>
>   <version>0.0.0</version>
>   <description>The learning_topic package</description>
> 
>   <!-- One maintainer tag required, multiple allowed, one person per tag -->
>   <!-- Example:  -->
>   <!-- <maintainer email="jane.doe@example.com">Jane Doe</maintainer> -->
>   <maintainer email="szf@todo.todo">szf</maintainer>
> 
> 
>   <!-- One license tag required, multiple allowed, one license per tag -->
>   <!-- Commonly used license strings: -->
>   <!--   BSD, MIT, Boost Software License, GPLv2, GPLv3, LGPLv2.1, LGPLv3 -->
>   <license>TODO</license>
> 
> 
>   <!-- Url tags are optional, but multiple are allowed, one per tag -->
>   <!-- Optional attribute type can be: website, bugtracker, or repository -->
>   <!-- Example: -->
>   <!-- <url type="website">http://wiki.ros.org/learning_topic</url> -->
> 
> 
>   <!-- Author tags are optional, multiple are allowed, one per tag -->
>   <!-- Authors do not have to be maintainers, but could be -->
>   <!-- Example: -->
>   <!-- <author email="jane.doe@example.com">Jane Doe</author> -->
> 
> 
>   <!-- The *depend tags are used to specify dependencies -->
>   <!-- Dependencies can be catkin packages or system dependencies -->
>   <!-- Examples: -->
>   <!-- Use depend as a shortcut for packages that are both build and exec dependencies -->
>   <!--   <depend>roscpp</depend> -->
>   <!--   Note that this is equivalent to the following: -->
>   <!--   <build_depend>roscpp</build_depend> -->
>   <!--   <exec_depend>roscpp</exec_depend> -->
>   <!-- Use build_depend for packages you need at compile time: -->
>   <!--   <build_depend>message_generation</build_depend> -->
>   <!-- Use build_export_depend for packages you need in order to build against this package: -->
>   <!--   <build_export_depend>message_generation</build_export_depend> -->
>   <!-- Use buildtool_depend for build tool packages: -->
>   <!--   <buildtool_depend>catkin</buildtool_depend> -->
>   <!-- Use exec_depend for packages you need at runtime: -->
>   <!--   <exec_depend>message_runtime</exec_depend> -->
>   <!-- Use test_depend for packages you need only for testing: -->
>   <!--   <test_depend>gtest</test_depend> -->
>   <!-- Use doc_depend for packages you need only for building documentation: -->
>   <!--   <doc_depend>doxygen</doc_depend> -->
>   <buildtool_depend>catkin</buildtool_depend>
>   <build_depend>geometry_msgs</build_depend>
>   <build_depend>roscpp</build_depend>
>   <build_depend>rospy</build_depend>
>   <build_depend>std_msgs</build_depend>
>   <build_depend>turtlesim</build_depend>
>   <build_export_depend>geometry_msgs</build_export_depend>
>   <build_export_depend>roscpp</build_export_depend>
>   <build_export_depend>rospy</build_export_depend>
>   <build_export_depend>std_msgs</build_export_depend>
>   <build_export_depend>turtlesim</build_export_depend>
>   <exec_depend>geometry_msgs</exec_depend>
>   <exec_depend>roscpp</exec_depend>
>   <exec_depend>rospy</exec_depend>
>   <exec_depend>std_msgs</exec_depend>
>   <exec_depend>turtlesim</exec_depend>
> 
>           <build_depend>message_generation</build_depend>
>           <exec_depend>message_runtime</exec_depend>
>           
>   <!-- The export tag contains other, unspecified, tags -->
>   <export>
>     <!-- Other tools can request additional information be placed here -->
> 
>   </export>
> </package>
> ```
>
> 3.在CMakeLists.txt添加编译选项
>
> - find_package(.......message_generation)
>
> ```cmake
> ## Find catkin macros and libraries
> ## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
> ## is used, also find other catkin packages
> find_package(catkin REQUIRED COMPONENTS
>   geometry_msgs
>   roscpp
>   rospy
>   std_msgs
>   turtlesim
>   message_generation
> )
> ```
>
> - add_message_files(FILES Person.msg)
>   generate_messages(DEPENDENCIES std_msgs)
>
> ```cmake
> ## Generate added messages and services with any dependencies listed here
> # generate_messages(
> #   DEPENDENCIES
> #   geometry_msgs#   std_msgs
> # )
> 
> add_message_files(FILES Person.msg)
> generate_messages(DEPENDENCIES std_msgs)
> ```
>
> - catkin_package(...... message_runtime)
>
> ```cmake
> ###################################
> ## catkin specific configuration ##
> ###################################
> ## The catkin_package macro generates cmake config files for your package
> ## Declare things to be passed to dependent projects
> ## INCLUDE_DIRS: uncomment this if your package contains header files
> ## LIBRARIES: libraries you create in this project that dependent projects also need
> ## CATKIN_DEPENDS: catkin_packages dependent projects also need
> ## DEPENDS: system dependencies of this project that dependent projects also need
> catkin_package(
> #  INCLUDE_DIRS include
> #  LIBRARIES learning_topic
>    CATKIN_DEPENDS geometry_msgs roscpp rospy std_msgs turtlesim message_runtime
> #  DEPENDS system_lib
> )
> ```
>
> 配置订阅者、发布者的代码编译规则
>
> - add_executable(person_publisher src/person_publisher.cpp)
>   target_link_libraries(person_publisher ${catkin_LIBRARIES})
>   add_dependencies(person_publisher ${PROJECT_NAME}_generate_messages_cpp)
>
>   add_executable(person_subscriber src/person_subscriber.cpp)
>   target_link_libraries(person_subscriber ${catkin_LIBRARIES})
>   add_dependencies(person_subscriber ${PROJECT_NAME}_generate_messages_cpp)
>
> ```cmake
> ## Rename C++ executable without prefix
> ## The above recommended prefix causes long target names, the following renames the
> ## target back to the shorter version for ease of user use
> ## e.g. "rosrun someones_pkg node" instead of "rosrun someones_pkg someones_pkg_node"
> # set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")
> 
> ## Add cmake target dependencies of the executable
> ## same as for the library above
> # add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
> 
> ## Specify libraries to link a library or executable target against
> # target_link_libraries(${PROJECT_NAME}_node
> #   ${catkin_LIBRARIES}
> # )
> 
> add_executable(velocity_publisher src/velocity_publisher.cpp)
> target_link_libraries(velocity_publisher ${catkin_LIBRARIES})
> 
> add_executable(pose_subscriber src/pose_subscriber.cpp)
> target_link_libraries(pose_subscriber ${catkin_LIBRARIES})
> 
> add_executable(person_publisher src/person_publisher.cpp)
> target_link_libraries(person_publisher ${catkin_LIBRARIES})
> add_dependencies(person_publisher ${PROJECT_NAME}_generate_messages_cpp)
> 
> 
> add_executable(person_subscriber src/person_subscriber.cpp)
> target_link_libraries(person_subscriber ${catkin_LIBRARIES})
> add_dependencies(person_subscriber ${PROJECT_NAME}_generate_messages_cpp)
> 
> ```
>
> 编译，运行两个程序即可

## <服务模型>

> ![服务模型](/home/szf/图片/服务模型.png)

### 客户端Client的编程实现

创建功能包：

> catkin_create_pkg <package_name> [depend1]  [depend2] [depend3]

> 创建：cd~/catkin_ws/src
>
> ​            catkin_create_pkg learning_service std_msgs rospy roscpp geometry_msgs turtlesim
>
> 编译：cd~/catkin_ws
>
> ​			catkin_make
>
> ​			//source~/catkin_ws/devel/setup.bash		
>

创建客户端代码：

> - 初始化ROS节点
> - 创建一个Client实例
> - 发布服务请求数据
> - 等待Server处理之后的应答结果

例程：

```c++
/**
 * 该例程将请求/spawn服务，服务数据类型turtlesim::Spawn
 */

#include <ros/ros.h>
#include <turtlesim/Spawn.h>

int main(int argc, char** argv)
{
    // 初始化ROS节点
	ros::init(argc, argv, "turtle_spawn");

    // 创建节点句柄
	ros::NodeHandle node;

    // 发现/spawn服务后，创建一个服务客户端，连接名为/spawn的service
	ros::service::waitForService("/spawn");
	ros::ServiceClient add_turtle = node.serviceClient<turtlesim::Spawn>("/spawn");

    // 初始化turtlesim::Spawn的请求数据
	turtlesim::Spawn srv;
	srv.request.x = 2.0;
	srv.request.y = 2.0;
	srv.request.name = "turtle2";

    // 请求服务调用
	ROS_INFO("Call service to spwan turtle[x:%0.6f, y:%0.6f, name:%s]", 
			 srv.request.x, srv.request.y, srv.request.name.c_str());

	add_turtle.call(srv);

	// 显示服务调用结果
	ROS_INFO("Spwan turtle successfully [name:%s]", srv.response.name.c_str());

	return 0;
};
```

配置客户端代码编译规则：

> add_executable(turtle_spawn src/turtle_spawn.cpp)
> target_link_libraries(turtle_spawn ${catkin_LIBRARIES})

```cmake

## Add cmake target dependencies of the executable
## same as for the library above
# add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
# target_link_libraries(${PROJECT_NAME}_node
#   ${catkin_LIBRARIES}
# )

add_executable(turtle_spawn src/turtle_spawn.cpp)
target_link_libraries(turtle_spawn ${catkin_LIBRARIES})
```

编译运行

> cd~/catkin_ws
>
> catkin_make
>
> roscore
>
> rosrun turtlesim turtlesim_node
>
> rosrun learning_service turtle_spawn

### 服务端Server的编程实现

实现一个服务器：

> - 初始化ROS节点；
> - 创建Server实例；
> - 循环等待服务请求，进入回调函数；
> - 在回调函数中完成服务功能功能的处理，并反馈应答数据。

```c++
/**
 * 该例程将执行/turtle_command服务，服务数据类型std_srvs/Trigger
 */
 
#include <ros/ros.h>
#include <geometry_msgs/Twist.h>
#include <std_srvs/Trigger.h>

ros::Publisher turtle_vel_pub;
bool pubCommand = false;

// service回调函数，输入参数req，输出参数res
bool commandCallback(std_srvs::Trigger::Request  &req,
         			std_srvs::Trigger::Response &res)
{
	pubCommand = !pubCommand;

    // 显示请求数据
    ROS_INFO("Publish turtle velocity command [%s]", pubCommand==true?"Yes":"No");

	// 设置反馈数据
	res.success = true;
	res.message = "Change turtle command state!"

    return true;
}

int main(int argc, char **argv)
{
    // ROS节点初始化
    ros::init(argc, argv, "turtle_command_server");

    // 创建节点句柄
    ros::NodeHandle n;

    // 创建一个名为/turtle_command的server，注册回调函数commandCallback
    ros::ServiceServer command_service = n.advertiseService("/turtle_command", commandCallback);

	// 创建一个Publisher，发布名为/turtle1/cmd_vel的topic，消息类型为geometry_msgs::Twist，队列长度10
	turtle_vel_pub = n.advertise<geometry_msgs::Twist>("/turtle1/cmd_vel", 10);

    // 循环等待回调函数
    ROS_INFO("Ready to receive turtle command.");

	// 设置循环的频率
	ros::Rate loop_rate(10);

	while(ros::ok())
	{
		// 查看一次回调函数队列
    	ros::spinOnce();
		
		// 如果标志为true，则发布速度指令
		if(pubCommand)
		{
			geometry_msgs::Twist vel_msg;
			vel_msg.linear.x = 0.5;
			vel_msg.angular.z = 0.2;
			turtle_vel_pub.publish(vel_msg);
		}

		//按照循环频率延时
	    loop_rate.sleep();
	}

    return 0;
}

```

配置客户端代码编译规则：

编译

运行![服务端编程实现](/home/szf/图片/服务端编程实现.png)

### 服务数据的定义与使用

定义srv文件:

> - 创建srv文件夹，在srv文件夹中创建person.srv文件

> - 在person.srv中定义数据
>
> - ```c++
>   string name
>   uint8  age
>   uint8  sex
>   
>   uints8 unkuown = 0
>   uint8 male   = 1
>   uint8 female = 2
>   ---
>   string result
>   ```

在package.xml中添加功能包依赖

> - ```xml
>     <!--   <build_export_depend>message_generation</build_export_depend> -->
>     <!-- Use buildtool_depend for build tool packages: -->
>     <!--   <buildtool_depend>catkin</buildtool_depend> -->
>     <!-- Use exec_depend for packages you need at runtime: -->
>     <!--   <exec_depend>message_runtime</exec_depend> -->
>     <!-- Use test_depend for packages you need only for testing: -->
>     <!--   <test_depend>gtest</test_depend> -->
>     <!-- Use doc_depend for packages you need only for building documentation: -->
>     <!--   <doc_depend>doxygen</doc_depend> -->
>     <buildtool_depend>catkin</buildtool_depend>
>     <build_depend>geometry_msgs</build_depend>
>     <build_depend>roscpp</build_depend>
>     <build_depend>rospy</build_depend>
>     <build_depend>std_msgs</build_depend>
>     <build_depend>turtlesim</build_depend>
>     <build_export_depend>geometry_msgs</build_export_depend>
>     <build_export_depend>roscpp</build_export_depend>
>     <build_export_depend>rospy</build_export_depend>
>     <build_export_depend>std_msgs</build_export_depend>
>     <build_export_depend>turtlesim</build_export_depend>
>     <exec_depend>geometry_msgs</exec_depend>
>     <exec_depend>roscpp</exec_depend>
>     <exec_depend>rospy</exec_depend>
>     <exec_depend>std_msgs</exec_depend>
>     <exec_depend>turtlesim</exec_depend>
>     
>     <build_depend>message_generation</build_depend>
>     <exec_depend>message_runtime</exec_depend>
>   ```
>
>   

在CMskeLists.txt添加编译选项(参考话题消息）

> - find_package(.......message_generation)
>
> - add_service_files(FILES Person.srv)
>
>   generate_messages(DEPENDENCIES std_msgs)
>
> - catkin_package(...... message_runtime)

编译生成语言相关文件

编写客户端、服务端代码：

```c++

/**
 * 该例程将执行/show_person服务，服务数据类型learning_service::Person
 */
 
#include <ros/ros.h>
#include "learning_service/Person.h"

// service回调函数，输入参数req，输出参数res
bool personCallback(learning_service::Person::Request  &req,
         			learning_service::Person::Response &res)
{
    // 显示请求数据
    ROS_INFO("Person: name:%s  age:%d  sex:%d", req.name.c_str(), req.age, req.sex);

	// 设置反馈数据
	res.result = "OK";

    return true;
}

int main(int argc, char **argv)
{
    // ROS节点初始化
    ros::init(argc, argv, "person_server");

    // 创建节点句柄
    ros::NodeHandle n;

    // 创建一个名为/show_person的server，注册回调函数personCallback
    ros::ServiceServer person_service = n.advertiseService("/show_person", personCallback);

    // 循环等待回调函数
    ROS_INFO("Ready to show person informtion.");
    ros::spin();

    return 0;
}


```

```c++

/**
 * 该例程将请求/show_person服务，服务数据类型learning_service::Person
 */

#include <ros/ros.h>
#include "learning_service/Person.h"

int main(int argc, char** argv)
{
    // 初始化ROS节点
	ros::init(argc, argv, "person_client");

    // 创建节点句柄
	ros::NodeHandle node;

    // 发现/spawn服务后，创建一个服务客户端，连接名为/spawn的service
	ros::service::waitForService("/show_person");
	ros::ServiceClient person_client = node.serviceClient<learning_service::Person>("/show_person");

    // 初始化learning_service::Person的请求数据
	learning_service::Person srv;
	srv.request.name = "Tom";
	srv.request.age  = 20;
	srv.request.sex  = learning_service::Person::Request::male;

    // 请求服务调用
	ROS_INFO("Call service to show person[name:%s, age:%d, sex:%d]", 
			 srv.request.name.c_str(), srv.request.age, srv.request.sex);

	person_client.call(srv);

	// 显示服务调用结果
	ROS_INFO("Show person result : %s", srv.response.result.c_str());

	return 0;
}
```

配置服务器、客户端代码编译规则（参考消息的定义与使用）

> add_executable(person_server src/person_server.cpp)
> target_link_libraries(person_server ${catkin_LIBRARIES})
> add_dependencies(person_server ${PROJECT_NAME}_gencpp)
>
> add_executable(person_client src/person_client.cpp)
> target_link_libraries(person_client ${catkin_LIBRARIES})
> add_dependencies(person_client ${PROJECT_NAME}_gencpp)

编译，运行

![服务消息](/home/szf/图片/服务消息.png)

## <参数服务器>

### 参数的使用与编程方法

- 参数模型

![image-20221016031518224](/home/szf/.config/Typora/typora-user-images/image-20221016031518224.png)







- 