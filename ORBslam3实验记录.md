运行kitti双目数据集

```
./Examples/Stereo/stereo_kitti Vocabulary/ORBvoc.txt Examples/Stereo/KITTI00-02.yaml /home/juo/data_odometry_gray/dataset/sequences/00

```

先开两个终端分别跑左右影像的名称分别是`/cam0/image_raw`、`/cam1/image_raw`，所以我们需要一个“转发器”，将数据流转发一下。利用ROS中的`topic_tools`就可以实现。我们分别打开两个终端

```
rosrun topic_tools throttle messages /cam0/image_raw 20.0 /camera/left/image_raw
rosrun topic_tools throttle messages /cam1/image_raw 20.0 /camera/right/image_raw
```

播放bag

```
rosbag play MH_03_medium.bag
```

必须要用老的setting才能跑不知道为什么

```
rosrun ORB_SLAM3  Stereo Vocabulary/ORBvoc.txt /home/juo/ORB_SLAM3_detailed_comments/Examples_old/Stereo/EuRoC.yaml true
```

