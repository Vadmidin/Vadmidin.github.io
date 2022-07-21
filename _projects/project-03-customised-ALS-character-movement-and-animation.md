---
title: "Project #3: Customised ALS character movement and animation"
image: 
  path: /images/project-03-customised-ALS-character-movement-and-animation-2048x512.jpg
  thumbnail: /images/project-03-customised-ALS-character-movement-and-animation-512x256.jpg
  caption: # "Photo from [Pexels](https://www.pexels.com)"
---

# *A workflow for generating models, rigging and creating reusable animation compatible with the UE mannequin skeleton*

## Overview
For study and learning purposes, I have spent time with the community version of the [Advanced Locomotion System (ALS)](https://github.com/dyanikoglu/ALS-Community), figuring out a way to create a customised workflow for animating characters.

<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_11.mp4" type="video/mp4" />
   </video>
</div>
<br>

### Setup
Ignoring the funky looking character model, the rig for this character is a [Rigify](https://docs.blender.org/manual/en/2.81/addons/rigging/rigify.html) rig, but at the same time the skeleton used is compatible with the Unreal Engine 4 mannequin skeleton. This means that not all animations need to be created by hand (though, in this case, they are), because they can be purchased from the marketplace and simply be used in Animation Blueprints right away.

### Nonlinear animation
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_10.mp4" type="video/mp4" />
   </video>
</div>
<br>
Instead of creating each animation for each movement direction from scratch, we use nonlinear animation. This means that all we need to do is create a single animation (run forward, for example) and then only make additive poses for each direction. It even works for things like a crouch walking. All you need to do is create a crouched additive pose and all the directional animations also work. After that we can bake all of them down separetely and export them to the engine and use them in animation blueprints.

### In engine
<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_12.mp4" type="video/mp4" />
   </video>
</div>
<br>
Following the C++ implementation of ALS community closely and exporting and creating the animation blueprints similar to how they are made in ALS, allowed me to also replicate character movement states that drive the animations.

I have customised the ALS community project to fit in with a more "True First Person" experience. The character blueprints allow for the characters first person torso and arms to be visible.

<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_13.mp4" type="video/mp4" />
   </video>
</div>
<br>
Additionally, I've tinkered around with a horizontal+ implementation for camera components, a separate field of view slider for the characters first person view model and forward rendering via a vertex shader, such that the first person view models are always rendered on top of everything, to prevent them from clipping inside of walls.

<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src="{{ site.baseurl }}/videos/Vadmidin.github.io_14.mp4" type="video/mp4" />
   </video>
</div>
<br>
I have also implemented a Horizontal+ aspect ratio for camera components, to allow for ultra wide monitor support. As you can see changing the viewport size always adjusts the scene in a way that we will never gain or lose any vertical information, but will in turn expand our viewing range horizontally instead. This is the same system that Call of Duty®: Modern Warfare (2019) uses.

Not much more to say about this project. By now I feel like there are better ways to implement animation blending and state management systems as of Unreal Engine 5 using the new control rig with full body IK.