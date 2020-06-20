# PBR-Notes
###PBR涉及的公式和知识点太多，在这里做一个总结方便记忆<br>
-
本篇是https://learnopengl-cn.github.io/07%20PBR/01%20Theory/的读书笔记<br>
PBR理论的核心就是一个反射率方程。首先把反射率方程摆在开头，然后对其中元素逐个解读<br>
    反射率方程(The Reflectance Equation)
    Lo(p,ωo)=∫Ωfr(p,ωi,ωo)Li(p,ωi)n⋅ωidωi
