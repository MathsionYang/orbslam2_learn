# ORB-SLAM2特征匹配——Design by 叶培楚（小C）

## 依赖项

    1. opencv 
        主要用来做图像可视化，读取图像，以及提取图像特征点和图像匹配等操作；  

## 编译

    1. 常规编译   
    cd $path/source_code    
    mkdir build    
    cd build     
    cmake ..     
    make -j8    

## 运行

    1. 可以直接用C哥提供的run.bash文件直接跑起来:    
    chmod +x run.bash    
    ./run.bash

    2. 或者自己输入命令行:     
    cd $path/source_code     
    ./bin/keyframe_select  ./dataset/   

## 思路   

    1. 查看不需要插入关键帧的条件,包括:是否纯定位模式,是否全局优化中,是否刚经历重定位;     
    2. 查看新帧的内点数量,一方面跟前一个关键帧的共视部分不能太少,另一部分则是重叠率不能太高;
    3. 最小帧数和最大帧数以及关键帧队列帧数三个要求必须三选其一.


## 代码实现

    1. 读取图像,包括深度和彩色图像;   
    2. 对第一帧彩色图像提取特征点,并计算每个点对应的深度值,设置第一帧的点作为地图点(只是为了方便,没有定义map.cpp);   
    3. 开始逐帧处理,对新帧提取特征点并与前一个关键帧进行特征匹配;    
    4. 匹配点若包含前一个关键帧中的地图点,则表示当前帧含有内点,统计内点数量;     
    5. 根据阈值筛选内点是否满足条件;    
    6. 其他条件主要是最大/最小帧数,以及关键帧队列数目,三个条件满足一个即可.     

## 参考资料

 本模块是C哥为了完善博客而写的,所以本模块对应的博客为[ORBSLAM关键帧的筛选和插入](https://www.cnblogs.com/yepeichu/p/10784265.html).欢迎大家批评指正!           
 C哥邮箱为:peichu.ye@mail2.gdut.edu.cn,欢迎交流!
