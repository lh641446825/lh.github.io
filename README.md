# 物体6自由度位姿估计综述（持续更新中）
&#160; &#160; &#160; &#160;物体位姿估计在机器人领域（如机械臂抓取），AR/VR领域，无人驾驶领域有着广泛的应用，在物体跟踪，建模等相关领域也有着重要的影响。

![](https://github.com/lh641446825/picture/blob/master/2.jpg?raw=true) 
</div>
<center>图1  机器人抓取</center>

![](https://github.com/lh641446825/picture/blob/master/3.jpg?raw=true)
<center>图2 VR领域</center>

## 一、 识别，检测与位姿估计的区别

&#160; &#160; &#160; &#160;识别是判断图像中是否包含某物体的任务，它是二元分类问题。检测是在图像内定位物体的位置，包括物体比例的估计或完整的2D边界框估计。位姿估计是推断出物体在3D世界中的位置，涉及估计3D物体平移和3D物体旋转。
![](https://github.com/lh641446825/picture/blob/master/4.jpg?raw=true)
<center>图3 识别、检测与位姿估计</center>

## 二、位姿估计的分类

### 1. 常规的位姿估计

&#160; &#160; &#160; &#160;给定RGB-D图像的情况下，估计刚性物体的3D平移和3D旋转。训练数据包含物体在不同视点下的图像，如图3所示，每个图像均注释了groundtruth位姿。结果为包含旋转和平移的绿色边界框。
&#160; &#160; &#160; &#160;深度通道极大地简化了位姿估计问题。它包含有关物体形状的线索，物体边界的标志是深度不连续，深度测量与光照条件无关。许多RGB-D方法包括最终细化，其将物体的3D模型与估计位置处的局部深度对准，例如，通过迭代最近点（ICP）。因此，允许初始位姿估计稍微粗略，因为它只是细化的开始。

![](https://github.com/lh641446825/picture/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20190901205045.png?raw=true)
<center>图4 常规的物体位姿估计</center>

### 2.从单个RGB图像估计6自由度位姿
&#160; &#160; &#160; &#160;将RGB-D输入改为RGB输入。但是RGB输入不太可靠，因为它们直接受到光照变化的影响，并且物体边界不太突出，取决于背景。此外，物体与相机的距离很难准确估计，因为投影尺寸随着距离的变化只有微小变化。细化不能利用局部场景几何，例如ICP。因此，准确的位姿估计更难以实现。但是RGB-D相机，例如Kinect在户外不能很好地工作。

### 3.多个物体的位姿估计

&#160; &#160; &#160; &#160;同时训练多个物体。给定RGB或RGB-D图像，系统估计图像中存在的所有物体的位姿。然而并非所有系统已知的物体都出现在输入图像中。因此，除了位姿估计之外，系统必须预测物体在图像中是否可见的概率。如图4所示，评估标准：准确性，合理的时间内处理许多物体的能力。

![](https://github.com/lh641446825/picture/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20190901205329.png?raw=true)
<center>图5 多个物体的位姿估计</center>

### 4.相机的定位

&#160; &#160; &#160; &#160;环境或场景本身可以被认为是刚性物体并且可以估计其位姿。估计相机的位姿，与场景位姿相反。给出已知环境的RGB或RGB-D图像，估计拍摄图像相机的6自由度位姿。如图5所示。从概念上来看，这个问题比物体位姿估计更容易，因为物体不需要被定位。而实践中，相机定位非常具有挑战性，因为场景通常不是完全静态的，包含大的，平面的，无纹理的区域和像窗户一样的重复结构。此外，在某些应用中，场景可以达到很大的范围，例如基于城市尺度的图像定位。

![](https://github.com/lh641446825/picture/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20190901205505.png?raw=true)
<center>图6 相机的位姿估计</center>
