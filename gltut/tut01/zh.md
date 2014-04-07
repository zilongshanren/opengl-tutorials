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
