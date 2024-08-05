---
layout: post
title: How Do Computers Render 3D?
---

3D computer generated images are everywhere; video games, film and television, engineering, research and education, and so much more. How are computers able to produce these kinds of images?

![](animation01-1280x720.jpg)
<!-- https://www.blender.org/ -->

In essence, the goal is to simulate a camera's view into a virtual 3D world, similar to how a camera in the real world would be able to produce an image.

# Simulating a camera

At first, the solution to this problem might seem straightforward. We could try to simulate the way a camera works in the real world. That is, we would use our understanding of the physical world, to simulate the emission of light from light sources in our world (for example, the sun). We can think of light, which is often modelled as particles or waves in physics, as *rays* that travel though space and bounce around. These rays have a colour associated with them, analagous to how we say that light waves have a wavelength. In the real world, eventually, some of this light reaches the camera lens creates an image inside of the camera (which can then be used by a digital sensor, or a roll of film).

As an algorithm, simulating this would look something like:

> - For each light source in our world:
>   - Do the following some number of times (see note below):
>     - Start at the light source and pick a random direction.
>     - Emit a ray in that direction. Simulate the trajectory of the ray, bouncing around the scene.
>     - If the ray reaches our camera, and more precisely, intersects the plane/rectangle which defines our image, then contribute the colour of the ray to the part of the image which it intersects.

**Note:** for each light source we would need to simulate a large number of ray emissions. Consider that some of these rays would also never reach the camera. The number of rays would depend on the amount of time we expose the image to incoming light (known as *shutter speed*). It would also depend on the light source's *emissivity*, that is, how much light it produces.

In theory, this would produce a physically correct image that we would expect from a real camera. However, computers today are not powerful enough to perform such a physically accurate simulation of this universe. 

<!-- Add note on how there would be an astronomical amount of work to do -->

Instead we must rely on approximation of this process.

# Ray-tracing


![](Ray_trace_diagram.png)
<!-- https://commons.wikimedia.org/wiki/File:Ray_trace_diagram.svg -->

- A note on ray-tracing

## Online vs. offline rendering

# Representation of objects in 3D

# Rasterization
- Converting points from 3D to 2D: perspective
- How we simulate camera movements

<!-- Add some useful links for learning more about making a 3D renderer and further reading -->

<!-- # Conclusion

If the physically accurate simulation of cameras interested you, you might enjoy my other article on [how computers simulate realistic motion of objects](simulating-physics.md). -->