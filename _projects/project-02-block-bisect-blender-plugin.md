---
title: "Project #2: Block bisect blender plugin"
image: 
  path: /images/project-02-block-bisect-blender-plugin-2048x512.jpg
  thumbnail: /images/project-02-block-bisect-blender-plugin-512x256.jpg
  caption: # "Photo from [Pexels](https://www.pexels.com)"
---

# *A blender plugin for generating all block types for both convex and concave room creation*

## Overview
This is a blender plugin I created to aid me in the generation of not only simple block shapes, but also diagonal and corner pieces for use in games, with the click of a single button. This is a bit of a prelude to the creation of the Paper2D game prototype, but since this has more to do with Python and Blender, I figured it might be better to separate it out as a standalone project. After all, the resulting block models are modular and could be used for a bunch of different applications, e.g. a Wave Function Collapse algorithm, for procedural level generation later on.

### Block creation summary
Software used:
1. MagicaVoxel (for creating a 3D voxel mesh from a tile-able 2D pixel art texture, with a custom color palette)
2. VoxEdit (for much better exported mesh topology)
3. Blender (using my custom plugin for generating minimum required block pieces) <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop"><source src="{{ site.baseurl }}/videos/Vadmidin.github.io_08.mp4" type="video/mp4" /></video>

### Block generation
Since the requirement for the games' style are a bit specific, mainly because of the wall fading mechanics, I needed a way to quickly generate all the pieces that make up a room for e.g. a dungeon block environment.

In summary, the steps taken for each block piece are:
1. Bisect the original block.
![alt text](/images/project-02-block-bisect-blender-plugin-1280x1024.jpg "Bisected original block")
2. Generate a simple plane mesh and bake a texture onto it from the appropriate projection axis.
![alt text](/images/project-02-block-bisect-blender-plugin-1280x1024-02.jpg "Diagonal plane mesh")
3. From the previous bisection cross-section, create a small "cutter" piece, and using the boolean modifier, create holes at the edges of the plane.
![alt text](/images/project-02-block-bisect-blender-plugin-1536x1024.jpg "Cutter piece")
4. Join both the bisected mesh and the plane together. <video style="display:block; width:100%; height:auto;" autoplay controls loop="loop"><source src="{{ site.baseurl }}/videos/Vadmidin.github.io_09.mp4" type="video/mp4" /></video>

And after generating each piece, it results in a set of meshes that all fit together perfectly, are tile-able and are possible to mix and match with other block types, to create smooth transitions from biome to biome.
![alt text](/images/project-02-block-bisect-blender-plugin-1024x1024.jpg "After separating each piece")

Overall, with this workflow creating more and more block types for an artist, in the future, will be a lot faster and easier.

### Room creation in engine from blocks
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_05.mp4" type="video/mp4" />
   </video>
</div>
<br>
Right now there isn't a good way implemented for room creation in the engine itself. Each wall, floor, ceiling piece is just a StaticMeshActor blueprint with many StaticMeshComponents added. For a small demo this is fine, but for a larger scale project a toolset should definitely be created. Perhaps some kind of spline system could work.

Also, the performance impact is not too high. I would guess it's enough to be able to run on a mobile device, but have not tested. Together with Unreal Engine 5 Nanite and Dynamic Mesh Instancing it is possible to have huge amounts of these blocks on screen at once, and maintain high frame rate. For each new block type (with its own set of pieces) the draw call count would increase only by 17, due to some blocks requiring multiple materials, to avoid a more complicated workflow, that involves baking block faces down to a single texture. Improvements are definitely possible.