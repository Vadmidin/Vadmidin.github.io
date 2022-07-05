---
title: "Project #1: Paper2D game prototype"
image: 
  path: /images/project-01-paper2D-game-prototype-2048x512.jpg
  thumbnail: /images/project-01-paper2D-game-prototype-512x256.jpg
  caption: # "Photo from [Pexels](https://www.pexels.com)"
---

# A combination of 2D and 3D

## Overview
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_01.mp4" type="video/mp4" />
   </video>
</div>
<br>
This is a showcase of a small set of features for a prototype of a (most likely) mobile game. The game is a combination of a classic Dungeon Crawler and Fruit Ninja.

## Feature #1: Custom camera behavior
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_06.mp4" type="video/mp4" />
   </video>
</div>
<br>
One of the more important game features is the camera itself. An example that demonstrates the idea is, that the levels are made up of different rooms and the player could be initially viewing the room from a certain angle. But later as the player progresses, due to some event, the perspective shifts, and the player is able to return to that very same room. However, they would be able to see things they previously couldn’t, but, in fact, were there all along.

You may notice that during the camera rotation, the sprites (character and props) in the level all also rotate to face the camera. This is done via a vertex shader, and because of this, the effect would be applied to each CameraComponent individually. So, theoretically, since we don't actually change the rotation of the Actor or SpriteComponent, this effect should work in a multiplayer environment. Imagine if two cameras are looking at the same sprite from two different perspectives.

## Feature #2: Mesh Component occlusion fading
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_07.mp4" type="video/mp4" />
   </video>
</div>
<br>
Since both Paper2D Sprites/Flipbooks and regular 3D StaticMeshComponents inherit from MeshComponent, they both use a common/reusable system of interfaces and custom state management ActorComponents that are called when there is something between the player character and the camera. 

We are constantly firing a capsule trace and when something is hit we tell it to fade if it implements the "Fadeable" interface.

> Sidenote: All of the walls, floors, ceilings are made up of instanced blocks and for the fading effect we use a masked Material and apply a custom dithering pattern and animate it via a Timeline and FloatCurve. Since UE Nanite doesn’t support Masked Materials (yet! Maybe in UE 5.1), the blocks' static meshes have 2 versions of them: One with Nanite, one - without. So normally all blocks are Nanite, but when we need them to do the fade out/in effect, we first replace them with the Non-nanite blocks.

### Room creation:
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_05.mp4" type="video/mp4" />
   </video>
</div>
<br>
Right now there isn't a good way implemented for room creation. Each wall, floor, ceiling piece is just a StaticMeshActor blueprint with many StaticMeshComponents added. For a small demo this is fine, but for a larger scale project the toolset should definitely be created. Perhaps some kind of spline system could work.

## Feature #3: Character "flipping" effect
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_02.mp4" type="video/mp4" />
   </video>
</div>
<br>
Expanding on the vertex shader, allowed me to create this "flipping" effect of the character.
Like you would flip a page in a book. Using Custom Primitive Data on the Mesh Component, a Timeline and Float Curve it is possible to animate and set the flipping amount and flipping speed.

## Feature #4: Fruit Ninja-esque gameplay
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_03.mp4" type="video/mp4" />
   </video>
</div>
<br>

### Debug view:
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_04.mp4" type="video/mp4" />
   </video>
</div>
<br>

