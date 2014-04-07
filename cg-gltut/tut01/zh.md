---
layout: default
title: 第一章:预备知识
section: cg-gltut/tut01
---
<style>
  h3 {
	margin: 20px 0px 10px 0px;
  }
</style>

免责申明（必读！）：本网站提供的所有教程的翻译原稿均来自于互联网，仅供学习交流之用，切勿进行商业传播。同时，转载时不要移除本申明。如产生任何纠纷，均与本博客所有人、发表该翻译稿之人无任何关系。谢谢合作！

原文链接：[http://www.arcsynthesis.org/gltut/Basics/Introduction.html](http://www.arcsynthesis.org/gltut/Basics/Introduction.html)

##第一部分： 基础

进行图形编程对于许多新人来说是一项非常艰难的任务。渲染管线（rendering pipeline）涉及了许多步骤，每一个步骤都需要进行大量数学操作。某一些渲染管线的阶段(stage)还可以运行一些程序，程序的结果可以供后续阶段使用。

理解渲染管线并且能够把它当成实现许多视觉效果的工具，这是对于一个图形程序员(graphics programmer)的基本要求。

本章将介绍3D图形学中涉及到的基础数学。同时，它也会简单地介绍一下OpenGL的渲染管线。并且，我会向你展示数据是如何在渲染管线中流动的。

本章与其它章节有所不同，因为它不包含任何的源代码。在本章中，我们将会学习到向量数学，图形渲染理论以及OpenGL。

这也是阅读本系列教程的入门篇。

###Vector Math(向量数学)

本书假设你熟悉基本的代数和几何，但是你不一定要了解向量数学。后面的内容会向你介绍一些更复杂的内容，但是，本章，我们只介绍基本的vector math.

一个向量可以有许多含义，具体含义取决于我们是怎么看待它的，是从几何角度来看，还是从数值角度来看。这两个角度，向量都是具有维度(dimension)的。

一个二维向量被给定在一个平面内，而一个三维向量则可以指向任何物理空间。向量还可以有更多的维度，但是，通常我们讨论向量都只关心2维到4维的情况。

理论上来说，一个向量也可以只含一个维度。这样的向量叫做标量(scalar).

就几何意义来说，一个向量可以表示两层含义：一个点或者一个给定平面内的一个方向。一个向量坐标可以表示一个空间内的一个位置。比如，下图中我们有一个位置向量A:

####Figure 1. Position Vectors(位置向量)

![figure1](./res/VectorPosition.svg)

一个向量也可以表示一个方向。方向向量是没有原点（origin）的。它仅仅表示的是一个空间中的方向而已。

下图中的向量都是方向向量，但是向量B和向量D是等价的，虽然看起来它们画的位置可能有所差别.

####Figure 2. Direction Vectors(方向向量)

![figure2](./res/VectorDirections.svg)

从几何的角度来看，这样子描述向量是非常好的，但是向量也可以有它的数值(numerically)表示形式。在这种情况下，一个向量被表示成一串数字序列，每一维有一个相应的数字。

因此，一个二维的向量有两个数，而一个三维的向量则有三个数。以此类推，n维的向量就有n维的数。而标量，从数值表示来看，它只含一个数。

向量中的每一维里的数被叫做向量的分量(component)。每一个分量通常会指定名字。比如，一个向量的第一个分量一般叫做X分量。

第二个分量叫做Y分量，第三个是Z分量。如果它有第四个分量的话，那么就命名为W。

当用我们书写向量的时候，通常用小括号把向量的各个分量括起来，中间用逗号隔开。

因此，一个3D向量可以写成(0,2,4);它的x分量是0，y分量是2，而z分量是4.当我们把向量写作一个方程式的时候，它的写法如下：

![columnVector](./res/ColumnVector.svg)

在数学方程中，向量的名字一般用粗体表示，而它的头上会标有一个箭头符号,表示这个变量是有方向的。

当我们作图来表示向量的时候，位置向量和方向向量是有所区别的。然而它们的数值表示却看不出差别。

惟一的区别就是你怎么使用它们。因此，你可以把一个向量当做是一个位置或者一个方向，然后对它做相应的向量运算，然后再考虑它的结果是一个位置还是一个方向。

虽然，向量有单独的数值分量，但是一个向量作为一个整体也可以对它进行一些数学操作。

我们接下来会从几何和数值角度介绍一些向量运算.

###Vector Addition(向量加法)

我们可以把两个向量相加。它的几何意义如下所示：

####Figure 3. Vector Addition

![VectorAddition](./res/VectorAddition.svg)

记住：向量的方向是可以平移而它的值是不会受到影响的。因此，你可以把两个向量首尾相连，那么两个向量的和就是从第一个向量的头指向第二个向量的尾。（我们假定箭头表示向量的尾部。）

###Figure 4. Vector Addition Head-to-Tail

![VectorAdditionHeads](./res/VectorAdditionHeads.svg)

从数值角度来看，向量的加法仅仅是两个分量分别相加即可。

####Equation 1. Vector Addition with Numbers

![VectorAdditionNum](./res/VectorAdditionNum.svg)

任何操作，如何它是针对向量的每一个分量进行运算，那么此操作叫做“逐分量”操作。

向量加法是逐分量操作。任何逐分量操作都要求两个进行运算的向量有相同的维度。

####Vector Negation and Subtraction.

你也可以对一个向量取反。它的结果就是调转向量的方向:

####Figure 5. Vector Negation(向量取反)

![VectorNegation](./res/VectorNegation.svg)

从数值角度来看，这意味着对向量的每一个分量都要取反。

####Equation 2. Vector Negation

![VectorNegationNum](./res/VectorNegationNum.svg)

正如同标量数学一样，向量的减法其实就是向量的加法，只不过第二个向量先做取反操作而已。

####Figure 6. Vector Subtraction

![VectorSubtraction](./res/VectorSubtraction.svg)

####Vector Multiplication.

向量的乘法是诸多向量运算之中没有几何意义的一个。

把两个方向相乘，或者把两个位置相乘，这并得不出什么几何意义。但是，这并不意味着向量乘法没有用了,在某些场合下还是有用的.

两个向量的乘法只需要把两个向量的对应分量相乘即可，这一点和向量的加法很像。

####Equation 3. Vector Multiplication(向量乘法)

![VectorMultiplicationNum](./res/VectorMultiplicationNum.svg)

####Vector/Scalar Operations.

向量也可以和标量参与运算。回想一下，标量就是一个数字。向量是可以乘以一个标量的。

这样会使向量的长度变大或者变小，取决于被乘标量的值。

####Figure 7. Vector Scaling(向量缩放)

![VectorScalarMult](./res/VectorScalarMult.svg)

从数值角度来看，这也是一个逐分量的乘法，向量的每一个分量都和这个标量进行乘法运算.

####Equation 4. Vector-Scalar Multiplication

![VectorScalarMultNum](./res/VectorScalarMultNum.svg)

标量也可以与向量相加。这一点跟向量与向量的乘法类似，它也是没有几何意义的。我们只需要把向量的每一个分量与此标量相加即可。

####Equation 5. Vector-Scalar Addition

![VectorScalarAddNum](./res/VectorScalarAddNum.svg)

####Vector Algebra(向量代数)

掌握这些向量操作及其几何、数值意义对我们搞图形学是非常有好处的。

向量与向量的加法和乘法规则同样适应于标量与向量的乘法与加法。它们都满足交换率(commutative)，结合率（associative）和分配率(distributive).

####Equation 6. Vector Algebra

![VectorMathProperties](./res/VectorMathProperties.svg)

向量/标量 运算有类似的属性。

**长度(Length)**.
向量是有长度的。一个向量的长度是从它的起始点到结束点的距离。

从数值角度来看，我们可以通过以下方程式来计算。

####Equation 7. Vector Length

![VectorLengthNum](./res/VectorLengthNum.svg)

这里使用了毕达哥拉期(Pythagorean)定理来计算向量的长度。这个方程可以适应于任何维度的向量长度计算，不只是2维或者3维。

**单位向量和正规化(Unit Vectors and Normalization)**.
一个向量如果长度为1，那么我们管它叫做单位向量（unit vector）。它通常用来表示一个方向上的基准长度。
一个单位向量在数学方程中可以表示为a^（注意这个^要放在变量的名字上面）.

一个向量也可以通过正规化方法转化成一个单位向量。我们可以通过除以向量的长度来计算，或者乘以向量长度的倒数(reciprocal)。

####Equation 8. Vector Normalization(向量正规化)

![VectorNormalizationNum](./res/VectorNormalizationNum.svg)

本节并没有介绍所有的向量运算。一些新的向量运算会在后续章节中逐步引入。(译者：比如向量的点积和叉积就没有介绍).

本节介绍的向量运算大部分都是逐分量的运算。

**区间符号(Range Notation)**.
本系列教程中会经常使用到一些标准符号用来表示一个值在某一个区间范围内。

如果一个值的范围是0到1，同时它包含0和1，那么此值的区间表示形式为[0,1].

这个方括号表示范围是包含该值的。

如果一个值的范围是0到1，但是它不包含0，同时包含1，那么它的区间表示为(0,1].

这里的括号表示不包含该边界值。

如果一个值的范围是大于等于，且它的上限是正无穷大，那么它的区间表示形式为[0, ∞).

相反，如果一个值的范围是小于0并且它的下限是负无穷大，那么可以表示为 (-∞, 0).
