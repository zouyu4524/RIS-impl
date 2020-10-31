# 天线理论与技术课程设计

<div style="margin: 0 auto; font-size: 20px; font-weight: bold;" align="center">邹雨泽</br>D201677498</div>

## 基于超表面的波束可重构天线技术研究

可复现源码: [zouyu4524/RIS_impl](https://github.com/zouyu4524/RIS-impl)

## 课题背景

可重构天线旨在通过改变天线的物理特性参数，使天线的某些辐射特性根据应用场景和应用需求加以改变。**方向图可重构天线**可以满足通信空间分集需求，在保持天线工作频率和极化方式不变的情况下改变天线的最大辐射方向，即方向图主瓣方向。相比于全向天线，能提高指定方向上的信号辐射或接受质量，又减少了不必要的能量辐射；相比于定向辐射天线，可以在不增加天线数量的情况下增加通信系统的灵活度；相比于相控阵天线，可以避免臣大的天线阵列和复杂的馈电系统，并且能极大降低通信系统成本。

## 应用场景

在商业应用方面，作为5G通信中的关键技术，大规模天线(Massive MIMO)技术通常使用密集天线阵列, 但是密集排布的天线不但会占据大量空间, 还会降低通信信道的自由度, 因而限制了多路复用增益的提高, 不利于通信性能的提高。相比之下, 天线可重构技术可以在不增加天线数量的情况下, 通过天线空间分集、辐射方向图分集或极化分集技术, 降低子信道的相关性, 进而提高通信系统容量。另外, 在移动卫星通信中, 车载、船载、机载等移动卫星通信应用的需求愈发强烈, 人们更希望交通工具在移动过程中保持卫星通信。但由于汽车、船只、飞机等移动交通工具在移动过程中位置和姿态不断变化, 普通天线难以保持辐射方向始终与通信卫星对准。而波束可重构天线可以根据交通工具的位置等信息计算出卫星相对位置, 改变天线辐射方向, 使交通工具在移动中实时保持卫星通信。

## 原理概述

本节介绍一维周期性排列的漏波单元设计一种波束可重构天线。

### 基片集成波导技术

矩形波导作为一种三维立体结构, 在与微带线等平面结构连接时往往需要复杂的三维连接结构, 吴柯等人于2001年提出了一种将微带线和矩形波导集成在同一个介质板上的方法<sup>[3]</sup>, 简化了两者的连接结构, 使用这种方法设计出的结构被称为基片集成波导(Substrate integrated waveguide, SIW)。基片集成波导通过在微带线介质板上打下一系列金属孔来模拟波导的传播形式, 解决了波导体积过大而不易集成的难题。

<div style="margin: 0 auto;" align="center">
    <img src="figures/SIW.png" width=400px></br>
    <b>图1. 基片集成波导示意图</b>
</div>

微带线结构具有体积小，重量轻，集成度高，工艺简单，成本低等优点，但是辐射泄露损耗大，品质因数低，在毫米波频段，这样的缺点尤为明显，因此限制了微带线在高频频段的应用。传统矩形波导虽然有着良好的电磁波传播特性，但是体积太大，不易集成，成本较高。而基片集成波导在避免了微带线和波导缺点的同时，又兼具了微带线和波导的优点：品质因数高，辐射损耗小，功率容量大，频带宽、抗电磁干扰能力强，并且体积小重量轻，容易设计、加工、集成，成本低。基片集成波导因其优势被广泛应于各种微波器件的设计中，例如天线、滤波器、功分器、振荡器、耦合器等等，尤其是在毫米波电路中，基片集成波导可以代替损耗高、Ｑ值低的微带线结构。除此之外，基片集成波导还支持高次模的传输，适合应用于高速信号传输系统的设计中，提高高速互连系统的数据传输速率以及频谱利用率.

基片集成波导是一种周期性结构，通常在PCB、LTCC上打金属过孔，起到金属电壁的作用，使电磁波被限制在通孔和金属平面共同形成的介质填充矩形波导内传输。基片集成波导上面的金属通孔为了减少损耗和电磁波泄露，需要满足如下条件:

<p align="center"><img alt="$$&#10;s&lt; 2d, \quad d &lt;0.2 w,&#10;$$" src="svgs/5e60cc4be33fdedbcee045f162a606a9.svg" align="middle" width="138.39785355pt" height="14.611878599999999pt"/></p>

其中<img alt="$d$" src="svgs/2103f85b8b1477f430fc407cad462224.svg" align="middle" width="8.55596444999999pt" height="22.831056599999986pt"/>表示金属通孔直径；<img alt="$s$" src="svgs/6f9bad7347b91ceebebd3ad7e6f6f2d1.svg" align="middle" width="7.7054801999999905pt" height="14.15524440000002pt"/>代表金属通孔排列周期，即相邻两通孔间的距离；<img alt="$w$" src="svgs/31fae8b8b78ebe01cbfbe2fe53832624.svg" align="middle" width="12.210846449999991pt" height="14.15524440000002pt"/>表示两排金属通孔之间的距离。

### 设计原理

基于单元相位调控的波束可重构天线，通过控制每个辐射单元的补偿相位，实现波束辐射方向的可重构特性。一维辐射单元按照图2的方法等间距周期性排列，图中黑点表示沿<img alt="$x$" src="svgs/332cc365a4987aacce0ead01b8bdcc0b.svg" align="middle" width="9.39498779999999pt" height="14.15524440000002pt"/>轴放置的单元.

<div style="margin: 0 auto;" align="center">
    <img src="figures/原理1.png" width=400px></br>
    <b>图2. 等间距周期排列单元示意图</b>
</div>

设相邻单元间隔距离为<img alt="$d_p$" src="svgs/23a76559c7248122345562ab3e71add4.svg" align="middle" width="15.33244184999999pt" height="22.831056599999986pt"/>, 具有这种排列结构的天线期望辐射波束的偏角为<img alt="$\theta$" src="svgs/27e556cf3caa0673ac49a8f0de3c73ca.svg" align="middle" width="8.17352744999999pt" height="22.831056599999986pt"/>时, 所需各个位置单元泄露出的电磁波应具有如下相位:

<p align="center"><img alt="$$&#10;\Phi_{\text{exp}} = - k_0 \cdot \sin\theta \cdot \left( n\cdot d_p\right) + \Phi_{\text{exp0}}, \quad  n=1,\ldots, N&#10;$$" src="svgs/74c5aa69864047561ca23c91afba6990.svg" align="middle" width="363.48619725pt" height="17.031940199999998pt"/></p>

其中<img alt="$k_0$" src="svgs/1b63f35b880a6307974273a3ff6063c9.svg" align="middle" width="15.11042279999999pt" height="22.831056599999986pt"/>表示自由空间波数, <img alt="$n$" src="svgs/55a049b8f161ae7cfeb0197d75aff967.svg" align="middle" width="9.86687624999999pt" height="14.15524440000002pt"/>为单元序列号, <img alt="$\Phi_{\text{exp0}}$" src="svgs/9960788b72e59f1aa802baa874d7ff1d.svg" align="middle" width="38.436259949999986pt" height="22.465723500000017pt"/>表示起始相位。而实际上, 电磁波在沿波导结构传送至各个单元位置时的相位为:

<p align="center"><img alt="$$&#10;\Phi_{\text{real}}=-k_g \cdot \left( n\cdot d_p\right) + \Phi_{\text{real0}}, \quad n=1,\ldots, N&#10;$$" src="svgs/75e7336dc6f89c36146196f890607680.svg" align="middle" width="323.28032385pt" height="17.031940199999998pt"/></p>

<img alt="$\Phi_{\text{real0}}$" src="svgs/e041dc1430ed11aa43744829c2732ac3.svg" align="middle" width="39.680556299999985pt" height="22.465723500000017pt"/>表示起始相位, <img alt="$k_g$" src="svgs/1401bd98b6700a93fc106aa528f75456.svg" align="middle" width="15.383845949999989pt" height="22.831056599999986pt"/>为电磁波在导波结构中传播的波数, <img alt="$k_g$" src="svgs/1401bd98b6700a93fc106aa528f75456.svg" align="middle" width="15.383845949999989pt" height="22.831056599999986pt"/>的计算方法为: <img alt="$k_g=\frac{2\pi}{\lambda_g}=k_0 \sqrt{\epsilon_r \mu_r}$" src="svgs/7165f30643a492455dd09ca94e7f6ed5.svg" align="middle" width="139.42500164999998pt" height="27.77565449999998pt"/>
综上, 各个单元需要补偿的相位为:

<p align="center"><img alt="$$&#10;\Phi_{\Delta}=\Phi_{\text{exp}}-\Phi_{\text{real}} = (k_g - k_0 \sin\theta) \cdot n \cdot d_p + \Phi_0, \quad n = 1, \ldots, N&#10;$$" src="svgs/9959476e8694d1594cc6353f99799c15.svg" align="middle" width="457.3058391pt" height="17.031940199999998pt"/></p>

<img alt="$\Phi_0$" src="svgs/621e65dab60f2d177b0f41784a500134.svg" align="middle" width="18.424726649999986pt" height="22.465723500000017pt"/>等于<img alt="$\Phi_{\text{exp0}}$" src="svgs/9960788b72e59f1aa802baa874d7ff1d.svg" align="middle" width="38.436259949999986pt" height="22.465723500000017pt"/>与<img alt="$\Phi_{\text{real0}}$" src="svgs/e041dc1430ed11aa43744829c2732ac3.svg" align="middle" width="39.680556299999985pt" height="22.465723500000017pt"/>之差, 在计算每个单元的补充相位时, 合理设计<img alt="$\Phi_0$" src="svgs/621e65dab60f2d177b0f41784a500134.svg" align="middle" width="18.424726649999986pt" height="22.465723500000017pt"/>可以提高波束的辐射方向精度。在天线设计中, 辐射单元沿导波结构等间距排列, 每个单元通过改变与导波结构相连的位置实现不同的相位补偿。每个单元与导波结构的连接方式有限, 以2-bit为例：

<div style="margin: 0 auto;" align="center">
    <img src="figures/原理2.png" width=600px></br>
    <b>图3. 一维2-bit单元排列示意图</b>
</div>

辐射单元按一维等间距周期排列, 相邻两单元相距<img alt="$d_p$" src="svgs/23a76559c7248122345562ab3e71add4.svg" align="middle" width="15.33244184999999pt" height="22.831056599999986pt"/>距离, 约为工作频率对应自由空间波长的一半。每个单元中, 有两个漏波结构对称排列于导波结构两侧, 2-bit编码的辐射单元有四种位置可与导波结构相连(如图3中A,B,C,D所示), 这四个位置分别编码为1,2,3,4。每次仅取一个位置与导波结构相连, 由于每个漏波结构的两个连接位置相邻距离<img alt="$d_s$" src="svgs/3f2c93f4db0df26af089195b2ac29c1c.svg" align="middle" width="14.760334049999992pt" height="22.831056599999986pt"/>为四分之一介质波长, 且漏波结构关于导波结构对称, 故1,2,3,4四个位置连接上导波结构分别可以补偿相位<img alt="$0^\circ$" src="svgs/54836da6218aedf599dfa60ca0de248e.svg" align="middle" width="14.954403749999988pt" height="22.63850490000001pt"/>, <img alt="$-90^\circ$" src="svgs/618d34bc6b3a55a1785c37b5910aba5f.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/>, <img alt="$-180^\circ$" src="svgs/ace3357a0a34bf381a0f9efdb6ae3429.svg" align="middle" width="44.17825664999999pt" height="22.63850490000001pt"/>, <img alt="$-270^\circ$" src="svgs/eef4f06f1324c265846096b8b24090d2.svg" align="middle" width="44.17825664999999pt" height="22.63850490000001pt"/>。将各个单元相位补偿公式计算所得结果数字化对应2-bit的标准如下:

<p align="center"><img alt="$$&#10;\Phi=\begin{cases}&#10;    0^\circ &amp; \Phi_{\Delta}&lt;-315^\circ~\text{or}~\Phi_{\Delta}\geq -45^\circ\\&#10;    -90^\circ &amp; -135^{\circ} \leq \Phi_{\Delta} &lt; -45^\circ\\&#10;    -180^\circ &amp; -225^{\circ} \leq \Phi_{\Delta} &lt; -135^\circ\\&#10;    -270^\circ &amp; -315^{\circ} \leq \Phi_{\Delta} &lt; -225^\circ\\&#10;\end{cases}&#10;$$" src="svgs/53c073dde6b32538eb47874ce886aba2.svg" align="middle" width="307.2375834pt" height="88.76802659999998pt"/></p>


## 仿真建模

基于以上的原理分析, 通过HFSS仿真软件模拟仿真以验证设计。共设计了10个连续排列的2-bit单元。

### 模型结构

天线设计及参数如图4, 表1所示。

<div style="margin: 0 auto;" align="center">
    <img src="figures/model_design.png" height=300px></br>
    <b>图4. 天线设计图</b>
</div>

<b>表1. 天线设计参数</b>
| 参数 | <img alt="$l_c$" src="svgs/4cc9e8e54a2e5e73ab9f2a4a0e13db35.svg" align="middle" width="10.77952754999999pt" height="22.831056599999986pt"/> | <img alt="$w_c$" src="svgs/6769e5356d96c7937a25a9e7ff1786e9.svg" align="middle" width="17.643161249999988pt" height="14.15524440000002pt"/> | <img alt="$l_s$" src="svgs/e65bf2ade026fd4982cacbfa9302d213.svg" align="middle" width="11.10924539999999pt" height="22.831056599999986pt"/> | <img alt="$w_s$" src="svgs/3d83e09256ee57f17530c5fca35206dd.svg" align="middle" width="17.97287909999999pt" height="14.15524440000002pt"/> | <img alt="$d_s$" src="svgs/3f2c93f4db0df26af089195b2ac29c1c.svg" align="middle" width="14.760334049999992pt" height="22.831056599999986pt"/> |
|:---:|:---:|:---:|:---:|:---:|:---:|
|值(mm)| 23 | 9.6 | 3 | 2 | 10 |
| 参数 | <img alt="$w_m$" src="svgs/632bb59e30c41191cd91e8dda5c8add4.svg" align="middle" width="23.433357749999992pt" height="14.15524440000002pt"/> | <img alt="$gap$" src="svgs/1885ff9fa2e7b1e1a4dd4965ee97a9bc.svg" align="middle" width="25.390077899999987pt" height="14.15524440000002pt"/> | <img alt="$l_1$" src="svgs/469f525d671e1e96713a0a17a13f2468.svg" align="middle" width="11.45742179999999pt" height="22.831056599999986pt"/> | <img alt="$w_1$" src="svgs/4b4518f1b7f0fb1347fa21506ebafb19.svg" align="middle" width="18.32105549999999pt" height="14.15524440000002pt"/> | <img alt="$d_p$" src="svgs/23a76559c7248122345562ab3e71add4.svg" align="middle" width="15.33244184999999pt" height="22.831056599999986pt"/> |
|值(mm)| 1.5 | 2 | 8 | 3 | 25 |

相应的呈现在HFSS中的模型如图5所示。

<div style="margin: 0 auto;" align="center">
    <img src="figures/HFSS_model.png" width=450px></br>
    <b>图5. HFSS天线模型</b>
</div>

> 图中, 红色方块表示连接到导波的开关, 矩形黄铜色为漏波单元棕色为微带线。

根据理论公式, 分别验证偏转角为<img alt="$-25^\circ$" src="svgs/ec89edf38d6eb8a69c246adcc3bd1180.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/>, <img alt="$0^\circ$" src="svgs/54836da6218aedf599dfa60ca0de248e.svg" align="middle" width="14.954403749999988pt" height="22.63850490000001pt"/>以及<img alt="$50^\circ$" src="svgs/a000665e9c369b09735b4fa1126f5ebb.svg" align="middle" width="23.17361309999999pt" height="22.63850490000001pt"/>三种情形, 计算可得这三种情形下10个单元导波连接方式分别为:

<div style="font-size: 12px">

| <span style="font-size:8px">目标角度</span>  | Unit1 | Unit2 | Unit3 | Unit4 | Unit5 | Unit6 | Unit7 | Unit8 | Unit9 | Unit10 |
|:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |
| <img alt="$-25^\circ$" src="svgs/ec89edf38d6eb8a69c246adcc3bd1180.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/> | 1 | 2 | 3 | 4 | 1 | 2 | 3 | 4 | 1 | 3 |
| <img alt="$0^\circ$" src="svgs/54836da6218aedf599dfa60ca0de248e.svg" align="middle" width="14.954403749999988pt" height="22.63850490000001pt"/> | 1 | 3 | 4 | 2 | 4 | 1 | 3 | 1 | 3 | 4 |
| <img alt="$50^\circ$" src="svgs/a000665e9c369b09735b4fa1126f5ebb.svg" align="middle" width="23.17361309999999pt" height="22.63850490000001pt"/> | 1 | 4 | 3 | 2 | 1 | 4 | 3 | 2 | 1 | 4 | 
</div>

### 仿真结果

三种目标角度对应的开关设计仿真图如下所示:

<div style="margin: 0 auto;" align="center">
    <img src="figures/angle=-25.png" width=450px></br>
    <b>(a) <img alt="$\theta=-25^\circ$" src="svgs/46963e026722e19e0a6a82122f92ad66.svg" align="middle" width="66.05020454999999pt" height="22.831056599999986pt"/></b></br>
    <img src="figures/angle=0.png" width=450px></br>
    <b>(b) <img alt="$\theta=0^\circ$" src="svgs/995f2c3701039f7b043ca86954be1591.svg" align="middle" width="45.045560999999985pt" height="22.831056599999986pt"/></b></br>
    <img src="figures/angle=50.png" width=450px></br>
    <b>(c) <img alt="$\theta=50^\circ$" src="svgs/9ab6b5f781d74465402de6b966661c9b.svg" align="middle" width="53.26477034999999pt" height="22.831056599999986pt"/></b></br>
    <b>图6. 不同波束方向角开关连接图示</b>
</div>


#### 实际波束方向角

+ <img alt="$-25^\circ$" src="svgs/ec89edf38d6eb8a69c246adcc3bd1180.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/>

<div style="margin: 0 auto;" align="center">
    <img src="figures/-25/xoz.png" width=450px></br>
    <b>(a) 极坐标</b></br>
    <img src="figures/-25/E_plane.png" width=450px></br>
    <b>(b) 平面坐标系</b></br>
    <img src="figures/-25/3d.png" width=450px></br>
    <b>(c) 3维图</b></br>
    <b>图7. <img alt="$-25^\circ$" src="svgs/ec89edf38d6eb8a69c246adcc3bd1180.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/>方向性仿真图</b>
</div>

> 实际得到的增益最高对应角度为<img alt="$-24^\circ$" src="svgs/8cf33389906482799b2b6b1feac27c59.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/>。

+ <img alt="$0^\circ$" src="svgs/54836da6218aedf599dfa60ca0de248e.svg" align="middle" width="14.954403749999988pt" height="22.63850490000001pt"/>

<div style="margin: 0 auto;" align="center">
    <img src="figures/0/xoz.png" width=450px></br>
    <b>(a) 极坐标</b></br>
    <img src="figures/0/E_plane.png" width=450px></br>
    <b>(b) 平面坐标系</b></br>
    <img src="figures/0/3d.png" width=450px></br>
    <b>(c) 3维图</b></br>
    <b>图8. <img alt="$0^\circ$" src="svgs/54836da6218aedf599dfa60ca0de248e.svg" align="middle" width="14.954403749999988pt" height="22.63850490000001pt"/>方向性仿真图</b>
</div>

> 实际得到的增益最高对应角度为<img alt="$-1^\circ$" src="svgs/8acd6a3c89428a5b72143e20f1c2863a.svg" align="middle" width="27.739837949999988pt" height="22.63850490000001pt"/>, 与论文[2]中结果一致。


+ <img alt="$50^\circ$" src="svgs/a000665e9c369b09735b4fa1126f5ebb.svg" align="middle" width="23.17361309999999pt" height="22.63850490000001pt"/>

<div style="margin: 0 auto;" align="center">
    <img src="figures/50/xoz.png" width=450px></br>
    <b>(a) 极坐标</b></br>
    <img src="figures/50/E_plane.png" width=450px></br>
    <b>(b) 平面坐标系</b></br>
    <img src="figures/50/3d.png" width=450px></br>
    <b>(c) 3维图</b></br>
    <b>图9. <img alt="$-25^\circ$" src="svgs/ec89edf38d6eb8a69c246adcc3bd1180.svg" align="middle" width="35.95904729999999pt" height="22.63850490000001pt"/>方向性仿真图</b>
</div>

> 实际得到的增益最高对应角度为<img alt="$46^\circ$" src="svgs/4f83ce5b8242f5e04fa7f191e5bb419b.svg" align="middle" width="23.17361309999999pt" height="22.63850490000001pt"/>, 与论文[2]中结果一致。


> 仿真记录: 仿真很吃内存, 约占50G; 过程耗时, 一组大约耗时10小时。

## 总结

本次课程设计复现了论文[2]中设计的基于微带线与基片集成波导技术的可重构天线。组合调节连续等间距排列于微带线上的单元与导波连接模式可构成对准不同角度的波束。调节方式易于计算, 为波束可重构天线设计提供了简单有效的方法。

## 参考文献

[1]. 刘丽. 基于超表面的波束可重构天线技术研究[D]. 2019.  
[2]. Chang L , Li Y , Zhang Z , et al. Reconfigurable 2-bit Fixed-Frequency Beam Steering Array Based on Microstrip Line[J]. IEEE Transactions on Antennas and Propagation, 2018, PP(99):1-1.  
[3]. Deslandes D , Wu K . Integrated microstrip and rectangular waveguide in planar form[J]. IEEE Microwave and Wireless Components Letters, 2002, 11(2):68-70.