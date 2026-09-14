#### Blinn-Phong reflection model
$$L = k_a I_a
+ k_d \left(\frac{I}{r^2}\right)\max(0,\mathbf{n}\cdot\mathbf{l})
+ k_s \left(\frac{I}{r^2}\right)\max(0,\mathbf{n}\cdot\mathbf{h})^p$$
- diffuse漫反射
	- 多少光被材料吸收
	- 多少光到达
	- 单位面积上反射多少光
$$L_d = k_d \left(\frac{I}{r^2}\right) \max(0,\mathbf{n}\cdot\mathbf{l})$$
- 镜面反射
	- 半程向量h
	- 和光照角度和观测角度都有关
	- p:规范高光大小
$$L_s = k_s \left(\frac{I}{r^2}\right)\max(0,\mathbf{n}\cdot\mathbf{h})^p$$
- 环境光
	- 和光照角度和观测角度都无关

![[Pasted image 20260906194807.png]]