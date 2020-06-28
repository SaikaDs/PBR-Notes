# PBR-Notes
## 本篇是[LearnOpenGL-PBR-理论](https://learnopengl-cn.github.io/07%20PBR/01%20Theory/)的笔记<br>
PBR涉及的公式和知识点太多，在这里做一个总结方便记忆<br>
PBR理论的核心就是一个反射率方程。首先把反射率方程摆在开头，然后对其中元素逐个解读<br>
`反射率方程(The Reflectance Equation)`
## Lo(p,ωo) = ∫Ω Fr(p,ωi,ωo) Li(p,ωi) n⋅ωi dωi<br>
#### `p` 该点(被着色的点)<br>
#### `Lo` 该点在观察方向的辐射率<br>
#### `Li` wi方向上入射光的辐射率<br>
#### `wo` 出射立体角，可视作观察方向向量<br>
#### `wi` 入射立体角，可视作入射方向向量<br>
#### `Ω` 以点p为球心的半球领域(入射方向wi在该领域内做积分)<br>
#### `n` 法线，n⋅ωi(点乘)表示入射光和法线的夹角的余弦，乘上Li以计算入射能量<br>
#### `Fr` 双向反射分布函数(BRDF)，以下为通常用的Cook-Torrance BRDF模型，它分为漫反射部分和镜面反射部分<br>
#### Fr = kd Flambert + ks Fcook-torrance<br>
* `kd` `ks` 分别为入射光线中被折射(对应漫反射)和被反射(对应镜面反射)的比例，其中ks就是菲涅尔方程的计算结果<br>
* `Flambert` 漫反射部分，Flambert = c/π，其中`c`为表面颜色<br>
* `Fcook-torrance` 镜面反射部分，Fcook-torrance = D F G / 4(ωo⋅n)(ωi⋅n)<br>
  * `D` 法线分布函数(Normal Distribution Function):<br>
估算在受到表面粗糙度的影响下，取向方向与中间向量一致的微平面的数量。这是用来估算微平面的主要函数。它宏观上与粗糙度和观察方向有关<br>
例(Trowbridge-Reitz GGX法线分布函数): NDFggxtr(n,h,α) = α^2 / π((n·h)^2(α^2-1)+1)^2<br>
其输入为宏观法线向量n，中间向量h，粗糙度α，它返回一个与h取向一致的微平面的比例(一致的微平面越多则越亮)，取值在0-1之间<br>
  * `F` 菲涅尔方程(Fresnel Equation):<br>
描述了在不同的表面角下表面所反射的光线所占的比率，仅与观察方向有关，当观察角度越倾斜，这个比率越高，即反射光相比折射光越多<br>
例(Fresnel-Schlick近似法): Fschlick(n,v,Fo) = Fo + (1-Fo)(1-(n·v))^5<br>
其输入为法线向量n，观察方向向量v，基础反射率Fo，即垂直观察时反射光线所占的比率(保底比率)，它是由折射指数计算出的，它是一个三维向量，对于RGB每个通道都有它们的反射率。在计算Fo的过程中还可以引入金属度来优化：由于非金属和金属的基础反射率相差较大，非金属一般为0.04(三通道相同)，而金属为0.5-1.0且不一定三通道相同，即有颜色。因此一种表面，无论是否是金属，都可以用0.04和其表面颜色基于金属度做插值来获得其Fo。表现为F0=mix(0.04,surfaceColor.rgb,metalness);<br>
n·v为法向量点乘观察向量，即cosθ<br>
  * `G` 几何函数(Geometry Function)：<br>
从统计学上近似求得了微平面间相互遮蔽的比率，它与粗糙度、观察方向和光照方向有关<br>
例(Schlick-GGX函数): Gschlickggx(n,h,k) = n·h / (n·h)(1-k)+k<br>
其输入为法线向量n，观察方向(或光照方向)向量h，经选择的粗糙度k。<br>
k本质上就是粗糙度α，但稍有不同，当该几何函数是针对直接光照时，k=(α+1)^2/8；而针对IBL光照时，k=α^2^/2<br>
注意，在光线射入和摄像机观察时，我们都应该考虑微平面间相互遮蔽的影响。因此我们需要针对光照方向和观察方向分别应用一次Schlick-GGX函数(因此上述参数中用h来指代方向)，并利用史密斯法把二者结合起来:
史密斯法: Gfinal(n,v,l,k)=Gschlickggx(n,v,k)Gschlickggx(n,l,k)<br>
其中v是观察方向，l是光照方向<br>
## 至此，反射率方程的所有元素介绍完毕，把它完全展开就是下面的样子：
![](https://github.com/SaikaDs/PBR-Notes/blob/master/pic.jpg)

