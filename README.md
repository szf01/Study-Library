# 项目内容

学习精简笔记及资料总结

# ROS

- [详细资料](http://www.autolabor.com.cn/book/ROSTutorials/chapter1/11-rosjian-jie-yu-an-zhuang/112rosshe-ji-mu-biao.html)
- [官网](http://wiki.ros.org/)，右上角有搜索功能
- [ROS源代码](https://github.com/ros)
- [answers搜索](http://answers.ros.org)或者邮件列表归档
- [提问](http://answers.ros.org/questions/ask)上提问。

# Markdown

- [csdn 语法手册](https://blog.csdn.net/witnessai1/article/details/52551362?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166592044816782391813984%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166592044816782391813984&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-52551362-null-null.142^v56^control,201^v3^add_ask&utm_term=markdown&spm=1018.2226.3001.4187) 

- [Markdown指南网站](https://www.markdownguide.org/getting-started/)
- [约翰·格鲁伯的《马克当》文档](https://daringfireball.net/projects/markdown/)，由马克当的创建者编写的原始指南。
- [降价教程](https://www.markdowntutorial.com/)，一个开源网站，允许您在网络浏览器中尝试Markdown。
- [真棒马克当](https://github.com/mundimark/awesome-markdown)，降价工具和学习资源的列表。
- [排版降价](https://dave.autonoma.ca/blog/2019/05/22/typesetting-markdown-part-1)，一个由多个部分组成的系列，描述了一个使用[潘多克](https://pandoc.org/)和[ConTeXt](https://www.contextgarden.net/) ，对 Markdown 文档进行排版的生态系统。

# Vscode配置

# STM32

- 外部中断（编码器AMT102）
- 定时器
- 串口调试 VOFA+

# CPP

- 资源：
- 踩坑：
1. 无法debug，编译"xxx exe Permission denied"：可能程序陷入死循环，任务管理器结束进程，并修改程序，重新编译即可，[参考](https://blog.csdn.net/gruhgd/article/details/83927041)
2. 编译报错"Error：redefinition of class xxx" : .h文件没有#pragma once ， [参考](https://blog.csdn.net/qq_31347869/article/details/94085312)
# Cmake(Windows)
- [vscode中使用视频教程](https://www.bilibili.com/video/BV13K411M78v?p=2&vd_source=baa784078e67e28c38d26cf6881f8357)
- 配置环境：g++ gcc cmake vscode cmake插件 cmaketools插件
- 基于g++命令,生成带调试信息的可执行文件：
    > g++ -g xx.cpp xxx.cpp -o xx(可执行文件的名字)
- 基于cmake:
  新建并编写CMakelists.txt
    > project(NAME)
    
    > add_executable(name xx.cpp xxx.cpp)
  进行多文件编译，调试（插件自动完成）
  
    > mkdir build
    
    > cd build
    
    > cmake ..
    
    > #如果电脑已经安装VS 可能会调用微软MSVC编译器，第一次使用（cmake -G "MinGW Makefiles" ..），后面还是（cmake ..）
    
    > mingw32-make.exe
    
 - 配置json
  可以参考Study-Code仓库



