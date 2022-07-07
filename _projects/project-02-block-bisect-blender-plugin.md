---
title: "Project #2: Block bisect blender plugin"
image: 
  path: /images/project-02-block-bisect-blender-plugin-2048x512.jpg
  thumbnail: /images/project-02-block-bisect-blender-plugin-512x256.jpg
  caption: # "Photo from [Pexels](https://www.pexels.com)"
---

# *A blender plugin for generating all block types for both convex and concave room creation*

## Overview

This is a blender plugin I created to aid me in the generation of not only simple block shapes, but also diagonal and corner pieces for use in games, with the click of a single button. This is a bit of a prelude to the creation of the Paper2D game prototype, and since this is mostly to do with Python and Blender, I figured it might be better to separate it out as a standalone project.

### Block generation:
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_08.mp4" type="video/mp4" />
   </video>
</div>
<br>

Since the requirement for the games' style are a bit specific, mainly because of the wall fading mechanics, I needed a way to quickly generate all the pieces that make up a room for e.g. a dungeon environment.

### Room creation in engine from blocks:
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_05.mp4" type="video/mp4" />
   </video>
</div>
<br>
Right now there isn't a good way implemented for room creation in the engine itself. Each wall, floor, ceiling piece is just a StaticMeshActor blueprint with many StaticMeshComponents added. For a small demo this is fine, but for a larger scale project a toolset should definitely be created. Perhaps some kind of spline system could work.