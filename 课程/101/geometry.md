隐式几何：方程表示的几何体
显式几何：点集表示的几何体
SGF --- ray marching

###### 贝塞尔曲线
一种类似插值的方法产生的曲线，由多个点（一般4个）产生的点集构成

其他曲线：spline B-spline and so on

##### 三角形操作
细分
- loop division: 全三角形，取中点+所有点卷积
- catmull-clark division 任意多边形可用，边中点和图形中心+所有点卷积
合并
- 计算所有边删去的二次标准差依次删去

shadow mapping
- 经典的阴影生成
- 测试看到的每个点能否被光源看到
- 类似z-buffering

