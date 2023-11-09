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

### 2. Lane and Spawner

#### 1) Assets

- LaneBlueprint
- SpawnerBlueprint

### 3. Lightsaber

#### 1) Assets

- LightEnumeration
- LightsaberBlueBlueprint
- LightsaberRedBlueprint

### 4. Floor and Light

#### 1) Assets

- FloorMaterial
- FogBlueprint
- LightBlueprint
- LightEnumeration
- RailMaterial
- TempBlueprint

### 5. Score

#### 1) Assets

- ScoreBlueprint

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
