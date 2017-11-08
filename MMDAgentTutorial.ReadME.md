# MMDAgent Tutorial

The MMDAgent application was written in Japanese and hence the following are some useful English information about how to use it.

Here is a link to the extensive WiKi in Japanese, on [MMD](https://translate.googleusercontent.com/translate_c?depth=1&hl=en&rurl=translate.google.com&sl=ja&sp=nmt4&tl=en&u=https://www20.atwiki.jp/mmpp/pages/29.html&usg=ALkJrhj8LCJjYjeJSOARyn0bX-Hdw1L9Bw), which I have linked through Google Translate for you.

This document is a summary of the key points.


## Contents
1. Introduction
2. System Requirements
3. How to get MMDAgent
4. MMDAgent Avatar Structure

       {++ ToDo ++}: Directory names and what they are for...

5. Creating your Agent/Avatar: .mdf File
6. Creating the Stage: .fst File

       {++ ToDo ++}: Lighting-Camera


7. Creating Movement & Expressions: .vmd File

       {++ ToDo ++}: Rotation


8. Creating Voice Banks: .ojt File

       {++ ToDo ++}: Voice Regcognition
       {++ ToDo ++}: Speech-Synthesis
       {++ ToDo ++}: Music-Images MP3, Sync and Dance


9. Adding your Models

       {++ ToDo ++}: Plug-ins
       {++ ToDo ++}: Others/Misc


10. Adding Props/Acessories
11. How you can help
12. Useful Tips & Links
13. Credits


## 1. Introduction

This has been reproduced here as lots of information found on forums, whose entries can get pulled down/deleted when members leave.
If it seems incomplete, the chances are it is, as I am still finding more information. This is Unoffical, meaning this is Not by the creators of MMDAgent.


## 2. System Requirements
Well theres not really any listed So most of this is assumed...

Recommendations (Mostly assumed...):
- Processor : 2.00GHz
- Ram : 2GB
- Direct X : Latest recommended
- Japanese Language Pack (JLP): Optional, But HIGHLY recommended!
- MikuMikuDance : Optional, Needed if you want to make Motions
- Notepad : Optional, To create the .ojt,.mdf,.fst Files.
- EditPad Lite : Optional, Alternative to Notepad for people who don't/are unable to have the JPN Language pack installed.

If you do not have the Japanese Language Pack installed/enabled, then you will still be able to use MMDAgent, however, you will come across many problems such as:

- Retarted Skin error:

      To fix this, use a computer with the Japanese Language Pack installed...
      I think (will test on a computer with JPN Language pack installed).

- An error saying it was unable to load textures for a model. (Should be a dark see-through black-ish box with Red Text.): To fix this do either of:

      A. Use a computer with the Japanese Language Pack installed.
      Or
      B. Open the model in PMDEditor/MikuMikuDance and change the texture names to english.

 
## 3. How to get MMDAgent
This guide is based on the assumption that you have already downloaded the latest release of MMDAgent. (It being MMDAgent RC.)
The latest version can be found at their homepage at:

   [MMDAgent Web site](http://www.mmdagent.jp/)

    Instructions:
    Under "MMDAgent version" column, download the link labeled "Binary Package (for 32-bit Windows)".
    (Although it says 32-Bit Windows, it is completely compatable with 64-bit...)

There are also editing tools to support creation and maintenance of the agents, which usually refer to MMDAgent as the full program name [MikuMikuDance](https://learnmmd.com/http:/learnmmd.com/download-the-latest-version-mikumikudance/).


## 4. MMDAgent Avatar Structure

    {++ ToDo ++}: Directory names and what they are for...



## 5. Creating your Agent/Avatar: .mdf File
Lets get started in making your agent. Be prepared (Go get a jug of coffee...), as this is a long read!

So, first you are going to want to open your favourite word editing program. This can be Notepad, Wordpad, MS Word, EditPad Lite or Notepad++. As long as you can type & save "plain text" without any formatting, then all is good.

The .mdf basically consists of all the settings, one line for each setting. All the settings I know are listed below. Possilble values are written underneath each setting, as well as a description for each value. Replace ## with any of the possible values:


### use_cartoon_rendering=##

    e.g. use_cartoon_rendering=true
    - True - black border created around model.
    - False - No border.

If enabled use 'e'(increase) or Shift+'e'(decrease) size of border.

Size of border (If enabled) can also be set via the carton_edge_width setting below.


### use_mmd_like_cartoon=##

    e.g. use_mmd_like_cartoon=True
    - True - Don't know
    - False - Don't Know

I have not noticed a difference between T or F, Tell me if you do, or what an idiot I am and how obvious it really is...


### cartoon_edge_width=##

    e.g. cartoon_edge_width=0.35
    - Any number - Minimum 0, Highest = inifinite?, Bigger Number = Bigger Border
    
    NB: Only works if 'use_cartoon_rendering' is set to true

Use_cartoon_rendering' must me set to true otherwise this setting is useless


### cartoon_edge_step=##

    e.g. cartoon_edge_step=1.2
    - Any number

NB: Only works if 'use_cartoon_rendering' is set to true.
Sets the amount to in/decrease 'cartoon_edge_width' when pressing 'e' and Shift+'e'


### cartoon_edge_selected_color=#1#,#2#,#3#,#4#

    e.g. cartoon_edge_selected_color=1.0,0.0,0.0,1.0
    - Any number - % of RGB colours - Minimum 0.0, Highest 1.0
    #1# = Red
    #2# = Green
    #3# = Blue
    #4# = Unknown?

Colour when a model is selected (Clicked on)


### rendering_rotation=0.0,0.0,0.0

    - Any number - Minimum 0.0, Highest 1.0

Sets the angle for the camera. I think its X,Y,Z...Haven't tested yet.


### rendering_transition=0.0,0.0,0.0

    e.g. rendering_transition=0.0,0.0,0.0
    - Any number

Sets the location of the camera: X-Higher = Move Left, Y-Higher = Move Down, Z-Higher = Move Forward


### rendering_scale=value

    e.g. rendering_scale=1.2
    - Any number

Scale for models/accessories/backgrounds. When an object is created the dimensions are multiplied by the value.

NB: Do not get this confused with Zoom. 


### stage_size=25.0,25.0,40.0

    - Any number

Used to set the dimensions of the stage/room as X, Y, Z. I think, but not sure...


### show_fps=value

    e.g. show_fps=false
    - true
    - false

Decides whether FPS is shown or not.


### fps_position=-2.5,22.0,3.0

    - Any Number

Sets locations of counter. I think its X,Y,Z didn't spend time on it


### window_size=value1,value2

    e.g. window_size=600,600
    - value1 - sets the width of the window
    - value2 - sets the height of the window

Sets the window size.


### top_most=value

    e.g. top_most=true
    - true - Always on top, even when switching to another window
    - false - Will be covered if changed to another window/application.

Sets whether MMDAgent will always be on top.


### full_screen=value

    e.g. full_screen=false
    - true
    - false

Full screen or not.


### log_size=value1,value2

    e.g log_size=80,30
    - Any number, (X-Value,Y-Value)

How big the console log thingy is.

Must be toggled to visable via the 'D' Key.


### log_position=-17.5,3.0,-20.0

    - Any Number

Location of the log, X,Y,Z I think...

Must be toggled to visable via the 'D' Key.


### log_scale=1.0

    - any number

Size of log Multiplied by this value.

Must be toggled to visable via the 'D' Key.


### light_direction=0.5,1.0,0.5,0.0
 
    - Any Numbers

The direction that stage lighting is coming from to illuminate the Agent/Avatar.

This can also be changed manually by Shift+Ctrl+LeftClick then Dragging mouse around the screen.


### light_intensity=0.6

    - Any Number, Highest Value=1,Lowest Value=0

How bright the stage lighting/sun is.


### light_color=1.0,1.0,1.0

    - Any number Between 0(lowest/None) to 1.0(Highest/full)

Colour of the stage lighting/sun, Format is R,G,B


### campus_color=0.0,0.0,0.2

    - Any number Between 0(lowest/None) to 1.0(Highest/full)

Colour of the Background/Void, Format is R,G,B.

Pure White is Surreal and pure Black gives you issues with Agent visibility, so play with colours until they are good for your Agent.


### max_multi_sampling=4

    - Unknown, Number perhaps?

I have no idea, Email me if you do.


### max_multi_sampling_color=4

    - Unknown, Number perhaps?

I have no idea, Email me if you do.


### motion_adjust_frame=0

    - Unknown, Number perhaps?

Have no idea, Email me if you do.


### bullet_fps=120

    - Any Number, Higher Number = More fluid movement of hair/clothes

Sets the fps (frames per second) for anything affected by gravity.


### rotate_step=0.08

    - Any Number, Higher = Faster, Lower = Slower

Controls the speed at which you rotate the camera when using Arrow keys.


### translate_step=0.5

    - Any Number, Higher = Faster, Lower = Slower

Controls the speed at which you move the camera when using - Shift + Arrow Keys


### scale_step=1.05

    - Any Number, Higher = Faster, Lower = Slower

Controls the speed at which Zoom-In and Out, when using the '+' and '-' Keys.


### use_shadow_mapping=false

    - True
    - False

Sets whether shadows are rendered ontop of models.

Can be toggled with the 'X' key.


### shadow_mapping_texture_size=1024

    - Any Number, Higher = Darker, Lower = Lighter

Controls how dark the shadows are.


### shadow_mapping_self_density=1.0

    - Number

I Have no idea what this does. Email me if you do.


### shadow_mapping_floor_density=0.5

    - Number?

I Have no idea what this does. Email me if you do.


### shadow_mapping_light_first=true

    - true?
    - false?

I Have no idea what this does. Email me if you do.


### display_comment_frame=0.0

    - Number?

I Have no idea what this does. Email me if you do.



## 6. Creating the Stage: .fst File
The stage can be created 2 different ways:

#### .fst Method

This method uses an action in the .fst file to create one wall and one floor. The wall and floor consist of images in any of the .xpmd / bmp / png / tga formats.


#### .pmd/x Method

First see 'Adding Props/Acessories' to use .x files.

To use a proper stage just summon it using an action in the .fst file or manually.

    {++ ToDo ++}: Lighting-Camera


## 7. Creating Movement & Expressions: .vmd Files
Movement and Expressions is created with MMD. To make sure the movement will work for real, use the same model you plan to use to create your motions.

Movement/Expression files are .vmd and are created & saved using MMD

Here are some links to Tutorials regarding the use of the MME program, a tool for editing movements and models that the MMDAgent can play.

- [MMD First Steps Make your own motions from scratch](https://learnmmd.com/http:/learnmmd.com/mmd-make-your-own-motions/)
How do I make my models move in MikuMikuDance? Why does my model move so slowly? How do I keep my model from moving until I want it to? 

- [MMD Model Hair Textures Made With . . . IMVU Tutorials?!](https://learnmmd.com/http:/learnmmd.com/mmd-model-hair-textures-made-imvu-tutorials/)
How can I make realistic hair? What should I look up for hair texture tutorials? ...read more 

- [Easily Make Realistic Hair Texture for MMD Models](https://learnmmd.com/http:/learnmmd.com/make-realistic-hair-texture-mmd-models/)
What programs can I use to create realistic hair texture for MMD Models? How can ...read more 

- [Easy Fun MMD Music Video Mahlazer Motion Download "Feel the Sound"](https://learnmmd.com/http:/learnmmd.com/mmd-music-video-feel-the-sound-by-mahlazer/)
How do I make an MMD music video? What's the easiest way to make a ...read more 

- [I'd never eat your brain - The Zombie Song download links](https://learnmmd.com/http:/learnmmd.com/id-never-eat-brain-zombie-song-download-links/)
Today I went looking through YouTube for a new MMD project to share on LearnMMD...

- [Using Texture Transparency hides MMD model problem areas](https://learnmmd.com/http:/learnmmd.com/using-texture-transparency-hides-mmd-model-problem-areas/)
How can texture transparency make my model look better? Is there a shortcut to making... 

- [Position stage near MMD coordinate axis center-line](https://learnmmd.com/http:/learnmmd.com/position-stage-near-coordinate-axis-center-line/)
How can I move the coordinate axis center-line into the part of the stage where ...read more 

    {++ ToDo ++}: Rotation


## 8. Creating Voice Banks: .ojt File
If you want to actually make your own voice bank, I'm afraid I don't know how, The program used for voice synthsizing is [jTalk](http://open-jtalk.sourceforge.net/) for Linux. However you are able to manipulate the voice using the .ojt file. If you manage to create a nice sounding .ojt file post here to share (If you want to).

    {++ ToDo ++}: Voice Regcognition
    {++ ToDo ++}: Speech-Synthesis
    {++ ToDo ++}: Music-Images MP3, Sync and Dance


## 9. Adding your Models
Your going to want to keep all your models in a folder to keep it organized, Also, Don't forget that certain models may need extra textures such as the miku.pmd from MMD requires a eye.bmp in the same folder. Also don't forget if the texture names are in Japanese and you don't have the Japanese language pack installed you will have problems, Scroll up to '4. System Requirements' to see what to do to fix it.

I won't be listing how to create models as that does not apply to MMDAgent and I have still not found an editor in English that works! I am currently relying on the greater worldly experience and skills of colleagues on the Deviant Art forum.

    {++ ToDo ++}: Plug-ins
    {++ ToDo ++}: Others/Misc


## 10. Adding Props/Acessories
Props and Acessories. MMDAgent only (I think) accepts .pmd files as accessories, If you have an .x file that you want to use, you are going to have to open up PMDeditor and open the .x file, then Save it as a .pmd file. From there just use a ModelAdd event in your .fst or by command to bring your accessory onto the stage.


## 11. How you can help
I need help. Lots of help. This is going to be big and there is no way I can get all the skills needed to complete this project in a reasonable timeframe.
Please feel free to send me any info i missed, so i can add to this guide, especially if you want to share the mysteries of editing PMD files :).

## 12. Useful Tips & Links
These are the real experts in MMDAgent:

#### VPVP Wiki
The place for MMD resources, Although its in Japanese Google Translate does a good enough job and using it you should be able to navigate around the site.

#### MMDAgent
The homepage to this wonderful avatar program. 

#### VocaloidOtaku
A good forum to talk about Vocaloids and what not. Also has a section for MikuMikuDance.

#### Youtube
Youtube, if you don't know what it is...Now you do, YouTube, A Big giant Video hosting site with like what, a billion videos? You should be able to find tutorials or MMD resources on youtube. You can also find Mole-Chan on Youtube.

#### Nico Nico Douga
Nico Nico Douga, Pretty much the japanese version of youtube. Filled with many videos of anime/Vocaloid and other Japanese culture. Your going to need an account to watch videos (registration is free) as well as a grasp on kanji if you going to wanna use the search.

#### EditPadPro
A extremely useful app for people who don't have the Japanese language pack installed. EditPadPro can open files which have messed up chars(All those fs) and convert it into proper Japanese.
To do so after opening the files, Menu->Convert->Text encoding, Set it to 'Interpret the original Data' and set the new encoding to 'Windows 932: Japanese SHIFT-JIS'

#### Know your Name in Japanese
Useful for when you want your Agent to say your name.

#### Katakana to English Converter
Another useful site for turning english into katakana for whatever reason you'd want, Best to do word by word.


## 13. Credits
Thanks for reading, hope some parts are useful to you.

Special thanks to:
 - Midget & Mole-Chan : Who started the first version of this document.
 - MMDAgents Creators : For creating MMDAgent.
 - Yu Higuchi : For creating MikuMikuDance.

