# Hit Saber

## DEMO

<div align="center">
    <a href="https://youtu.be/aUlHyvz5wyc?si=x3WUbfo8tZx4KefE">
        <img src="/ReadmeAssets/Thumbnail 1.png">
    </a>
</div>

## Phase 1: Music Selection and Conceptualization

<!-- Choose a music track and brainstorm initial concepts for your immersive VR music experience. -->

Inspired of following two reference, I decided to design the VR rhythm game where user can slice the cube which flies toward to oneself. The one can have immersive experience of enjoying the song while slashing each cubes to the rhythm.

<blockquote>
"Believer" is a song by American pop rock band Imagine Dragons.
</blockquote>

<div align="right">
    <a href="https://en.wikipedia.org/wiki/Believer_%28Imagine_Dragons_song%29">https://en.wikipedia.org/wiki/Believer_%28Imagine_Dragons_song%29</a>
</div>

<br>

<p align="center">
    <img src="/ReadmeAssets/Believer.jpg">
</p>

<blockquote>
Beat Saber is a VR rhythm game where you slash the beats of adrenaline-pumping music as they fly towards you, surrounded by a futuristic world.
</blockquote>

<div align="right">
    <a href="https://beatsaber.com/">https://beatsaber.com/</a>
</div>

<br>

<p align="center">
    <img src="/ReadmeAssets/Beat Saber.jpg">
</p>

https://store.steampowered.com/app/620980/Beat_Saber/

## Phase 2: Storyboarding and World Building

<!-- Craft storyboards that outline the narrative, seamlessly fusing visual and auditory elements. Begin constructing the VR environment within Unreal Engine. -->

The BPM (Beats Per Minute) of the song "Beliver - Imagine Dragons" is 125. Therefore, We have to set the amount of delay as multiple of 60/125 seconds.

https://songbpm.com/@imagine-dragons/believer

We will build the world refer to the gameplay screenshot of the game "Beat Saber". The game will start at the empty level only with two lightsabers which are turned off. The song starts and the cubes begin to fly towards the user if and only if the user grab and turn on the two lightsabers.

<div align="center">
    <img src="/ReadmeAssets/Beat Saber 1.jpg" style="width: 20%">
    <img src="/ReadmeAssets/Beat Saber 2.jpg" style="width: 20%">
    <img src="/ReadmeAssets/Beat Saber 3.jpg" style="width: 20%">
    <img src="/ReadmeAssets/Beat Saber 4.jpg" style="width: 20%">
</div>

## Phase 3: VR Development

<!-- Continue to Build and fine-tune your VR music experience, emphasizing user interactions and emotional resonance. -->

### 1. Cube

#### 1) Assets

- ColorEnumeration
- CubeBlueprint
- CubeMaterial
- CubeMaterialBlack
- CubeMaterialBlue
- CubeMaterialRed
- CubeMesh
- DirectionEnumeration
- DirectionMaterial

#### 2) Mesh and Material

First, we have to create the mesh of cube by blender. Create rounded cube, manipulate the value of radius and complexity, and export it. We can use the mesh of cube created in blender by importing it in unreal engine as "CubeMesh".

Second, let's create the material of cube. Set suitable value of metalic and roughness, and create two parameter named "Color" and "Glow". They will decide the base color and degree of glowness of the material. Based on the default material named "CubeMaterial", we can create material instances named "CubeMaterialBlack", "CubeMaterialBlue", and "CubeMaterialRed". Manipulate each parameter suitably for each material instances.

#### 3) Blueprint

Third, we have initialize the cube whenever it is created by the spawner. "Initialize" function will create the cuboid or cylinder according to the direction of cube, and set the material of the cube according to the color of the cube.

Fourth, let's make the cube to fly towards to the user. Subtract specific value from the x location of the actor every tick. We can multiply the delta seconds value in order to translate the actor regardless of the frequency that the event tick is called.

Finally, we'll create the "slice" function that slices the procedure mesh of cube in respect to the given plane position and plane normal vector. plane position and plane normal vector is calculated by blade position, blade center position, and cube location vectors. Plane position is as same as the cube location. Plane normal vector approximately equals to cross product of (cube location - blade center position) and (blade center position - blade position) since the vector that is perpendicular to two vectors can be calculated by the cross product of two vectors.

<p align="center">
    <img src="/ReadmeAssets/Cross Product.jpg" style="width: 50%">
</p>

Whenever the "slice function" is called, there are some variety of following functions to be executed.

1. Play haptic event to the according controller.
2. Add Score to the score blueprint.
3. Simulate physics, enable gravity, add impulse to the two sliced cubes.
4. Shine the background structures.
5. Destory the two sliced cubes after some delay.

### 2. Lane and Spawner

#### 1) Assets

- LaneBlueprint
- SpawnerBlueprint

#### 2) Blueprint

First, we have to implement "SpawnCube" function in the lane blueprint. It spawns a single cube at the location of itself and initializes the cube with given direction and color.

Second, implement "SpawnCubeAt" function in the spawner blueprint. the spawner consists of tweleve lanes, three rows and four lanes per row. the function gets index, direction, and color as parameter, and executes "SpawnCube" function of the lane according to the given index.

Third, make a preset of spawning cubes according to the BPM of the song. Since the BPM of the song is 125, we will delay 2 \* (60 / 125) seconds between each cube spawn event. We may make some arbitary fancy preset of spawning cubes, but in this project I choose to repetedly call the "SpawnCubeAt" function with random parameters with some correction. Correction prevents too difficult cube spawning consecutively.

### 3. Lightsaber

#### 1) Assets

- BladeMaterial
- BladeMaterialBlack
- BladeMaterialBlue
- BladeMaterialRed
- LightEnumeration
- LightsaberBlueBlueprint
- LightsaberRedBlueprint

#### 2) Mesh and Material

First, we have to create the mesh of blade. Create cylinder, manipulate the value of radius and length. Add the point light overlapping to the cylinder, manipulate the vlaue of source radius and source length so that we can have the effect of light is emmersing from the blade.

Second, let's create the material of blade. Create four parameter named "Color", "Glow", "Exponentln", and "BaseReflectFractionln". They will decide the base color, degree of glowness, and parameter of fresnel effect of the material. Based on the default material named "BladeMaterial", we can create material instances named "BladeMaterialBlack", "BladeMaterialBlue", and "BladeMaterialRed". Manipulate each parameter suitably for each material instances.

#### 3) Blueprint

Third, we have to make the lightsaber grabbable and turnable. Add grabcomponent to static mesh handle and implement "TurnOn" and "TurnOff" function, each of which turns on and turns off the static mesh blade with some ease out dissolving effect using "FInterp To" funciton.

Finally, change the collision preset of the blade to "OverlapAll", and every time the blade collider starts to overlap with the cube, call the slice function of the cube with current blade position and blade center position parameters. I've tried countless times with "OnComponentHit", not "OnComponentBeginOverlap". However, every time the user grabs the given actor, "VRPawn" blueprint attaches the child object (lightsaber) to the parent object (hand controller), so that the collider of the child is deactivated while it is attached to the parent until grab ends.

### 4. Floor and Light

#### 1) Assets

- FloorMaterial
- FogBlueprint
- LightBlueprint
- LightEnumeration
- RailMaterial
- TempBlueprint

#### 2) Blueprint

Light blueprint changes the color of themselves respect to the combo status of the user. It has two functions, named "StartShine" and "EndShine". Whenever the slice function of the cube is called, "StartShine" function is called and every single light blueprint in the level starts to shine as the color of the sliced cube. They keep shine and change color until the user miss the cube. If the user miss the cube, "EndShine" function is called and every single light blueprint in the level ends to shine and turns into black.

### 5. Score

#### 1) Assets

- ScoreBlueprint

#### 2) Blueprint

There is only one custom event in the score blueprint, which is "AddScore". It is called whenever the slice function of the cube is called, and it simply adds the score by 1 and apply the result to the user interface.

## Phase 4: Testing and Refinement

<!-- Test the VR project, gather feedback from peers, and apply refinements to ensure optimal audience engagement. -->

<a href="https://youtu.be/1bJSK-3MMjY?si=UxJjdJHugrcuiEOT">Testing and Refinement 1</a><br>
<a href="https://youtu.be/WyRjtOE3s9k?si=NGZiQilPCQFB1ERG">Testing and Refinement 2</a><br>
<a href="https://youtu.be/ULakozg99vY?si=z6Mp2sO24LvQDIU3">Testing and Refinement 3</a><br>
<a href="https://youtu.be/aUlHyvz5wyc?si=W6TUjX6S7xGxvNi_">Testing and Refinement 4</a><br>

## Phase 5: Demo

<!-- Demo your project to the class, give and receive critical feedback to your peers. -->

<div align="center">
    <a href="https://youtu.be/aUlHyvz5wyc?si=x3WUbfo8tZx4KefE">
        <img src="/ReadmeAssets/Thumbnail 1.png">
    </a>
</div>

## Phase 6: Documentation

### 1. How to Play

#### 1) Hardware Requirement

- Oculus Quest 2
- CPU: Intel i5-4590 / AMD Ryzen 5 1500x
- GPU: NVIDIA GTX 1050 Ti / AMD Radeon RX 470
- RAM: 8GB
- OS: Windows 10

#### 2) Software Requirement

- Oculus App
- Steam
- Steam VR
- Unreal Engine 5.3

#### 3) Instruction

1. git clone https://github.com/hoosong0235/Hit-Saber.git
2. Enjoy :)

#### 4) Tutorial

https://www.meta.com/ko-kr/help/quest/articles/headsets-and-accessories/oculus-link/connect-link-with-quest-2/  
https://www.youtube.com/watch?v=Z4sClxhgsxk&t=359s

### 2. Reference

#### 1) Beat Saber

https://beatsaber.com/  
https://store.steampowered.com/app/620980/Beat_Saber/

#### 2) Video

https://www.youtube.com/watch?v=Dzp4U94vIVY  
https://www.youtube.com/watch?v=yIo1nF-BVqk  
https://www.youtube.com/watch?v=0wKWoAFoqoo  
https://www.youtube.com/watch?v=ptEGTxpZ1_M  
https://www.youtube.com/watch?v=2I65tb73_wo  
https://www.youtube.com/watch?v=EZwluOWmXTs&list=PL2QnxVoLRx4h4iye5VQq4RAaYR_ud6uoG  
https://www.youtube.com/watch?v=YnPjL_jIjgk&list=PL2QnxVoLRx4iWibY5ZfuYi3E3CTifIDJD  
https://www.youtube.com/watch?v=gh4k0Q1Pl7E

#### 3) Article

https://en.wikipedia.org/wiki/Believer_%28Imagine_Dragons_song%29  
https://songbpm.com/@imagine-dragons/believer
