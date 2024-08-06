---
layout: post
title: Rasterization - How Computers Render 3D Fast
author: Alexander Kaminsky
---

In the early days of computer graphics, performance of rendering techniques was especially important. For this reason, we relied heavily on approximations of how we capture images in real life.

Rasterization is a process in 3D computer graphics that converts 3D models into a 2D image, which can be displayed on a screen. It involves taking the vertices defining the geometry of 3D objects, projecting them onto an image, and then filling in the pixels that fall within the boundaries of those projected shapes.

In a way, this approach is similar to how a painter would start by drawing sketch lines (the projection stage) before painting/filling them in (the rasterization stage).

![]({{ site.baseurl }}/images/Dolphin_triangle_mesh.png)

<p style="font-size:0.8em; text-align:center">
    A polygon mesh of a dolphin represented using triangle primitives. In the process of rasterization, triangles are drawn to the image one at a time. 
    Chrschn. "Dolphin Triangle Mesh," <i>Wikimedia Commons</i>, 27 Mar. 2007, en.wikipedia.org/wiki/File:Dolphin_triangle_mesh.png.
</p>

## What do we mean by projection?

Projection is the process of mapping 3D points onto a 2D plane, like the 2D image that is eventually displayed on our computer screen. It transforms the positions of objects in a 3D space into corresponding positions on a 2D surface, simulating the view from a camera. One way of achieving this is using a [Model View Projection](https://jsantell.com/model-view-projection/) (MVP) matrix. The article I linked provides some really helpful visuals for understanding this transformation process.

## Shading

Similar to how an artist would have to shade the shapes that compose a drawing, in rasterization, models such as the [Phong shading model](https://learnopengl.com/Lighting/Basic-Lighting) are used to simulate how the effects of lighting on the final colouring of the shapes we draw.

## Ordering

One of the challenges with rasterization is determining the correct order in which the shapes should be drawn to our image. This is analogous to how a painter typically begins with a background and work towards the foreground.

One approach is **depth buffering**: To solve the ordering problem, a depth buffer is used. A buffer in this case is just a large block of computer memory. This buffer keeps track of the depth (distance from the camera) of each pixel. When a new pixel is processed from another shape, its depth is compared to the value already stored in the depth buffer. If the new pixel is closer to the camera, it updates the color and depth values; if not, it is discarded.

Another approach is **front-to-back rendering**. This requires sorting objects based on their distance from the camera to ensure they are processed in the correct order. Since the camera can move around the scene, this ordering needs to be frequently recomputed.

This problem becomes more challenging when shapes with transparency are introduced (no details).

## Further Reading

If this post has interested you in building your own 3D rasterized, I personally found [_LearnOpenGL_](https://learnopengl.com/) by Joey de Vries very helpful when starting out. It goes into the specific details of building a rasterizer using OpenGL, which is a standard that allows you to take advantage of your computer's graphics processing hardware.

**Note:** this post has given simply an overview. There are many details that I did not fill in. Following the linked guide will require some prerequisite knowledge in programming. Otherwise, it might become difficult to follow. For complete beginners I would suggest practicing programming skills with simpler projects first!