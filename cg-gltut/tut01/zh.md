---
layout: default
title: 第一章: 预备知识
section: cg-gltut/tut01
---
<style>
  h3 {
	margin: 20px 0px 10px 0px;
  }
</style>

免责申明（必读！）：本网站提供的所有教程的翻译原稿均来自于互联网，仅供学习交流之用，切勿进行商业传播。同时，转载时不要移除本申明。如产生任何纠纷，均与本博客所有人、发表该翻译稿之人无任何关系。谢谢合作！

原文链接：[http://www.arcsynthesis.org/gltut/Basics/Introduction.html](http://www.arcsynthesis.org/gltut/Basics/Introduction.html)

##Part I. The Basics

Graphics programming can be a daunting task when starting out. The rendering pipeline involves a large number of steps,
each dealing with a variety of math operations. It has stages that run actual programs to compute results for the next.
Mastering this pipeline, being able to use it as a tool to achieve a visual effect, is the essence of being a graphics programmer.

This section of the book will introduce the basic math necessary for 3D graphics. It will introduce the rendering pipeline as defined by OpenGL.
And it will demonstrate how data flows through the graphics pipeline.

Unlike most sections of this text, there is no source code or project associated with this section. Here, we will be discussing vector math, graphical rendering theory, and OpenGL. This serves as a primer to the rest of the book.

###Vector Math

This book assumes that you are familiar with algebra and geometry, but not necessarily with vector math. Later material will bring you up to speed on more complex subjects, but this will introduce the basics of vector math.

A vector can have many meanings, depending on whether we are talking geometrically or numerically. In either case, vectors have dimensionality; this represents the number of dimensions that the vector has. A two-dimensional vector is restricted to a single plane, while a three-dimensional vector can point in any physical space. Vectors can have higher dimensions, but generally we only deal with dimensions between 2 and 4.

Technically, a vector can have only one dimension. Such a vector is called a scalar.

In terms of geometry, a vector can represent one of two concepts: a position or a direction within a particular space. A vector position represents a specific location in space. For example, on this graph, we have a vector position A:

####Figure 1. Position Vectors

![figure1](./res/VectorPosition.svg)

A vector can also represent a direction. Direction vectors do not have an origin; they simply specify a direction in space.

These are all direction vectors, but the vectors B and D are the same, even though they are drawn in different locations:

####Figure 2. Direction Vectors

![figure2](./res/VectorDirections.svg)

That's all well and good for geometry, but vectors can also be described numerically. A vector in this case is a sequence of numbers, one for each dimension.

So a two-dimensional vector has two numbers; a three-dimensional vector has three. And so forth. Scalars, numerically speaking, are just a single number.

Each of the numbers within a vector is called a component. Each component usually has a name. For our purposes, the first component of a vector is the X component.

The second component is the Y component, the third is the Z, and if there is a fourth, it is called W.

When writing vectors in text, they are written with parenthesis.

So a 3D vector could be (0, 2, 4); the X component is 0, the Y component is 2, and the Z component is 4. When writing them as part of an equation, they are written as follows:

![columnVector](./res/ColumnVector.svg)

n math equations, vector variables are either in boldface or written with an arrow over them.

When drawing vectors graphically, one makes a distinction between position vectors and direction vectors. However, numerically there is no difference between the two.

The only difference is in how you use them, not how you represent them with numbers. So you could consider a position a direction and then apply some vector operation to them,
and then consider the result a position again.

Though vectors have individual numerical components, a vector as a whole can have a number of mathematical operations applied to them.

We will show a few of them, with both their geometric and numerical representations.

###Vector Addition.

You can take two vectors and add them together. Graphically, this works as follows:

![VectorAddition](./res/VectorAddition.svg)

Remember that vector directions can be shifted around without changing their values. So if you put two vectors head to tail,
the vector sum is simply the direction from the tail of the first vector to the head of the last.

###Figure 4. Vector Addition Head-to-Tail

![VectorAdditionHeads](./res/VectorAdditionHeads.svg)

Numerically, the sum of two vectors is just the sum of the corresponding components:

####Equation 1. Vector Addition with Numbers

![VectorAdditionNum](./res/VectorAdditionNum.svg)

Any operation where you perform an operation on each component of a vector is called a component-wise operation.

Vector addition is component-wise. Any component-wise operation on two vectors requires that the two vectors have the same dimensionality.

####Vector Negation and Subtraction.

You can negate a vector. This reverses its direction:

####Figure 5. Vector Negation

![VectorNegation](./res/VectorNegation.svg)

Numerically, this means negating each component of the vector.

####Equation 2. Vector Negation

![VectorNegationNum](./res/VectorNegationNum.svg)

Just as with scalar math, vector subtraction is the same as addition with the negation of the second vector.

####Figure 6. Vector Subtraction

![VectorSubtraction](./res/VectorSubtraction.svg)

####Vector Multiplication.

Vector multiplication is one of the few vector operations that has no real geometric equivalent.

To multiply a direction by another, or multiplying a position by another position, does not really make sense. That does not mean that the numerical equivalent is not useful, though.

Multiplying two vectors numerically is simply component-wise multiplication, much like vector addition.

####Equation 3. Vector Multiplication

![VectorMultiplicationNum](./res/VectorMultiplicationNum.svg)

####Vector/Scalar Operations.

Vectors can be operated on by scalar values. Recall that scalars are just single numbers. Vectors can be multiplied by scalars.

This magnifies or shrinks the length of the vector, depending on the scalar value.

####Figure 7. Vector Scaling

![VectorScalarMult](./res/VectorScalarMult.svg)

Numerically, this is a component-wise multiplication, where each component of the vector is multiplied with each component of the scalar.

####Equation 4. Vector-Scalar Multiplication

![VectorScalarMultNum](./res/VectorScalarMultNum.svg)

Scalars can also be added to vectors. This, like vector-to-vector multiplication, has no geometric representation. It is a component-wise addition of the scalar with each component of the vector.

####Equation 5. Vector-Scalar Addition

![VectorScalarAddNum](./res/VectorScalarAddNum.svg)

####Vector Algebra.

It is useful to know a bit about the relationships between these kinds of vector operations.

Vector addition and multiplication follow many of the same rules for scalar addition and multiplication. They are commutative, associative, and distributive.

####Equation 6. Vector Algebra

![VectorMathProperties](./res/VectorMathProperties.svg)

Vector/scalar operations have similar properties.

**Length**. Vectors have a length. The length of a vector direction is the distance from the starting point to the ending point.

Numerically, computing the distance requires this equation:

####Equation 7. Vector Length

![VectorLengthNum](./res/VectorLengthNum.svg)

This uses the Pythagorean theorem to compute the length of the vector. This works for vectors of arbitrary dimensions, not just two or three.


**Unit Vectors and Normalization**. A vector that has a length of exactly one is called a unit vector. This represents a pure direction with a standard, unit length. A unit vector variable in math equations is written with a ^ over the variable name.

A vector can be converted into a unit vector by normalizing it. This is done by dividing the vector by its length. Or rather, multiplication by the reciprocal of the length.

####Equation 8. Vector Normalization

![VectorNormalizationNum](./res/VectorNormalizationNum.svg)

This is not all of the vector math that we will use in these tutorials. New vector math operations will be introduced and explained as needed when they are first used.

And unlike the math operations introduced here, most of them are not component-wise operations.

Range Notation. This book will frequently use standard notation to specify that a value must be within a certain range.

If a value is constrained between 0 and 1, and it may actually have the values 0 and 1, then it is said to be “on the range” [0, 1].

The square brackets mean that the range includes the value next to it.

If a value is constrained between 0 and 1, but it may not actually have a value of 0, then it is said to be on the range (0, 1].

The parenthesis means that the range does not include that value.

If a value is constrained to 0 or any number greater than zero, then the infinity notation will be used. This range is represented by [0, ∞).

Note that infinity can never be reached, so it is always exclusive. A constraint to any number less than zero, but not including zero would be on the range (-∞, 0).
