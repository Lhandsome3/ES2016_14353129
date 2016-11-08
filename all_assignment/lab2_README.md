# 基于配置DOL的过程


##一.DOL框架描述
Distributed Operation Layer （DOL） : 

A software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.The DOL consists of basically three parts:

- DOL Application Programming Interface
- DOL Functional Simulation
- DOL Mapping Optimization

##二.DOL安装笔记

###1.使用虚拟机安装ubuntu

 因为上学期上操作系统课需要安装ubuntu，用的电脑是Mac OS X，所以当时装的虚拟机是paralells，一些基本的配置已经完毕。 

###2.在ubuntu下安装一些必要的环境
执行如下语句：

    $ sudo apt-get update

    $ sudo apt-get install ant

    $ sudo apt-get install openjdk-7-jdk , 执行结果如下：

![openjdk-7-jdk](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/openjdk-7-jdk.png)

    $ sudo apt-get install unzip , 执行结果如下：

![unzip](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/unzip.png)
 
###3.下载文件
可以使用虚拟机直接下载，也可以从主机拷贝到虚拟机中。因为ta在实验压缩包中已经给出所需要下载的文件，所以只需要将systemc-2.3.1.tgz文件和dol_ethz.zip文件夹拷贝到ubuntu中即可，如下：

![systemc-2.3.1](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/systemc-2.3.1.png)
![dol_ethz](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/dol_ethz.png)

###4.解压文件
新建dol的文件夹,执行语句$ mkdir dol

将dolethz.zip解压到dol文件夹中，执行语句$ unzip dol_ethz.zip -d dol

![dol](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/dol.png)

解压systemc，执行语句$ tar -zxvf systemc-2.3.1.tgz

###5.编译systemc
解压后进入systemc－2.3.1的目录下，执行语句

    $ cd systemc-2.3.1

新建一个临时文件夹objdir，执行语句
     
    $ mkdir objdir

进入该文件夹objdir，执行语句

    $cd objdir

运行configure，执行语句

    $ ../configure CXX=g++ --disable-async-updates

运行configure之后的结果和实验文档中给出的截图一致，因为在是实验中忘记截这个步骤的图了，所以这一步没有贴图说明。

编译

    $ sudo make install
    
编译完后文件目录如下：

![ls](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/ls.png)

可以看到include,lib-linux64（因为我装的是64位的）

记录当前的工作路径（后面会有用处），如下：

![road](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/road.png)

这里表示我当前的工作路径为/home/paralells/systemc-2.3.1


###6.编译dol
进入刚刚dol的文件夹，即执行语句$ cd ../dol，修改build_zip.xml文件，找到下面这段话，就是说上面编译的systemc位置在哪里，

`<property name="systemc.inc" value="YYY/include"/>`

`<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>`

把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）

因为我的是64位系统，所以修改如下：

![64](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/64.png)

然后编译

    $ ant -f build_zip.xml all

若成功会显示build successful

接着试着运行第一个例子：进入build/bin/mian路径下

    $ cd build/bin/main

然后运行第一个例子

    $ ant -f runexample.xml -Dnumber=1

成功结果如图：

![concat](https://raw.githubusercontent.com/Lhandsome3/ES2016_14353129/master/concat.png)

###7.dol配置成功

##三.实验感想
对于实验一：

实验一就是跟着文档的步骤一步步进行配置即可，在配置的过程中没有出现什么问题，一切都是按照文档的步骤正常进行。

对于实验二:

需要先安装git，然后将实验报告放到本地仓库，再在github上建立一个仓库，将这两个仓库关联起来，因为有[Git教程­ 廖雪峰的官方网站的参考](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000),所以也是一步步按照教程上面来。至于MarkDown编辑器，我下的是Mou，因为刚开始接触MarkDown语法，所以不是很熟悉，写报告的时间花得长一点，但是因为MarkDown语法也有教程，所以大大降低了这次实验的难度。我觉得实验报告用Mou写出来很舒服，喜欢上了这个编译器。



