#### BDPT
双向路径追踪

#### MLT metropolis light transport
[简要介绍](https://zhuanlan.zhihu.com/p/497375112)

#### photon mapping
pros：good at 
一种简单做法：
- photon tracing从光源射出线，直至到达漫反射表面
- photon collection从摄像机射出线，直至到达漫反射表面，估计单位面积上光子数量

> [!NOTE] 光子数量估计方法
> 注意此处使用单位面积内光子数量和某一光子数量所占面积的区别
> 单位面积内光子数量：有偏估计
> 某一光子数量所占面积：随着光子数量趋近无限大，面积趋近无限小，此时是无偏估计（consistent）

#### VCM vertex connection and merging


#### IR instant radiosity

#### non-surface model
- 云雾：光的漫反射
- 头发：内含色素的可反射可折射的圆柱体：BCSDF
- 颗粒材质：

#### surface model
透光材质：玉    ->BSSRDF次表面散射
cloth：单根纤维渲染？作为材质表面渲染？作为散射介质渲染？trade-off
表面细节：瑕疵等真实感
程序化生成表面：例如用一个三维噪声函数生成木质纹理