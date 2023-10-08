+++
title = 'Tips of Matlab Simulink 1'
date = 2020-12-09T22:45:31+03:00
draft = false
+++



问题描述：
在使用MATLAB/Simulink时，将不同库的模块相连接，发现常常连不上。

<!-- more -->


原因：
MATLAB/Simulink 中的连接线有很多种，有电气线和信号线，其中信号线又分为Physical Signal 和 Simulink Signal。
电气线可以理解为电气回路中的连接线，没有方向，其中包含电压和电流信号，模块端口为方形，连出的电气线头为圆形，如下图所示
![1](/1629989193944.png)

而常见的信号线为Simulink中的数据流，为单向传输，模块端口和信号线头均为箭头，箭头方向表示信号传输方向，如上图中的g和m端口。

信号线和电气线不能直接相连，不同库的电气线也不能直接相连。
而信号线中又有一种比较特殊的称为物理信号线，如下图所示，这种连接线的端口为三角箭头，物理信号线和simulink信号线同样不能直接相连。
![2](/1629989223790.png)

解决办法：
1️⃣电气线与信号线相连：使用Voltage Measurement 或 Current Measurement，如下图
![3](/1629989241996.png)

2️⃣物理信号线与simulink信号线相连：使用PS-Simulink Converter 或 Simulink-PS Converter，如下图
![4](/1629989250702.png)


🐟🐟🐟