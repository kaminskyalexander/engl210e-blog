---
layout: post
title: How Do Computers Render 3D?
author: Alexander Kaminsky
---

3D computer generated images are everywhere: video games, film and television, engineering, research and education, and so much more. How are computers able to produce these kinds of images? In this post, I will go over the key information needed to understand what happens behind the scenes.

![]({{ site.baseurl }}/images/animation01-1280x720.jpg)

<p style="font-size:0.8em; text-align:center">
    Screenshot of animation in Blender 3D Software. The images visible to the artist in the software are generated in real-time. "Home of the Blender project - Free and Open 3D Creation Software." <i>Blender</i>, https://www.blender.org/
</p>
<!-- https://www.blender.org/ -->

In essence, the goal is to simulate a camera's view into a virtual 3D world, similar to how a camera in the real world would be able to produce an image.

## Simulating a camera

At first, the solution to this problem might seem straightforward. We could try to simulate the way a camera works in the real world. That is, we would use our understanding of the physical world, to simulate the emission of light from light sources in our world (for example, the sun). We can think of light, which is often modelled as particles or waves in physics, as **rays** that travel though space and bounce around. These rays have a colour associated with them, analogous to how we say that light waves have a wavelength. In the real world, eventually, some of this light reaches the camera lens creates an image inside of the camera (which can then be used by a digital sensor, or a roll of film).

![]({{ site.baseurl }}/images/Pinhole_Camera.svg)

<p style="font-size:0.8em; text-align:center">
    A diagram of how the simplest type of camera&mdash;a pinhole camera&mdash;casts an image of the outside world to a two-dimensional film. Pharr, Matt, et al. "A Pinhole Camera," <i>Physically Based Rendering: From Theory to Implementation</i>, pbr-book.org/3ed-2018/Introduction/Pinhole%20Camera.svg.
</p>

As an algorithm, simulating this would look something like:

> - For each light source in our world:
>   - Do the following some number of times (see note below):
>     - Start at the light source and pick a random direction.
>     - Emit a ray in that direction. Simulate the trajectory of the ray, bouncing around the scene.
>     - If the ray reaches our camera, and more precisely, intersects the plane/rectangle which defines our image, then contribute the colour of the ray to the part of the image which it intersects.

**Note:** for each light source we would need to simulate a large number of ray emissions. Consider that some of these rays would also never reach the camera. The number of rays would depend on the amount of time we expose the image to incoming light (known as **shutter speed**). It would also depend on the light source's **emissivity**, that is, how much light it produces.

In theory, this would produce a physically correct image that we would expect from a real camera. However, computers today are not powerful enough to perform such a physically accurate simulation of this universe. 

Instead we must rely on approximation of this process.

## Ray-tracing

Instead of simulating countless rays emitted from light sources and calculating their interactions with every object (which would be computationally expensive), we can trace rays from the camera/image back to the light sources. This reverse approach focuses only on rays that actually contribute to the visible image, making it more efficient.

This approach is not perfectly accurate, but becomes computationally feasibile.

More details about this ray-tracing approach can be found in my post about how [computers achieve photorealism](2024-08-05-ray-tracing.md).

Ray-traced images can take seconds to hours to compute, depending on the scene's complexity and the computational power available. For this reason there is a distinction between online and offline renderers:

## A note on online vs. offline rendering

**Offline rendering** is used in contexts like film production, where quality is prioritized over speed, and extensive computation time is acceptable. On the other hand, **online rendering**, requires near-real-time speeds, as seen in video games, where any kind of ray tracing must be optimized or simplified to maintain interactivity.

## Representation of objects in 3D

So far, we have glossed over how we represent the objects in our scene. Typically, these are defined by **3D models**. A 3D model is a mathematical representation of an object's shape in a digital space, often composed of polygons defined by vertices (points), edges, and faces that form a mesh.

![]({{ site.baseurl }}/images/Dolphin_triangle_mesh.png)

<p style="font-size:0.8em; text-align:center">
    A 3D model of a dolphin. 
    Chrschn. "Dolphin Triangle Mesh," <i>Wikimedia Commons</i>, 27 Mar. 2007, en.wikipedia.org/wiki/File:Dolphin_triangle_mesh.png.
</p>

This mesh can be textured and shaded to simulate the appearance of real-world objects when rendered.

## Rasterization

An alternative approach to ray-tracing is known as rasterization. This technique is primarily used in online rendering contexts such as video games due to its speed. Instead of tracing rays from the camera, rasterization works by projecting 3D objects onto a 2D image. One-by-one, these 2D shapes are then converted into pixels, and the colour of each pixel is filled in (like a colouring book) based on lighting and texture information.

This method is a lot faster computationally because it avoids the complex calculations of millions of ray traces bouncing around, however, it sacrifices some of the visual qualities that we get from a more realistic simulation of light.

More details about the rasterization technique can be found in my post about how [computers render 3D fast](2024-08-05-rasterization.md).

---

In summary, **ray-tracing** and **rasterization** are the two most common techniques used in rendering. I hope this post has sparked your interest in at least one of these techniques! It's also worth noting that these are not the only approaches to rendering. For example, another somewhat popular technique is **ray marching**. The field of computer graphics continues to evolve to this day, as people find creative ways to take advantage of today's computer hardware.
