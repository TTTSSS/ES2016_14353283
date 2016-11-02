#### I.Description

##### DOL框架描述

​	Distributed Operation Layer : The distributed operation layer (DOL) is a 	software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

#### II.How to install

##### DOL安装笔记

1.实验环境是LINUX，首先需要安装虚拟机并配置Ubuntu。(上学期OS课已经配置好了，可参考的一些教程如下)

VMWARE教程：

http://jingyan.baidu.com/article/0320e2c1ef9f6c1b87507bf6.html

VIRTUALBOX教程：

http://jingyan.baidu.com/article/cdddd41c5eea3153ca00e160.html

Ubuntu下载：

http://www.ubuntu.com/download/desktop

2.安装一些必要的环境

```
$	sudo apt-get update

$	sudo apt-get install ant

$ 	sudo apt-get install openjdk-7-jdk

$	sudo apt-get install unzip
```

3.下载文件。可以在虚拟机上直接下，也可以在主机上下好再拖进虚拟机。不过有的虚拟机可能没法在主机和虚拟机之间复制粘贴文件，解决方法有两个：一是直接百度VMtools相关问题按教程解决，二是用U盘在主机和虚拟机之间拷贝。

文件下载：

http://jingyan.baidu.com/article/c33e3f48a5c153ea15cbb5b2.html

```
$  sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
$  sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
```

4.解压文件

```
$  mkdir dol                       //新建dol的文件夹
$  unzipdol_ethz.zip -d dol        //将dolethz.zip解压到 dol文件夹中
$  tar -zxvf systemc-2.3.1.tgz     //解压systemc
```

5.编译systemc

```
$  cdsystemc-2.3.1                //解压后进入systemc-2.3.1的目录下
$  mkdir objdir                   //新建一个临时文件夹objdir
$  cdobjdir                       //进入该文件夹objdir
$  ../configure CXX=g++--disable-async-updates    //运行configure
```

运行configure后的结果：

![1](https://cloud.githubusercontent.com/assets/22443270/19917977/dbe97a20-a102-11e6-9714-bbd9ba359c07.png)

然后继续在命令行窗口执行以下命令：

```
$  sudo make install            //编译
$  pwd                          //输出当前所在路径，需记录当前的工作路径
```

得到当前的工作路径，需要记下来，后面要用：(这里贴出的图有点小错，应该需要去掉后面的/objdir路径，请大家注意~)![微信截图_20160921234110](https：//github.com/TTTSSS/ES2016_14353283/raw/master/微信截图_20160921234110.png)

5.编译dol

```
$  cd../dol                    //进入dol的文件夹
```

修改build_zip.xml文件，找到下面这段话，就是说上面编译的systemc位置在哪里：

```
<property name="systemc.inc" value="YYY/include"/>
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
```

把YYY改成上页pwd的结果，注意对于  64位 系统的机器，lib-linux要改成lib-linux64，修改后执行：

```
$  ant -f build_zip.xml all    //编译
```

若成功会显示build successful，贴一张成功的结果图：![猎豹截图20160922083157](https：//github.com/TTTSSS/ES2016_14353283/raw/master/猎豹截图20160922083157.png)

然后尝试运行第一个例子：

```
$  cd build/bin/main              //进入build/bin/mian路径下
$  ant -frunexample.xml -Dnumber=1    //运行第一个例子
```

运行结如下则说明DOL的开发环境配置已经完成。![微信截图_20160922150821](https：//github.com/TTTSSS/ES2016_14353283/raw/master/微信截图_20160922150821.png)

#### III.Experimental experiment

##### 实验感想和心得

1.一些Tips

(1)注意检查自己的系统到底是64位还是32位，然后再修改build_zip.xml文件中路径，还有路径中不要多加objdir,这直接决定后面build成不成功。本人就在这里坑里很久，以为自己装的是64位就在路径那里多加了64导致配置了好几次都不成功，所以一定要细心。

(2)最后一步build failed,在dol/build/bin/main 下 的 runexample.xml 215-217行需要注释或者删掉，

找到：
 <tstamp>

```
  <format property="touch.time"
          pattern="MM/dd/yyyy hh:mm aa"
          offset="-5" unit="second"/>
</tstamp>
<touch datetime="${touch.time}">
  <fileset dir="example${number}"/>
</touch>
```

修改为：
<!--     <tstamp>

```
  <format property="touch.time"
          pattern="MM/dd/yyyy hh:mm aa"
          offset="-5" unit="second"/>
</tstamp>
<touch datetime="${touch.time}">
  <fileset dir="example${number}"/>
</touch> -->
```

(3)第一次build successful, 但是最后build failed.

将最后一条指令ant -f runexample.xml -Dnumber=1改为sudo ant -f runexample.xml -Dnumber=1

2.感想和心得

(1)由于上学期已经用了VMvare一段时间，所以配置起来其实不太难，只要细心一点，按照实验文档一步步完成就可以了，在这个过程中认识到要学会自己检查问题和去网上搜索一些解决办法。

(2)Markdown初体验，简直像是打开了一扇新大门。在同学推荐下，在众多Markdown平台中选择了typora，另外Markdown上手好像不太复杂，而且整个界面和文本样式看起来都很舒服，治好了多年强迫症。唯一觉得不太舒服的是添加图片比较麻烦，不能直接复制粘贴。接下来应该会尝试一下多种Markdown平台，然后选一个适合的承包自己的实验报告。

