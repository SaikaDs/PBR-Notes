# PBR-Notes
## PBR涉及的公式和知识点太多，在这里做一个总结方便记忆<br>
本篇是[LearnOpenGL-PBR-理论](https://learnopengl-cn.github.io/07%20PBR/01%20Theory/)的读书笔记<br>
PBR理论的核心就是一个反射率方程。首先把反射率方程摆在开头，然后对其中元素逐个解读<br>
`反射率方程(The Reflectance Equation)`<br>
        Lo(p,ωo) = ∫Ω Fr(p,ωi,ωo) Li(p,ωi) n⋅ωi dωi
### 字母解读<br>
`p`该点(被着色的点)<br>
`Lo`该点在观察方向的辐射率<br>
`Li`wi方向上入射光的辐射率<br>
`wo`出射立体角，可视作观察方向向量<br>
`wi`入射立体角，可视作入射方向向量<br>
`Ω`以点p为球心的半球领域(入射方向wi在该领域内做积分)<br>
`n`法线，n⋅ωi(点乘)表示入射光和法线的夹角的余弦，乘上Li以计算入射能量<br>
`Fr`双向反射分布函数(BRDF)
>Fr=DFG/4(ωo⋅n)(ωi⋅n)
>`D`法线分布函数(Normal Distribution Function)
>


...<br>
### 内容解读<br>
#### fr(p,ωi,ωo)<br>
