---
layout: post
title: "Rendering a Storm: Part 1"
description: "Forward vs Deferred Rendering"
category: "Storm"
tags: [game-development, opengl, storm, rendering]
---
{% include JB/setup %}

# Deferred vs Forward Rendering

Storm is a Windows/Linux 2D action platformer game I have been developing for the last 6 months. The game is being built on a custom OpenGL 3.3 rendering engine that I have used as a fun learning project. There are tons of OpenGL documentation, tutorials and guides available online, but the vast majority only explain the basics of rendering a single textured triangle or cube, or simple shaders. When I decided I wanted to write my own rendering engine I found it almost impossible to find reliable discussions of engine architecture online. I want this series of posts to explain the high level concepts behind my rendering engine, hopefully they will be useful to other developers who have moved beyond most online tutorials and are trying to learn a little more about OpenGL.<!--more-->

## Forward Rendering

The standard way to render, or draw, objects with OpenGL is commonly referred to as *Forward Rendering*. If you follow most online tutorials, they will set up your OpenGL rendering process this way: 

For each Object in scene:
 
 1. Perform vertex transformations (Vertex Shader)
 2. Calculate colour of ever visible pixel on object based on object properties and light sources (Fragment Shader)
 3. Repeat for next Object

Forward Rendering often runs into problems when there are variable number of lights in the scene, as the fragment shader must iterate through each light source, and if the number of light sources is not known this can introduce branching (very bad in shaders) or force the use of some possibly ugly conditional shader compilation, or convoluted shader building scheme.

## Enter Deferred Lighting

*Deferred Lighting* (sometimes also known as *Deferred Rendering*) treats light sources, and the areas affected by those sources as geometry, and uses multiple rendering targets (buffers) to accumulate lighting and geometry data, eliminating all branching in shader programs, and greatly improving the efficiency of lighting calculations. The process looks something like this:

 1. Geometry Pass: For each object in Scene
    1. Perform vertex transformations (Geometry Vertex Shader)
    2. Save visible object properties (depth, colour/diffuse/specular, normals) to **Geometry Buffer** (Geometry Fragment Shader)
 2. Lighting Pass: For each light in Scene
    1. Perform vertex transformations lighting area geometry (Lighting Vertex Shader)
    2. Combine lighting information with saved geometry information to calculate final pixel colour (Lighting Fragment Shader)

The key to deferred rendering is the Geometry Buffer, where we save all information about visible objects, and only visible objects. In my next post we'll cover the specific contents of the Geometry Buffer as well as how to create/use one with C++ and Opengl 3.3