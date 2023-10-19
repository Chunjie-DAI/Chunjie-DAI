+++
title = 'Tips of Matlab Simulink 2'
date = 2020-12-23T23:45:31+03:00
draft = false
+++


>最近做仿真遇到了要使用Zero-Order Hold 和Memory模块的情况，但是不是特别懂他们之间的区别，谷歌了 一下发现他们俩和有个类似的兄弟，Unit Delay模块，于是索性写个写个文档总结一下。
<!--more-->


问题描述：
如何区分Zero-Order Hold，Memory和Unit Delay模块并正确使用。

解答：
首先我们来看下这三个模块长什么样，如图一所示，自上而下分别是Zero-Order Hold，Unit Delay和Memory模块，输入为一正弦波信号，周期为2s。
![1](/1629990321544.png)<center>Fig.1 Model comparison</center>

Zero-Order Hold：如字面意思，零阶保持器，可以理解为降频采样器，他会在每到sample time的时候对输入进行采样并输出出去，这个值将保持到下一个sample time到来，这就达到了一个降频采样的效果，该模型sampletime设为0.1s，输出如下：
![2](/1629990330324.png)<center>Fig.2 ZOH wave</center>

Unit Delay: 单位延时，将输入信号延时一个sample time，每个sample time的值其实都是上个采样周期的输入信号，因此需要指定initial value，这里设置为0初始值，sample time同样为0.1s，输出如下，可看出整体波形比图一延迟了0.1秒。
![3](/1629990365303.png)<center>Fig.3 UD wave</center>

Memory：记忆？这个模块其实和Unit Delay很类似，都是实现延迟离散化效果，而Memory的不同是它的sample time是和Simulink solver的运算步长有关系的，根据帮助文档的说明，该模型将把信号延迟一个主积分时间步，据测试发现，信号将被延迟一个Max Step Size。这里将Max Step Size设置为0.001s，波形如下，放大后可看到1秒时确实延时了0.001s，而另外两个模块的输出不变。
![4](/1629990376046.png)<center>Fig. 4 Memory wave</center>

![5](/1629990383656.png)<center>Fig. 5 Partial memory wave</center>

🐟🐟🐟