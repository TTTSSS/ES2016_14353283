一、改完的*.dot图

修改前的example1.dot：

![example1修改前的dot](https://cloud.githubusercontent.com/assets/22443270/19918269/c3faa748-a104-11e6-8788-e26a371454f7.png)

修改后的example1.dot：

 ![example1修改后的dot](https://cloud.githubusercontent.com/assets/22443270/19918292/ed41a0c0-a104-11e6-85c5-6c1289dfe3f7.png)

 修改example1，使其输出3次方数，tips:修改square.c：

 ![example1修改后的数据](https://cloud.githubusercontent.com/assets/22443270/19918316/12f9f95c-a105-11e6-8d90-506bddab7c5d.png)

修改前的example2.dot：

 ![example2修改前的dot](https://cloud.githubusercontent.com/assets/22443270/19918356/5f9cebe8-a105-11e6-8196-6ba41016b35a.png)
 
修改后的example2.dot：

 ![example2修改后的dot](https://cloud.githubusercontent.com/assets/22443270/19918371/9416a6d4-a105-11e6-8ca6-57c6541701a6.png)

 修改example2，让3个square模块变成2个, tips:修改xml的iterator ：

![example2修改后的数据](https://cloud.githubusercontent.com/assets/22443270/19918430/161d41b0-a106-11e6-9c90-737e8c91b2c6.png)

二、修改过程

1.example1，修改"i=i*i"为"i=i*i*i"，就可以得到3次方数

 ![squre.c图片](https://cloud.githubusercontent.com/assets/22443270/20047860/2160105c-a4f3-11e6-81ac-46b7508634c4.png)

2.example2，修改迭代次数，也就是下面的value为2，就可以让3个square模块变成2个：

 ![iterator图片](https://github.com/TTTSSS/ES2016_14353283/master/iterator图片.png)

3.注意生成的example文件在dol/build/bin/main/example下，是加锁的。当我们要生成新的dot图，需要先删掉之前的example文件，然后重新编译dol，运行example，运行指令在第一次实验配置中就已经接触过，为sudo ant –f runexample.xml –Dnumber=XXX。那么我们必须先解锁才能删除，解锁方法如下：

![解锁锁定文件](https://cloud.githubusercontent.com/assets/22443270/19918446/485ac012-a106-11e6-9a7c-e72c18f27587.png)
4.另外是一个小提示：生成的example1文件在dol/build/bin/main/example1，而修改example是在dol/examples/example1/src里，这点切勿搞混了。

三、实验感想

这次实验比较简单，修改的部分很少，但要求我们必须学会看懂代码，比如： /src 文件夹内包含2种文件：*.c, 与对应的.h，就是实现的模块，就是*.dot的 框框的功能描述。（每个模块要实现2个接口，xxx_init和xxx_fire两个函数， 分别是初始化这个模块是干了什么，以及这个模块开干的时候做什么） 

然后就是要学会观察修改前后输出结果和dot图的差别，体会代码对这些的影响，比如在example2中当我们修改了square的个数，很明显得，dot图里的square模块由2变成了3.
