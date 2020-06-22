# PBR-Notes
## PBR涉及的公式和知识点太多，在这里做一个总结方便记忆<br>
本篇是[LearnOpenGL-PBR-理论](https://learnopengl-cn.github.io/07%20PBR/01%20Theory/)的读书笔记<br>
PBR理论的核心就是一个反射率方程。首先把反射率方程摆在开头，然后对其中元素逐个解读<br>
`反射率方程(The Reflectance Equation)`<br>
## Lo(p,ωo) = ∫Ω Fr(p,ωi,ωo) Li(p,ωi) n⋅ωi dωi<br>
### 字母解读<br>
#### `p` 该点(被着色的点)<br>
#### `Lo` 该点在观察方向的辐射率<br>
#### `Li` wi方向上入射光的辐射率<br>
#### `wo` 出射立体角，可视作观察方向向量<br>
#### `wi` 入射立体角，可视作入射方向向量<br>
#### `Ω` 以点p为球心的半球领域(入射方向wi在该领域内做积分)<br>
#### `n` 法线，n⋅ωi(点乘)表示入射光和法线的夹角的余弦，乘上Li以计算入射能量<br>
#### `Fr` 双向反射分布函数(BRDF)，以下为通常用的Cook-Torrance BRDF模型，它分为漫反射部分和镜面反射部分<br>
#### Fr = kd Flambert + ks Fcook-torrance<br>
##### >`kd` `ks` 分别为入射光线中被折射(对应漫反射)和被反射(对应镜面反射)的比例<br>
##### >`Flambert` 漫反射部分，Flambert = c/π，其中`c`为表面颜色<br>
##### >`Fcook-torrance` 镜面反射部分，Fcook-torrance = D F G / 4(ωo⋅n)(ωi⋅n)<br>
###### >>`D`法线分布函数(Normal Distribution Function):<br>
>>>估算在受到表面粗糙度的影响下，取向方向与中间向量一致的微平面的数量。这是用来估算微平面的主要函数。<br>
>>>例:Trowbridge-Reitz GGX法线分布函数 NDFggxtr(n,h,α) = α^2 / π((n·h)^2(α^2-1)+1)^2<br>
>>>其输入为法线向量n，目标向量h，粗糙度α，它返回一个与h取向一致的微平面的比例(一致的微平面越多则越亮)，取值在0-1之间<br>
###### >>`F`菲涅尔方程(Fresnel Equation):<br>
>>描述了在不同的表面角下表面所反射的光线所占的比率，当观察角度越倾斜，这个比率越高，即反射光相比折射光越多<br>
>>
##### >


...<br>
### 内容解读<br>
#### fr(p,ωi,ωo)<br>
