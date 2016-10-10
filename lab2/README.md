# Lab1:DOL开发环境配置
作者:14M2 罗逸轩 14353227
***
## 一、工具简介
#### 1、Make工具
在Linux和Ubuntu环境中，make工具主要被用来进行工程编译和程序链接。<br>
Makefile文件：告诉make以何种方式编译源代码和链接程序。<br>
make通过比较对应文件（规则的目标和依赖）的最后修改时间，来决定哪些文件需要更新、那些文件不需要更新。
#### 2、Ant工具
Ant是一种基于Java的build工具。它用Java的类来扩展。其本身就是这样一个流程脚本引擎，用于自动化调用程序完成项目的编译，打包，测试等。<br>
Ant的优点如下：<br>
·跨平台性。Ant是纯java语言编写的，所示具有很好的跨平台性。<br>
·操作简单。Ant是由一个内置任务和可选任务组成的。Ant运行时需要一个XML文件(构建文件)。<br>
·容易维护和书写，结构清晰。<br>
·Ant可以集成到开发环境中。
#### 3、Java与Javac简介
他们的用途是编译或执行java代码。javac命令用来编译java文件，而java命令可以执行生成的class文件。
## 二、安装过程
#### 1、Linux系统安装
实验课所要求的实验环境在linux下进行，因此，需要安装虚拟机Ubuntu。本人采用的是在VMWARE下安装Ubuntu的方式
#### 2、必要环境的安装
在这里，我们需要安装一些Ubuntu下必要的环境，以便于接下来的开发任务：
```
$ sudo apt-get update
$ sudo apt-get install ant
$ sudo apt-get install openjdk-7-jdk
$ sudo apt-get install unzip
```
#### 3、解压DOL文件
首先在home目录下新建一个dol的文件夹用于存储：
```
$ mkdir dol
```
然后将实验文档中的dolethz.zip从windows复制到虚拟机中，再解压到dol文件夹中:
```
$ unzip dol_ethz.zip -d dol
```
接下来解压systemc：
```
$ tar -zxvf systemc-2.3.1.tgz
```
#### 4、编译systemc
解压之后，此时有一个systemc-2.3.1的目录，进入：
```
$ cd systemc-2.3.1
```
在其中，创建一个新的临时文件夹objdir：
```
$ mkdir objdir
```
然后进入该文件夹：
```
$ cd objdir
```
接下来运行configure：
```
$ ../configure CXX=g++ --disable-async-updates
```
运行结果如图：<p>
![pic1](https://raw.githubusercontent.com/smie14353227/ES2016_14353227/master/lab2/lab2_pic1.png)<p>
运行完configure之后，就开始编译：
```
$ sudo make install
```
然后执行语句：
```
$ ls
```
编译完成之后会得到如下的文件目录：<p>
![pic2](https://raw.githubusercontent.com/smie14353227/ES2016_14353227/master/lab2/lab2_pic2.png)<p>
然后记录当前的工作路径，以便接下来的文档修改：
```
$ pwd
```
可以得到工作路径为/home/lyx/systemc-2.3.1:<p>
![pic3](https://raw.githubusercontent.com/smie14353227/ES2016_14353227/master/lab2/lab2_pic3.png)<p>
#### 5、编译dol
此时，我们回到根目录，然后进入开始创建的dol文件夹中，找到build_zip.xml这个文件。这里我采取的方式是直接在文件管理器中打开然后通过编辑器修改，将其中的一段话修改为如下格式：
```
<property name="systemc.inc" value="YYY/include"/>
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
```
当中的YYY就是上一部中得到的工作路径。<br>
接下来借助ant工具进行编译：
```
$ ant -f build_zip.xml all
```
编译成功，将会显示build succesful：<p>
![pic4](https://raw.githubusercontent.com/smie14353227/ES2016_14353227/master/lab2/lab2_pic4.png)<p>
那么接下来尝试运行一下第一个例子。首先进入build/bin/mian路径下：
```
$ cd build/bin/main
```
然后运行：
```
$ ant -f runexample.xml -Dnumber=1
```
得到的成功运行结果如下图：<p>
![pic5](https://raw.githubusercontent.com/smie14353227/ES2016_14353227/master/lab2/lab2_pic5.png)<p>
以上，Linux下dol开发环境配置完成。
## 三、感想心得
此次dol环境的配置基于个人计算机上已经安装好的Ubuntu系统，进行相关工具的安装、编译环境的配置，整体按照步骤下来其实并不难。在这个过程中熟悉了在Ubuntu下的命令行操作，比如cd进入相关路径/文件夹，sudo进行软件安装，makedir创建文件夹等。更重要的是对于markdown这种轻量语言的学习，书写下来整篇文档对于这个语言有了大致的认识和运用能力，比如分级标题、代码框、换行缩进格式、插入图片等。总体来说收获很多。
### 参考资料
[1]SDCS of SYSU 2014级移动信息工程嵌入式系统实验课指导文档Lab2 版本控制 & 文档.pdf<br>
[2]http://www.jianshu.com/p/1e402922ee32/ Markdown——入门指南<br>
[3]http://www.appinn.com/markdown/#p Markdown 语法说明 (简体中文版)
