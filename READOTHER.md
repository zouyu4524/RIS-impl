# 天线理论与技术课程设计

<div style="margin: 0 auto; font-size: 20px; font-weight: bold;" align="center">邹雨泽</div>

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

$$
s< 2d, \quad d <0.2 w,
$$

其中$d$表示金属通孔直径；$s$代表金属通孔排列周期，即相邻两通孔间的距离；$w$表示两排金属通孔之间的距离。

### 设计原理

基于单元相位调控的波束可重构天线，通过控制每个辐射单元的补偿相位，实现波束辐射方向的可重构特性。一维辐射单元按照图2的方法等间距周期性排列，图中黑点表示沿$x$轴放置的单元.

<div style="margin: 0 auto;" align="center">
    <img src="figures/原理1.png" width=400px></br>
    <b>图2. 等间距周期排列单元示意图</b>
</div>

设相邻单元间隔距离为$d_p$, 具有这种排列结构的天线期望辐射波束的偏角为$\theta$时, 所需各个位置单元泄露出的电磁波应具有如下相位:

$$
\Phi_{\text{exp}} = - k_0 \cdot \sin\theta \cdot \left( n\cdot d_p\right) + \Phi_{\text{exp0}}, \quad  n=1,\ldots, N
$$

其中$k_0$表示自由空间波数, $n$为单元序列号, $\Phi_{\text{exp0}}$表示起始相位。而实际上, 电磁波在沿波导结构传送至各个单元位置时的相位为:

$$
\Phi_{\text{real}}=-k_g \cdot \left( n\cdot d_p\right) + \Phi_{\text{real0}}, \quad n=1,\ldots, N
$$

$\Phi_{\text{real0}}$表示起始相位, $k_g$为电磁波在导波结构中传播的波数, $k_g$的计算方法为: $k_g=\frac{2\pi}{\lambda_g}=k_0 \sqrt{\epsilon_r \mu_r}$
综上, 各个单元需要补偿的相位为:

$$
\Phi_{\Delta}=\Phi_{\text{exp}}-\Phi_{\text{real}} = (k_g - k_0 \sin\theta) \cdot n \cdot d_p + \Phi_0, \quad n = 1, \ldots, N
$$

$\Phi_0$等于$\Phi_{\text{exp0}}$与$\Phi_{\text{real0}}$之差, 在计算每个单元的补充相位时, 合理设计$\Phi_0$可以提高波束的辐射方向精度。在天线设计中, 辐射单元沿导波结构等间距排列, 每个单元通过改变与导波结构相连的位置实现不同的相位补偿。每个单元与导波结构的连接方式有限, 以2-bit为例：

<div style="margin: 0 auto;" align="center">
    <img src="figures/原理2.png" width=600px></br>
    <b>图3. 一维2-bit单元排列示意图</b>
</div>

辐射单元按一维等间距周期排列, 相邻两单元相距$d_p$距离, 约为工作频率对应自由空间波长的一半。每个单元中, 有两个漏波结构对称排列于导波结构两侧, 2-bit编码的辐射单元有四种位置可与导波结构相连(如图3中A,B,C,D所示), 这四个位置分别编码为1,2,3,4。每次仅取一个位置与导波结构相连, 由于每个漏波结构的两个连接位置相邻距离$d_s$为四分之一介质波长, 且漏波结构关于导波结构对称, 故1,2,3,4四个位置连接上导波结构分别可以补偿相位$0^\circ$, $-90^\circ$, $-180^\circ$, $-270^\circ$。将各个单元相位补偿公式计算所得结果数字化对应2-bit的标准如下:

$$
\Phi=\begin{cases}
    0^\circ & \Phi_{\Delta}<-315^\circ~\text{or}~\Phi_{\Delta}\geq -45^\circ\\
    -90^\circ & -135^{\circ} \leq \Phi_{\Delta} < -45^\circ\\
    -180^\circ & -225^{\circ} \leq \Phi_{\Delta} < -135^\circ\\
    -270^\circ & -315^{\circ} \leq \Phi_{\Delta} < -225^\circ\\
\end{cases}
$$


## 仿真建模

基于以上的原理分析, 通过HFSS仿真软件模拟仿真以验证设计。共设计了10个连续排列的2-bit单元。

### 模型结构

天线设计及参数如图4, 表1所示。

<div style="margin: 0 auto;" align="center">
    <img src="figures/model_design.png" height=300px></br>
    <b>图4. 天线设计图</b>
</div>

<b>表1. 天线设计参数</b>
| 参数 | $l_c$ | $w_c$ | $l_s$ | $w_s$ | $d_s$ |
|:---:|:---:|:---:|:---:|:---:|:---:|
|值(mm)| 23 | 9.6 | 3 | 2 | 10 |
| 参数 | $w_m$ | $gap$ | $l_1$ | $w_1$ | $d_p$ |
|值(mm)| 1.5 | 2 | 8 | 3 | 25 |

相应的呈现在HFSS中的模型如图5所示。

<div style="margin: 0 auto;" align="center">
    <img src="figures/HFSS_model.png" width=450px></br>
    <b>图5. HFSS天线模型</b>
</div>

> 图中, 红色方块表示连接到导波的开关, 矩形黄铜色为漏波单元棕色为微带线。

根据理论公式, 分别验证偏转角为$-25^\circ$, $0^\circ$以及$50^\circ$三种情形, 计算可得这三种情形下10个单元导波连接方式分别为:

<div style="font-size: 12px">

| <span style="font-size:8px">目标角度</span>  | Unit1 | Unit2 | Unit3 | Unit4 | Unit5 | Unit6 | Unit7 | Unit8 | Unit9 | Unit10 |
|:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |:---: |
| $-25^\circ$ | 1 | 2 | 3 | 4 | 1 | 2 | 3 | 4 | 1 | 3 |
| $0^\circ$ | 1 | 3 | 4 | 2 | 4 | 1 | 3 | 1 | 3 | 4 |
| $50^\circ$ | 1 | 4 | 3 | 2 | 1 | 4 | 3 | 2 | 1 | 4 | 
</div>

### 仿真结果

三种目标角度对应的开关设计仿真图如下所示:

<div style="margin: 0 auto;" align="center">
    <img src="figures/angle=-25.png" width=450px></br>
    <b>(a) $\theta=-25^\circ$</b></br>
    <img src="figures/angle=0.png" width=450px></br>
    <b>(b) $\theta=0^\circ$</b></br>
    <img src="figures/angle=50.png" width=450px></br>
    <b>(c) $\theta=50^\circ$</b></br>
    <b>图6. 不同波束方向角开关连接图示</b>
</div>


#### 实际波束方向角

+ $-25^\circ$

<div style="margin: 0 auto;" align="center">
    <img src="figures/-25/xoz.png" width=450px></br>
    <b>(a) 极坐标</b></br>
    <img src="figures/-25/E_plane.png" width=450px></br>
    <b>(b) 平面坐标系</b></br>
    <img src="figures/-25/3d.png" width=450px></br>
    <b>(c) 3维图</b></br>
    <b>图7. $-25^\circ$方向性仿真图</b>
</div>

> 实际得到的增益最高对应角度为$-24^\circ$。

+ $0^\circ$

<div style="margin: 0 auto;" align="center">
    <img src="figures/0/xoz.png" width=450px></br>
    <b>(a) 极坐标</b></br>
    <img src="figures/0/E_plane.png" width=450px></br>
    <b>(b) 平面坐标系</b></br>
    <img src="figures/0/3d.png" width=450px></br>
    <b>(c) 3维图</b></br>
    <b>图8. $0^\circ$方向性仿真图</b>
</div>

> 实际得到的增益最高对应角度为$-1^\circ$, 与论文[2]中结果一致。


+ $50^\circ$

<div style="margin: 0 auto;" align="center">
    <img src="figures/50/xoz.png" width=450px></br>
    <b>(a) 极坐标</b></br>
    <img src="figures/50/E_plane.png" width=450px></br>
    <b>(b) 平面坐标系</b></br>
    <img src="figures/50/3d.png" width=450px></br>
    <b>(c) 3维图</b></br>
    <b>图9. $50^\circ$方向性仿真图</b>
</div>

> 实际得到的增益最高对应角度为$46^\circ$, 与论文[2]中结果一致。


> 仿真记录: 仿真很吃内存, 约占50G; 过程耗时, 一组大约耗时10小时。

## 总结

本次课程设计复现了论文[2]中设计的基于微带线与基片集成波导技术的可重构天线。组合调节连续等间距排列于微带线上的单元与导波连接模式可构成对准不同角度的波束。调节方式易于计算, 为波束可重构天线设计提供了简单有效的方法。

## 参考文献

[1]. 刘丽. 基于超表面的波束可重构天线技术研究[D]. 2019.  
[2]. Chang L , Li Y , Zhang Z , et al. Reconfigurable 2-bit Fixed-Frequency Beam Steering Array Based on Microstrip Line[J]. IEEE Transactions on Antennas and Propagation, 2018, PP(99):1-1.  
[3]. Deslandes D , Wu K . Integrated microstrip and rectangular waveguide in planar form[J]. IEEE Microwave and Wireless Components Letters, 2002, 11(2):68-70.