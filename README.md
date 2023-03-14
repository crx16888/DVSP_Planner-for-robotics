# DVSP_Planner-for-robotics
This is a autonomous navigation based on DVSP, applying for drone.
And this is my second college students' innovation project.

Overall:

1 DVSP algorithm：

算法的整个探索过程被分为两个阶段。

第一阶段直接命名为探索(Exploration)，因为这一阶段机器人会一直收集未知的信息，真正符合探索的概念。在这一阶段，会使用RRT(Rapidly-exploring random tree)在机器人周围的局部区域内随机采样观测点，不断地扩展探索区域，并扩大全局的观测点图。大多数算法都包含这一阶段，且大多使用RRT或者RRG(Rapidly exploring random graph)延伸局部的观测点。

第二阶段则命名为重定位(Relocation)，因为这一阶段，机器人周围已经没有未知区域，需要被重新引导至较远处的未知区域继续探索。在这一过程中，机器人始终是在已知区域内行驶，不会收集任何的未知信息。根据这一思想，将算法命名为DSVP(Dual Stage Viewpoint Planner)。下图1是的方法的核心。蓝色点(Vi)为局部观测点，红色点(vi)为全局观测点，橙黄色圆点(FL)为局部的边界点，紫色圆(FG)为全局边界点。

当探索阶段，仍然有局部边界点时，则继续进行探索，生成探索轨迹(橙黄色轨迹线)。反之，当没有局部边界点时，进入重定位阶段，生成重定位轨迹(紫色轨迹线)。

总结：

第一阶段，随机生成树RRT算法 参考https://blog.csdn.net/reasonyuanrobot/article/details/107410097 以此达到机器人探索周围环境的目的（这应该是一种视野上的位置的扩展，为理解为相机或者雷达，那机器人应到达的位置如何确定？还是说这是一种基于传感器的路径观测，然后机器人分析出这个最合适的路径绕沿着树过去），找到离随机点最近的点生成树干，如果连起来会遇到障碍物那么这个路径就不生成。

第二阶段，基于已知环境的机器人重定位 通过周围障碍物等判断机器人在图中的位置，然后我们驱动它到未知区域区继续进行一的探索

故实际上：探索边界用的是rrt，重新规划路线扩展了rrt。探索的时候发现如果周围有局部边界那么就树生长然后继续探索；如果发现没有那么就通过之前已经生成的树回溯去寻找有边界的区域继续探索。

2 
