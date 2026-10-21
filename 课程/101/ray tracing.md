#### BRDF 和 rendering equation
BRDF：一个描述一束光从某个方向射到表面后，有多少比例会沿另一个方向反射出去的方程
-> __rendering equation__

![[Pasted image 20260914134240.png]]![[Pasted image 20260914134251.png]]![[Pasted image 20260914134303.png]]
###### 渲染方程与级数展开

**① 渲染方程每一项的来源**

出发点：BRDF 的定义 —— 出射 radiance 与入射 irradiance 之比

$$f(x,\omega_i,\omega_r)=\frac{dL_r(x,\omega_r)}{dE_i(x,\omega_i)}=\frac{dL_r(x,\omega_r)}{L_i(x,\omega_i)\cos\theta_i\,d\omega_i}$$

分母是 irradiance（单位面积能量），所以 $\cos\theta_i$ 来自定义本身：斜射的光在表面上被“摊薄”（foreshortening），单位面积分到的能量要乘 $\cos\theta_i$。

反解出 $dL_r=f\,L_i\cos\theta_i\,d\omega_i$，对所有入射方向（上半球 $\Omega$）积分，再加自发光，得渲染方程：

$$L_r(x,\omega_r)=L_e(x,\omega_r)+\int_\Omega L_r(x',-\omega_i)\,f(x,\omega_i,\omega_r)\cos\theta_i\,d\omega_i$$

- $L_i(x,\omega_i)=L_r(x',-\omega_i)$：照到 $x$ 的光 = 沿 $\omega_i$ 反向追到的第一个点 $x'$ 朝 $x$ 射出的光（从 $x'$ 看方向为 $-\omega_i$）
- **未知量 $L_r$ 出现在自己里面**：算 $x$ 多亮要先知道所有 $x'$，而 $x'$ 又依赖 $x$ —— 从“一个积分”升级为“积分方程”，这是全局光照必须递归求解的原因

**② 抽象成标准形式（Fredholm 第二类）**

把「点 + 方向」打包成 $u=(x,\omega_r)$：

$$I(u)=e(u)+\int I(v)\,K(u,v)\,dv$$

- $I(u)$：未知光场（即 $L_r$）；$e(u)$：发射项 $L_e$
- $K(u,v)=f\cos\theta_i$：核函数 = Light Transport Operator
- 第二类：未知量同时出现在积分**外**和积分**内**（只出现在积分内的是第一类）

**③ 算子化简**

$$\mathcal{L}=\mathcal{E}+\mathcal{K}\mathcal{L}\ \Rightarrow\ (I-\mathcal{K})\mathcal{L}=\mathcal{E}\ \Rightarrow\ \mathcal{L}=(I-\mathcal{K})^{-1}\mathcal{E}$$

（$I$ 是单位算子；$\mathcal{K}$ 是核 $K$ 作为算子作用在整个光场上的写法）这只是形式解 —— 算子求逆不能直接计算，目的是改写成可级数展开的形式。

**④ Neumann 级数展开**

类比 $\dfrac{1}{1-x}=1+x+x^2+\cdots\ (|x|<1)$：

$$(I-\mathcal{K})^{-1}=I+\mathcal{K}+\mathcal{K}^2+\mathcal{K}^3+\cdots$$

$$\mathcal{L}=\mathcal{E}+\mathcal{K}\mathcal{E}+\mathcal{K}^2\mathcal{E}+\mathcal{K}^3\mathcal{E}+\cdots$$

把 $\mathcal{K}$ 读作「再弹射一次」：

| 项 | 弹射次数 | 含义 |
| --- | --- | --- |
| $\mathcal{E}$ | 0 | 眼睛直接看到光源 |
| $\mathcal{K}\mathcal{E}$ | 1 | 直接光照 |
| $\mathcal{K}^2\mathcal{E}+\mathcal{K}^3\mathcal{E}+\cdots$ | $\geq 2$ | 间接光照 |

> 勘误：幻灯片写的 “Binomial Theorem” 严格说是**几何级数 / Neumann 级数**；二项式定理是 $(1+x)^n=\sum_k\binom{n}{k}x^k$。

**⑤ 为什么能展开：收敛条件 = 能量守恒**

$\|\mathcal{K}\|<1$ ⇔ 每次弹射都有损耗（吸收 / 飞出场景）→ $\mathcal{K}^n\mathcal{E}\to 0$：弹射无穷多次的光，能量早已衰减为零。对应 BRDF 的三条约束：$f\geq 0$；$f(\omega_i,\omega_r)=f(\omega_r,\omega_i)$（可逆性）；$\int_\Omega f\cos\theta\,d\omega\leq 1$。

**⑥ 与实现对上号**

- **Path tracing**：逐项估计这个级数 —— camera ray 采样一次积分 = 应用一次 $\mathcal{K}$，递归 + Russian roulette 做无偏截断
- **Radiosity**：场景离散成 patch 后算子变成矩阵，$l=e+Kl$ 用线性代数解
- **Whitted ray tracing**：把无穷级数截断到前几项（直接光 + 几次镜面反射/折射），是全局光照的近似

直接光照+间接光照 -> 全局光照




###### what's more
现实中按照rendering equation对全局光照直接模拟会让复杂度指数级上涨
需要一个能控制复杂度的方法：path tracing

#### rendering equation的实现
##### whitted style ray tracing
![[Pasted image 20260911103100.png]]
需要大量计算光线和表面的求交
- 隐式表面
- 三角形
为了加速：AABB（axis aligned binding boxes）
###### accularate
使用kd树：对空间的划分
计算大量三角形和矩形的求交问题，太慢，，

使用BVH：对物体的分组


##### path tracing 
###### 前置知识
- 为什么要有PT？
	- whitted style 不能解决glossy物体反射
	- 漫反射表面物体的反射？color blend？
	- 真实模拟rendering equation的开销过大
	- 在每一个像素内射出数条光线，在漫反射时 __随机__  取一条光路  
- radiometry
	![[Pasted image 20260913143728.png]]

	- radiant intensity 辐射强度
		每一单位立体角中的光强 -> 坎德拉

	- irradiance 辐照度
		- power per unit area
		- will falloff

	- radiance 辐亮度
		- power per solid angle per u.a. (radiant intensity per u.a.)(irradiance per solid angle)
- 蒙特卡洛积分
	$\int f(x)\,dx \approx \frac{1}{N}\sum_{i=1}^{N}\frac{f(X_i)}{p(X_i)}, \qquad X_i\sim p(x)$

	注意到此处有一个p(X)对取样偏好进行了抵消


###### 模拟方式
在每一个像素内射出数条光线，在漫反射时 __随机__  取一条光路 
光路用概率的01抉择决定是否继续延续，权重除以该概率以获得正确期望
问题：小光源影响大却难以被采样到，引入对光源的直接采样
(该问题可以泛化为：某些影响大的方向不易被采样到，这些方向不一定是光源，也可能是光源的二次反射，此时就需要更完备的方法如BDPT)
- 对光源的直接采样（NEE）
	问题：BRDF 采样是“瞎撞”，小光源命中概率 $\varepsilon$ 极小 → fireflies（大量 0 与偶发大值），需要 $N\sim 1/\varepsilon$ 才能收敛。直接光（$\mathcal{K}\mathcal{E}$）应**瞄准光源采样**。
	
	换元：把积分域从半球立体角搬到光源面积 $A$，$d\omega_i=\dfrac{\cos\theta'\,dA}{\|x-x'\|^2}$：
	
	$$L_{\text{direct}}=\int_A L_e\,f\,\frac{\cos\theta_i\cos\theta'}{\|x-x'\|^2}V\,dA
	\qquad
	\langle L\rangle=\frac{L_e\,f\,\cos\theta_i \cos\theta'\,V}{p_A\,\|x-x'\|^2}$$
	
	- 均匀采样面光源 $p_A=1/A$ → $\langle L\rangle \approx L_e\,f\,\cos\theta_i\,\Omega_L$：单样本即低方差
	- $\cos\theta_i$ 来自 BRDF 定义；$1/r^2$ 来自 radiance 衰减；$V$ 就是阴影光线
	- 采样 pdf 在**面积测度**下给，故权重除以 $p_A$ 而非立体角 pdf
	- 点光源/方向光是 delta 分布（$A=0$），不能撒点，直接求值
	
	限制：近镜面 glossy 时 BRDF 是窄尖峰，光源采样会打到峰外 → 与 BRDF 采样互补，用 __MIS__ 加权合并（同一方向两个 pdf 需换算到同一测度再相加）。
	
	实现要点：
	- 每个 bounce 做一次 NEE（= 级数每一项都以 $\mathcal{E}$ 收尾）
	- 若不用 MIS：BSDF 采样命中光源时不再计 $L_e$（避免重复计），只相机光线/镜面弹射命中才计
```
shade(p, wo)
    # Contribution from the light source.
    Uniformly sample the light at x' (pdf_light = 1 / A)
    Shoot a ray from p to x'
    if not blocked:
	    L_dir = L_i * f_r * cos θ * cos θ' / |x' - p|^2 / pdf_light

    # Contribution from other reflectors.
    L_indir = 0.0
    Test Russian Roulette with probability P_RR
    Uniformly sample the hemisphere toward wi (pdf_hemi = 1 / 2pi)
    Trace a ray r(p, wi)
    If ray r hit a non-emitting object at q
        L_indir = shade(q, -wi) * f_r * cos θ / pdf_hemi / P_RR

    Return L_dir + L_indir
```

###### further more
![[Pasted image 20260916142609.png]]![[Pasted image 20260916142547.png]]
1