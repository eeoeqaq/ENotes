视口变换
![[Pasted image 20260825120315.png]]

##### antialias
blur -> sample

空间频率的滤波：高通滤波？低通滤波？
filtering = avaraging = convolution

空间域的卷积 = 空间频率域的乘积
频率滤波 -> 原图卷积

##### 什么是alias？
![[Pasted image 20260828001213.png]]
空间域的乘积 <-> 频率域的卷积
取中央的频率峰即可恢复原图像
但在取样稀疏（fs偏小）情况下，相邻频率峰重叠（走样alias）
解决方法：
- 更密集的取样
- __更窄的频率峰（低通滤波）__
亦即 blurring -> sampling
blurring-> supersampling
一些抗锯齿：MSAA(multisampling AA) FXAA(fast approximate AA) TAA(temporal AA)
![[Pasted image 20260828011753.png]]
