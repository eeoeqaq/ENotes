#### whitted style
![[Pasted image 20260911103100.png]]
需要大量计算光线和表面的求交
- 隐式表面
- 三角形
为了加速：AABB（axis aligned binding boxes）
##### accularate
使用kd树：对空间的划分
计算大量三角形和矩形的求交问题，太慢，，

使用BVH：对物体的分组

##### radiometry
![[Pasted image 20260913143728.png]]

###### radiant intensity
每一单位立体角中的光强 -> 坎德拉

###### irradiance
- power per unit area
- will falloff

###### radiance
- power per solid angle per u.a. (radiant intensity per u.a.)(irradiance per solid angle)

##### BRDF
一个描述一束光从某个方向射到表面后，有多少比例会沿另一个方向反射出去的方程
-> ___rendering equation___

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
