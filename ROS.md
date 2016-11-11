

## Ubuntu14.04安装和配置ROS&Cartographer

#### 一、ROS：

1.The Basics

```
/etc/apt/sources.list
/etc/apt/sources.list.d/
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
```

2.Adding Respositories：

```
deb http://us.archive.ubuntu.com/ubuntu/ saucy universe
deb-src http://us.archive.ubuntu.com/ubuntu/ saucy universe
deb http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe
deb-src http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe
sudo add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ saucy universe multiverse"
sudo add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe multiverse
sudo apt-get update
deb http://archive.canonical.com/ubuntu saucy partner
deb-src http://archive.canonical.com/ubuntu saucy partner
sudo apt-get update
```

结果：

 ![lab5](F:\大三\嵌入式实验\lab5.png)

 ![lab5.3](F:\大三\嵌入式实验\lab5.3.png)

#### 二、Cartographer：

1.安装所有依赖项

```
sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev
```

 ![微信截图_20161111101412](微信截图_20161111101412.png)

 ![微信截图_20161111101516](微信截图_20161111101516.png)

2.首先安装ceres solver，选择的版本是1.11,路径随意，注意第二步，要先手动新建一个build文件夹

```
1.     git clone https://github.com/hitcm/ceres-solver-1.11.0.git

2.      cd ceres-solver-1.11.0/build

3.      cmake ..

4.      make –j

5.      sudo make install
```

 ![微信截图_20161111100219](微信截图_20161111100219.png)

 ![微信截图_20161111101841](微信截图_20161111101841.png)

 ![微信截图_20161111102735](微信截图_20161111102735.png)

3.然后安装cartographer，注意要先从前面的路径返回到Home

```
1.      git clone https://github.com/hitcm/cartographer.git

2 .     cd cartographer/build

3.       cmake .. -G Ninja

4.       ninja

5.       ninja test

6.       sudo ninja install
```

 ![微信截图_20161111103045](微信截图_20161111103045.png)

 ![微信截图_20161111103643](微信截图_20161111103643.png)

 ![微信截图_20161111105018](微信截图_20161111105018.png)

  ![微信截图_20161111105154](微信截图_20161111105154.png)

4.安装cartographer_ros

下载到catkin_ws下面的src文件夹下面：

```
git clone https://github.com/hitcm/cartographer_ros.git
```

 ![微信截图_20161111105443](微信截图_20161111105443.png)

然后到catkin_ws下面运行catkin_make即可。

5.数据下载测试

2d数据，大概500M，用迅雷下载

```
https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag

```

3d数据，8G左右，同样用迅雷下载

```
https://storage.googleapis.com/cartographer-public-data/bags/backpack_3d/cartographer_3d_deutsches_museum.bag
 
```

```
然后运行launch文件即可。
roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
roslaunch cartographer_ros demo_backpack_3d.launch bag_filename:=${HOME}/Downloads/cartographer_3d_deutsches_museum.bag
```