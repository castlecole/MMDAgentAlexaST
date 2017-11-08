# Snowboy - Alexa_MMDAgent for Raspberry Pi

This is a safe copy of the still developing project by Jianming Liu (https://github.com/jianmliu/Alexa_MMDAgent). Please refer to AlexaPi project to complete the "example_creds.py" and rename it to "creds.py". Only Snowboy is supported as the wake up word, but you could custom yours.


## Things used in this project 

### Hardware components:
- Raspberry Pi 3 Model B
- 3.5 TFT LCD for Raspberry Pi
- USB Microphone

### Software apps and online services:
- MMDAgent 1.6.1


## Story 
I have been thinking that it is a little dumb (even creepy) to just talk to a black speaker. I believe that the communication will be much more natural if Alexa has an avatar. Therefore, I have been working to bring Alexa alive, right in front of you with an Avatar. After days of work, eventually I figure out a framework, which is very flexible and open to further development. 
The key words are MMDAgent, Mikumikudance, snowboy, Alexa AVS, Alexa ASK, and Raspberry Pi. I'd like to explain how it works in the following:
- MMDAgent is a software package with voice recognition platform (Julius), voice synthesis(HTS), 3D character display and voice interaction control. However, it only supports Japanese. But thanks to the flexibility of MMDAgent, I eventually manged to implement Alexa as the brain of MMDAgent.
- Due to the flexibility of MMDAgent, it is possible to write your own plugins to extend its functions. To make it even easier, Python could be supported with the help of SubProcess plugin. This is especially important considering we already have AlexaPi.
- Mikumikudance, commonly abbreviated to MMD, is a freeware animation program that lets users animate and create 3D animation movies, originally produced for the Vocaloid character Hatsune Miku. MMD format is supported by MMDAgent and there are many resources available online in the MMD community including motion data and new characters etc.
- Snowboy is a hotword detection engine, which is used to wake up Alexa. The porting of Snowboy and Alexa AVS as MMDAgent plugins is based on the AlexaPi project. 
- Finally but not least, everything currently runs on a Raspberry Pi. The experimental OpenGL driver which uses the GPU to provide hardware acceleration should be enabled in order to achieve satisfactory performance. 

There are a lot of possibilities with the help of specially designed Alexa skills, which could take advantage of 3D character. One obvious example is that Alexa could dance with the music now, and she could also change her clothes based on the weather and the room temperature. Do you want to see your Alexa dressing in Bikini? It's time to shop some clothes for your Alexa today!


## Setting up of Raspberry Pi 2 or 3
1 or zero is not recommended due to limited CPU and GPU performance.
Install raspbian using NOOBS from a brand new TF card and RPi.

Format your card using: https://www.sdcard.org/downloads/formatter_4/
Remember to turn format size adjustment on.

Download the NOOBS from: https://www.raspberrypi.org/downloads/noobs/

Extract to you TF card and more details you could refer:
    https://www.raspberrypi.org/documentation/installation/sdxc_formatting.md 
    https://www.raspberrypi.org/help/videos/

Connect keyboard, mouse and HDMI monitor to RPi, Ethernet is not necessary if you have WiFi. Turn on your RPi and set up WiFi if necessary, then choose to install Raspbian.
Enable GPU hardware acceleration for OpenGL using:
- sudo raspi-config
- choose advanced options, GL driver and then yes

Meanwhile, you also need to adjust the GPU memory to 256 Mb in Menu->Raspberry Pi Configuration->Performance
sudo apt-get install mesa-utils
use glxgears to test the FPS, it should be around 60FPS instead of previous 25FPS

Download and compile the MMDAgent 1.6.1 wiget: http://sourceforge.net/projects/mmdagent/files/MMDAgent/MMDAgent-1.6.1/MMDAgent-1.6.1.zip/download -O MMDAgent-1.6.1.zip

unzip MMDAgent-1.6.1.zip
cd MMDAgent-1.6.1

Install the following packages in order to compile:
- sudo apt-get install libx11-dev mesa-common-dev libglu1-mesa-dev libxrandr-dev libasound2-dev

Download the SubProcess plugin to support Python script git clone: https://github.com/jianmliu/Plugin_SubProcess
Remember to put it inside MMDAgent-1.6.1 and edit Library_MMDAgent/src/lib/MMDAgent_util.cpp to replace:
    d = dlopen(path, RTLD_NOW);
with
    d = dlopen(path, RTLD_LAZY);

I don't know why RTLD_NOW cannot load the SubProcess plugin correctly, so I just use the LAZY approach as work around..
But after this edit, another issue regarding the PortAudio will appear, because it seems that it cannot detect the right endian, so we have to define it manually in:

    Library_PortAudio/src/src/common/pa_endianness.h

- #define PA_LITTLE_ENDIAN
- Eventually, you could make x11 and it will take a while.
- cd Plugin_SubProcess
- make -f Makefile.x11
- cd ../Release
- ls Plugins 
  to make sure you have the Plugins ready and remove the unnecessary Plugins as below:
- rm Release/Plugin_Julius.so
- rm Release/Plugin_OpenJTalk.so (since we do not use the Japanese recognition and synthesis)
- Download MMDAgent_Example and put it in the Release folder of MMDAgent-1.6.1
  wget http://sourceforge.net/projects/mmdagent/files/MMDAgent_Example/MMDAgent_Example-1.6/MMDAgent_Example-1.6.zip/download
  -  MMDAgent_Example-1.6.zip
  -  unzip MMDAgent_Example-1.6.zip
- mv -pr MMDAgent_Example-1.6/* Release
- cd Release
- ./MMDAgent MMDAgent_Example.mdf 

You will see MMDAgent if it could run correctly. You could type d to show the log info and the FPS too.
Finally, we have set up MMDAgent on RPi.

## The Alexa and Snowboy part
Before using the Alexa and Snowboy plugins for MMDAgent, I strongly suggest you try the great AlexaPi and Snowboy demo firstly, since most of the plugin implementation are based on them. In order to do recording, you also need USB microphone or audio adapter. I personally used USB web cam with microphone and you should be careful that some USB audio adapter cannot support 16K sampling rate, which is needed by Snowboy.

Download the Alexa and Snowboy plugins into Release as below:
git clone https://github.com/jianmliu/Alexa_MMDAgent
which includes mmdagent_snowboy.py, mmdagent_alexa.py and the updated MMDAgent_Example.fst script which is used to load these plugins. Meanwhile, there are some snowboy related libraries and model file too.
It should be noted that you could customize your wakeup work through the Snowboy website.
Another note is that I used a 3.5 inch SPI LCD screen in my case and I did not cover its configuration in this tutorial.
Finally, you could use Alexa or snowboy to wake it up and speak to Alexa now.

## To do list
There is still a long to do list, and some of them are:
- Develop a skill to change Alexa's clothes based on weather and temperature, maybe even mood;
- Develop a skill to dance with music;
- Add more motion responses;
- A more detailed tutorial and template regarding how to extend its functions, including how the plugin and script works etc.
- Study how to overcome the the disadvantages that AVS only supports audio steam in/out with only very limited context information available.

You are more than welcome to contribute to this project.


