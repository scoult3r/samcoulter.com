---
layout: post
title: "Rendering a Storm: Part 1"
description: "Component overview of my rendering engine."
category: "Storm"
tags: [game-development, opengl, storm, rendering]
---
{% include JB/setup %}

Storm is my baby, its a 2D action-adventure platforming game with a few rather unusual gameplay elements. This post isn't about gameplay though, its about rendering stuff. 

I want this post to serve as an architectural overview of the rendering back-end of Storm. When I first set out designing and implementing a renderer, I found loads of resources on how to use OpenGL, how to achieve specific graphical effects, and lots of game design patterns, but no real overviews of the architecture of a game renderer as a whole. I want this post to serve as ___<!--more-->

## Overview

For Storm, I am implementing (in OpenGL 3.3) a 2D **Deferred Lighting** renderer. The renderer performs at least two passes in order to render the screen, one **Geometry Pass** and one **Lighting Pass**. The geometry pass renders all object information to appropriate buffers on the graphics card, and then the lighting pass combines that information with information about all lights in the scene to draw the final image. Under some conditions a final post-processing pass may occur, where the rendering engine grey scales the image, or adds some other post-processing effect.

Deferred Lighting (aka Deferred Rendering) has a number of advantages over traditional **Forward Rendering**, but in order to talk about them we first need a general overview of the forward rendering pipeline. 

Forward rendering is simple to understand: For every object in the scene:

 1. If object is not visible (outside of the viewing region), abort the draw
 2. Render every pixel required for the object, taking into account the properties of the object material, the lights in the scene, and the depth of the object.

Forward rendering can run into trouble with variable numbers of light sources in a scene. 



## Rendering Primitives

There are a couple of primitives that the rendering engine operates on:

 * Mesh2D: An immutable object that is essentially just wrapper around a list of 2D coordinates specifying a convex object.
 * Images: A simple wrapper around a large array of <code>unsigned char</code> that make up a simple RGBA formatted image. Images are immutable, having a data accessor returning <code>const unsigned char*</code>.
 * Textures: Combination of a pointer to an Image, and a Mesh2D specifying a region of that image.
 * Materials: Combination of 3 Textures, one each for a colour (albedo) texture, a normal map texture and a specular map texture.
 * Lights: A single point specifying the light source, a Mesh2D specifying it's area of influence, and data specifying light intensity, falloff and colour.
 * Directional Lights: A single point specifying location of light source, and data specifying light intensity, falloff and colour.
 * Sprites: Combination of Mesh2D and a material, the basic render-able object.

As a deferred rendering engine, there are 2 primary rendering stages (plus post-processing).

 1. Geometry Pass: Render all visible Sprites, rendering each element of their material to a different texture attachment of the Geometry buffer.
 2. Lighting Pass: For the lighting pass, blending is enabled and a single quad the size of the view port is rendered, sampling the texture attachments of the geometry buffer.
    1. Render Directional Lights: Render all directional lights, using a single quad the size of the view port as its area of influence.
    2. Render Point Lights: For each point light in scene, render their area of influence.

