---
layout: post
title: "Rendering a Storm: Part 1"
description: "Component overview of my rendering engine."
category: "Storm"
tags: [game-development, opengl, storm, rendering]
---
{% include JB/setup %}

Storm is my baby, its a 2D action-adventure platforming game with a few rather unusual gameplay elements. This post isn't about gameplay though, its about rendering stuff. 

<!--more-->

There are a couple of primitives that the rendering engine operates on:

 * Mesh2D: An immutable object that is essentially just wrapper around a list of 2D coordinates specifying a convex object.
 * Images: A simple wrapper around a large array of <code>unsigned char</code> that make up a simple RGBA formatted image. Images are immutable, having a data accessor returning <code>const unsigned char*</code>.
 * Textures: Combination of a pointer to an Image, and a Mesh2D specifying a region of that image.
 * Materials: Combination of 3 Textures, one each for a colour (albedo) texture, a normal map texture and a specular map texture.
 * Lights: A single point specifying the light source, a Mesh2D specifying it's area of influence, and data specifying light intensity, falloff and colour.
 * Directional Lights: A single point specifying location of light source, and data specifying light intensity, falloff and colour.
 * Sprites: Combination of Mesh2D and a material, the basic renderable object.

As a deferred rendering engine, there are 2 primary rendering stages (plus post-processing).

 1. Geometry Pass: Render all visible Sprites, rendering each element of their material to a different texture attachment of the Geometry buffer.
 2. Lighting Pass: For the lighting pass, blending is enabled and a single quad the size of the viewport is rendered, sampling the texture attachments of the geometry buffer.
    1. Render Directional Lights: Render all directional lights, using a single quad the size of the viewport as its area of influence.
    2. Render Point Lights: For each point light in scene, render their area of influence.

