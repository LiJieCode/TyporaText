# Paper

A Weak Galerkin Finite Element Method for the Maxwell Equations.pdf

- 弱旋度定义



A weak Galerkin mixed finite element method for second order elliptic problems_2014

- 弱散度定义



求解椭圆型方程界面问题的浸入界面方法_田敏2013

- 界面问题是指模型方程中的输入量如差分方程的系数，源项等在界面处不连续或奇异的情况这类问题的解也是不光滑或不连续的。
- 实际生活中的很多现象都可以归结为界面问题，如不同传导率的两种材料的拼接相同物质在不同状态下的混存如水和冰，细胞在血管中的流动以及地下水流经不同的物体如石块，海绵）等界面问题涉及环境科学，物理学，生物数学等学科领域，引起了许多科研工作者的浓厚兴趣，如何正确处理界面问题已经成为解决实际问题的关键因素之一。
- 目前处理界面问题的主要方法



202012椭圆界面问题基于界面松弛有限元法的多项式保持重构方法_楚天舒.caj

- 有限元方法发展的过程





202205椭圆型界面问题的破裂再生核方法_杨学敏.caj

- 对椭圆型界面问题进行数值求解，由于模型方程中的<span style="color:blue; font-weight:bold">系数不连续</span>或<span style="color:blue; font-weight:bold">源项奇异</span>，导致了解的整体光滑性差，故而用以往方法计算该微分方程问题时，数值解在界面处达不到预期的精度或方法的效果较差，有时甚至不可用．
- 界面问题是从实际生活中抽象出来的一类微分方程．当界面光滑时，其解在扩散系数光滑的界面上也充分光滑．但通常情况下，界面均存在间断，亦或均是不规则的几何界面，这使得从界面问题剥离出的偏微分方程的解通常在界面处不连续，导致了大多数常规的求解此类方程的数值解法失去了原有的效果
- <span style="color:red; font-weight:bold">众多学者对界面问题进行了研究并提出了不同解法：</span>
- <span style="color:red; font-weight:bold">椭圆型界面问题的研究现状</span>







201505几类界面问题的非拟合有限元方法分析_王秋亮bEnglish.caj

- 非匹配网格





202104几类各向异性界面问题的有限元-有限差分方法_董白英.caj

- 浸入界面方法，
- 浸入界面有限元方法





 

所以，界面问题的研究对象通常由多种不同物质组成，界面被不同介质互相分开，因此这也就导致了对应问题的真解在跨过界面时的低光滑性，甚至存在间断的现象。

 

 

 

现代科学研究的三大途径：实验，理论分析，科学计算

 

随着我国超算中心计算性能的逐渐提高，加之数值模拟具有可重复性、环保、成本低等优点，科学计算也继理论分析和实验分析之后成为了第三种重要的科学研究方法。

 

 

 

界面问题起源于两相和多相流的模拟，通常可划分为两类：

（1）模型方程中的扩散系数虽不连续，但不存在奇异源项。此时，方程的解虽在界面处连续，但解的梯度间断。

（2）模型方程中自身就含有奇异源项且扩散系数在界面处间断。这种情况下，源项的奇异性决定了微分方程的解在界面处的连续性，且解的梯度在界面处间断。

 

针对是第二类带有扩散系数的椭圆界面问题，此类问题有许多实际应用，如：晶体生长、工程中的流体、电磁场问题以及油田探测开采等．由于该类问题在实际生活中有重要作用，因此，研究椭圆型界面问题有着重要的学术意义和应用价值，而数值求解方法也可以为其他界面问题提供思路与方向．

发展和研究高精度及快速算法已成为当前计算数学界和工程界的前沿研究热点。在众多的数值方法中，有限元方法由于可采用高阶有限元空间、对问题区域的适应性强、理论基础较为完善等特点，该类方法及其各种变形得到了广泛关注和研究。有限元方法是求解偏微分方程的一种行之有效的数值方法,广泛应用与科学与工程计算的各领域。它的基本思想是分段函数（多项式）逼近与变分原理。



模型方程的系数间断，真解间断，或者源项间断的现象，我们称之为界面问题，间断面称为界面，







201412三维椭圆型界面问题的有限差分法_薛芳.caj

- 根据含水层结构不同, 渗流可分类为
- 各向同性流: 各向异性流: 







202106椭圆界面问题的广义有限差分方法_邢亚楠.caj

因此，人们开发了浸入有限元（IFE）方法来处理独立于界面的网格上的界面问题。  IFE 的研究始于20 年前，在数学上发展成熟 [7-10]。例如，Gong 等人[7]使用浸入界面有限元方法（IIFEM）来求解非均匀跳跃条件下的椭圆界面问题，He  等人[8]则使用浸入有限元方法（IFEM）处理这个问题。  Wang[9]研究了一种针对椭圆界面问题跳跃条件的捕获有限差分方法。He 等人[10]讨论了用于求解二阶椭圆界面问题的双线性浸入有限元（IFE）空间。 IFE 方法具有期望的最佳收敛速度，并为快速求解器提供了对称的正定矩阵。  IFE 方法适用于复杂的几何形状和边界条件，适合求解非线性和非均匀问题。此外，IFE 方法已被广泛用于航空航天工程[11,12]。















浸入界面方法是为解决界面问题而专门设计的．在浸入界面方法中，对于界面附近的不规则节点，其周围相邻的节点处于界面两侧．结合界面跳跃条件等相关界面信息和泰勒公式，在不规则节点上构造了修正的差分格式，确保数值解在界面附近的精度．误差分析说明该方法是一类精确的界面方法，在无穷范数下具有二阶精度．以二维为例，［２７］中提出的关于浸入界面方法原始思想中，对扩散项的离散格式中除了包含通常中心差分所必需的五个节点外，需要在其余相邻节点中选择一个附加节点，方法的稳定性和收敛性与该附加节点有关．对于二维椭圆界面问题，［４４］中基于二次优化方法提出了一类满足极值原理的浸入界面方法，该方法的离散矩阵是Ｍ－矩阵，是一个有效且稳健的数值方法．随后该方法被推广到三维椭圆问题［４５］、抛物问题［４６］及移动界面问题［４７］等．［４８］中，对二维椭圆界面问题基于浸入界面方法建立了一类快速算法，通过引入一个增广变量，将问题转化为由两个方程组成的方程组问题．其中，第一个控制方程是带有奇异源项的界面问题，离散格式采用五点中心差分格式的同时，仅需对源项的离散增加修正项，且离散线性方程组可以使用ＦＦＴ或ＡＤＩ等快速算法求解；另一个是増广变量所满足的关于流通量的界面跳跃条件，该方程仅定义在界面上，维数比原问题低一维，通常使用ＧＭＲＥＳ方法［４９］求解．随后，浸入界面方法被广泛用于各类界面问题，例如带有移动界面的晶体增长与Stefan、带有间断系数的双曲型波动方程、带有移动界面的不可压Stokes问题和Navier-Stokes问题等多相流问题．文献［５７－５９］中基于浸入界面方法研究了界面问题的几何型和代数型多重网格方法．







有限元方法

弱有限元方法

超罚弱有限元方法

 

 

非贴体网格，甚至笛卡尔网格

 

 

 

椭圆界面问题，抛物界面问题，弹性界面问题，Helmholtz界面问题，stokes界面问题





此外，Li等人结合浸入界面方法的思想又提出了浸入界面有限元方法[3]，L. Tao、Y. Lin和X. He等人在这方面做了很多工作，包括理论分析及方法的应用等．B. Camp和T. Lin等人在［７１－７４］中，分别对一维问题和带有特殊界面的二维问题探究了高阶浸入界面有限元方法的构造过程．通常情况，浸入有限元方法是针对带有齐次跳跃条件的界面问题的一类非协调有限元方法，在L2范数下具有二阶收敛性．［７５－７７］中讨论了基于非协调浸入有限元空间的间断有限元方法，［７８，７９］中结合有限体积格式构造了浸入有限体积方法，［８０］基于光滑方法研究了使用浸入有限元方法处理带有非齐次跳跃条件的界面问题，［８１］中证明了通过增加惩罚项消除非协调性的影响，从而构造了无穷范数下具有二阶精度的浸入有限元方法．Ｃｈｅｎ和Ｈ．Ｊｉ等人在［８２－８４］中结合增广浸入界面方法思想和浸入有限元方法提出了一类新的有限元方法，该方法能处理非齐次跳跃条件，且在无穷范数下具有二阶精度．













**二、国内外研究现状分析**

求解界面问题的方法有很多，若直接采用经典有限差分法或有限元方法，得到的数值解可能很不理想，甚至方法是不可用的．因为在界面附近，数值解可能会产生激烈的振荡，从而很难得到理想的逼近精度和逼近效果．因此，当使用传统的数值方法（例如有限元方法[1]）求解界面问题时，需要使用非结构化的贴体网格，即网格要沿着界面进行剖分，即网格只能穿过三角剖分的顶点，来保证这些方法的收敛性．但是贴体网格在实际应用中会带来一些不便，例如，当界面几何比较复杂时，很难生成高质量的贴体网格；或者涉及到动态移动界面时需要重复生成贴体网格等．因此，人们便开始基于非贴体网格来研究求解界面问题的数值方法．目前，基于非贴体网格（或Cartesian网格）的数值方法的研究已有丰富的成果，例如：1977年C.S.Peskin提出的浸入边界方法[7]，1984年A.Mayo提出的基于网格的边界积分方法[8]，1988年S.Osher等人提出的虚拟流体方法[9]，1994年LeVeque和Li提出的浸入界面方法[2]等．

浸入界面方法可用于处理带有间断系数和奇异源项的椭圆型方程，主要根据问题本身的物理背景或受约束的微分方程得到跳跃条件，推导出更多的界面关系式，在远离界面的区域通常采用标准的有限差分方法或有限元方法．对于界面附近的网格点或单元，则依据得到的界面关系来修正原有的数值方法，通过比较无穷范数下的误差量级，浸入界面方法具有整体的二阶收敛性．若系数、解及其流通量的不连续性消失，浸入界面方法就是标准的有限差分方法或有限元方法。另外，对于界面问题或定义在不规则区域上的问题，当流通量或解的跳跃条件以导数形式给出时，界面处跳跃关系式的推导会变的相对比较复杂，而且涉及到高阶导数，增加了求解问题的复杂性．因此，Li等人又提出了广义浸入界面方法．通过引入新的一维变量处理界面处导数形式的跳跃条件使其同时满足已知的跳跃条件，该方法可简化界面关系式的形式，利于问题的求解． 

此外，Li等人结合浸入界面方法的思想又提出了浸入界面有限元方法[3]．通常情况，浸入有限元方法是针对带有齐次跳跃条件的界面问题的一类非协调有限元方法，在L2范数下具有二阶收敛性．Chen和H.Ji等人结合增广浸入界面方法思想和浸入有限元方法提出了一类新的有限元方法[4-6]，该方法能处理非齐次跳跃条件，且在无穷范数下具有二阶精度．

弱有限元方法(Weak Galerkin)是由Wang和Ye首次提出用来求解二阶椭圆问题的．WG方法的主要思想是引入弱梯度来代替强梯度．首次提出的WG方法在网格单元内部考虑单值函数，Song和Liu等人在原有WG方法的基础上结合DG方法的思想提出了超罚弱有限元方法(Over-penalized WG，简称为OPWG)，在网格单元内部考虑双值函数，剖分网格边界考虑单值函数，因此就有了弱跳跃的产生，进而引入罚项用来保证稳定性，弱连续性通过罚项和WG方法中的稳定子共同保证，过罚项和WG方法中的稳定子共同保证，对于OPWG方法选取基函数时较为灵活，在解决低正则性等问题有独特的优势，也会显著提高并行计算的效率，对椭圆问题[]，椭圆界面问题[], 超收敛分析[孟瑞]，Helmholtz方程[孙燕]等都已有了相关研究．











\begin{frame}

 \frametitle{研究基础}

 \justifying

 \quad 首先考虑\textcolor{blue}{分片线性多项式空间}．设$T \in \mathcal{T}_h$是一个界面单元，用$A_1$，$A_2$和$A_3$来表示单元的三个顶点．界面曲线$\Gamma$与单元$T$交于两点$D$和$E$，线段$DE$将单元$T$分成两个子单元$T^-$和$T^-$，如图2.







 \begin{figure}[htp!]

  \centering

  \includegraphics[width=0.4\linewidth]{demo002.jpg}

  \caption{界面单元图.}       \label{fig:B}

 \end{figure}



\end{frame}













\begin{frame}

 \frametitle{研究基础}

 \quad 通过结合界面条件构造分片线性函数．具体而言，构造与单元顶点$A_i(i=1,2,3)$相关的三个线性多项式函数$\Phi _i(i=1,2,3)$如下：

 \[

  \Phi_{i}(x, y)=\left\{\begin{array}{ll}

   \Phi_{i}^{-}(x, y)=a_{i}^{-}+b_{i}^{-} x+c_{i}^{-} y & \text { if }(x, y) \in T^{-} \\

   \Phi_{i}^{+}(x, y)=a_{i}^{+}+b_{i}^{+} x+c_{i}^{+} y & \text { if }(x, y) \in T^{+}

  \end{array},\right.

 \]

 根据前面分析，$\Phi _i(i=1,2,3)$应满足以下条件：

 \begin{enumerate}

  \item 节点值条件：

​     \[

​      \Phi_{i}(A_j)=\delta_ij, i=1,2,3

​     \]

  \item 函数跳跃条件：

​     \[

​      \left [ \left [  \Phi_i(D) \right ]  \right ]=\varphi (D),  \left [ \left [  \Phi_i(E) \right ]  \right ]=\varphi(E), i=1,2,3

​     \]

  \item 通量法向分量跳跃条件：

​     \[

​      \left [ \left [  \beta \frac{\partial \Phi_i }{\partial \mathbf n}  \right ]  \right ]=\psi

​     \]

 \end{enumerate}

\end{frame}











众所周知，跳跃条件可用于唯一定义材料界面上的线性IFE基函数。

界面跳转条件不足以唯一地确定更高阶IFE基函数。

不适当地选择额外条件来定义更高阶IFE基函数可能导致次优逼近能力











