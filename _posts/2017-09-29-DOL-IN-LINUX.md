---
layout:     post
title:    " linux环境下的DOL配置 "
data:   2017-09-29
excerpt:   " linux环境下的DOL配置 "
---

#### 关于DOL（分布式操作层）

> 分布式操作层（DOL）是一种能够将应用程序自动映射到多处理器SHAPES架构平台上的框架。DOL由三部分组成：
>- DOL应用程序编程接口：DOL定义了一组计算和通信程序，可以对SHAPES平台的分布式并行应用程序进行编程。使用这些例程，应用程序员可以编写程序，而不需要有关底层架构的详细知识。实际上，这些例程在硬件依赖软件（HdS）层进一步细化。
>- DOL功能模拟： 为了向程序员提供测试应用程序的可能性，已经开发了功能模拟框架。除应用程序的功能验证外，该框架还用于在应用程序级别获取性能参数。
>- DOL映射优化：DOL映射优化 的目标是将应用程序的一组最佳映射计算到SHAPES架构平台上。在第一步中，已经定义了基于XML的规范格式，允许在抽象级别描述应用程序和架构。然而，包含获得准确性能估计所需的所有信息。
 
&emsp;&emsp;~~虽然还是不明白，但是感觉应该像是Dev帮我们自动配置好的编译环境,只不过这里需要我们自己在Linux系统下配置java的编译环境。~~

#### 关于Make工具
>- 在Linux和Ubuntu环境中，make工具主要被用来进行工程编译和程序链接
>- Makefile文件：告诉make以何种方式编译源代码和链接程序
>- make通过比较对应文件（规则的目标和依赖）的最后修改时间，来决定哪些文件需要更新、那些文件不需要更新

#### 关于Ant工具
>- Ant是一种基于Java的build工具
>- Ant用Java的类来扩展
>- Ant本身就是这样一个流程脚本引擎，用于自动化调用程序完成项目的编译，打包，测试等

#### 关于java和javac（上次死锁实验也用到了，但这里也简述一下）
>- 用途：编译或执行java代码
>- javac命令用来编译java文件
>-java命令可以执行生成的class文件

&emsp;&emsp;总而言之，以后的实验都是在Linux系统下使用java进行的，而这些环境是编译和运行程序必要的。上次的实验是手写了一个.bat文件，然后在terminal修改权限之后运行手写的java程序，所以应该用不到这些环境。 

#### 配置步骤(在terminal下进行)
1. 安装一些必要的环境（如解压软件）
    
>   $ sudo apt-get update      
    $ sudo apt-get install ant       
    $ sudo apt-get install openjdk-7-jdk（这里根据自己虚拟机情况，我的安装的是8）      
    $ sudo apt-get install unzip
2. 下载systenc和dol文件   
> sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip     

Linux可以直接通过“sudo wget ++link++”下载对应网页中的内容，直接放在document里。   
3. 解压文件   
>   $ sudo mkdir dol   &emsp;&emsp;  #新建dol的文件夹    
    $ sudo unzip dol_ethz.zip -d dol  &emsp;&emsp;  #将dolethz.zip解压到 dol文件夹中    
    $ sudo tar -zxvf systemc-2.3.1.tgz  &emsp;&emsp;  #解压systemc

4. 编译systemc    
>   $ cd systemc-2.3.1  &emsp;&emsp;  #解压后进入systemc-2.3.1的目录下    
    $ sudo mkdir objdir  &emsp;&emsp;  #新建一个临时文件夹objdir    
    $ cd objdir  &emsp;&emsp;  #进入该文件夹objdir    
    $ sudo ../configure CXX=g++ --disable-async-updates  &emsp;&emsp;  #运行configure(能根据系统的环境设置一下参数，用于编译)

运行configure后截图：
![image](http://own160w85.bkt.clouddn.com/dol1.png)

>   接上面编译systemc    
    $ sudo make install  &emsp;&emsp; #编译     
    $ cd ..        
    $ ls  &emsp;&emsp;  #编译完后文件目录    

![image](http://own160w85.bkt.clouddn.com/2.png)

>   接上面编译systemc    
    $ sudo pwd  &emsp;&emsp;  #记录当前的工作路径（后续更改路径时用到）
    
5. 编译dol   
>   $ cd ../dol  &emsp;&emsp;  #进入刚才dol的文件夹    
    修改build_zip.xml文件：    
    找到下面这段话，就是说上面编译的systemc位置在哪里    
==<property name="systemc.inc" value="YYY/include"/>    
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>==    
把YYY改成上页pwd的结果（注意，对于64位系统的机器，lib-linux要改成lib-linux64）    
    开始编译：    
    $ sudo ant -f build_zip.xml all   &emsp;&emsp;  #编译成功会显示build successful   
    尝试运行第一个例子    
    $ cd build/bin/main   &emsp;&emsp;  #进入build/bin/main路径下    
    $ sudo ant -f runexample.xml -Dnumber=1  &emsp;&emsp;  #运行第一个例子    

运行结果：    
![image](http://own160w85.bkt.clouddn.com/3.png)    

---
