RealSIDShield<br/>
Version 1.0<br/>
<br/>
<img src="https://github.com/pappavis/EasyLab-retro-synth-Commodore-64/blob/master/RealSID%20shield/Pictures/Finished%20board%20mounted.JPG" width="40%" height="40%"><br/>
Copyright (c) 2012,2013, A.T.Brask (atbrask[at]gmail[dot]com)<br/>
<br/><br/>
This is an Arduino shield that makes it easy to use a MOS Technology 6581/8580 SID chip (the famous C64 sound chip). This repository contains all necessary PCB design files as well as some photos and a bit of demonstration code. At some point I'll write a post about it on my blog at http://www.atbrask.dk/ with some further explanations and perhaps some audio/video examples.<br/>
<br/>
The design works without any big problems. There are a couple of minor issues, but I think it's good enough to release into the wild. The board basically provides the necessary support electronics for the SID chip to work and be accessible from the Arduino. So far, I have only tested it with a 8580, but it should work fine with a 6581 too. The biggest difference is the VDD voltage for the SID chip. The board includes a little step-up converter for this. Once a board is built, it can only be used with one of the two kinds of SID.<br/>
<br/>
The example code is a simple music player that plays .SID files. It consists of a Python script that emulates the Commodore 64 CPU (using the py65 package from PyPI) and an Arduino sketch that handles the SID chip.<br/>
<br/>
I did have a few left over PCBs for sale, but as of October 2015 I'm all out. If anyone is interested, they can pretty easily order new ones themselves from a PCB house using the gerber files in this repository. If any specific components are unavailable/EOL you can just swap them for similar ones. Only a few of the capacitors and resistors are more or less critical.<br/>
<br/>
---------------<br/>
IMPORTANT NOTES<br/>
---------------<br/>
<br/>
The Arduino sketch code has only been tested on an Arduino Uno. The code uses direct port access for I/O and depends on the specific mapping from the B and D ports on an ATmega168/328 to the digital pins on the Arduino board. This makes the code incompatible with Arduino boards with different port/pin mappings. One such case is the Arduino Leonardo which is currently not (yet) supported.<br/>
<br/>
!!! BUILD AT YOUR OWN RISK !!!<br/>
If you end up frying your SID chip (or any other equipment), it's not my problem. :-)<br/>
<br/>
Some of the component values depend on the model of SID you plan to use with the shield. This is very important to get right. Plugging a 8580 into a 6581 board may damage the chip. The other way around is probably less damaging, but it would simply not yield any sound. Please use an IC socket for the SID chip. It hurts to see it get soldered in place... :-)<br/>
<br/>
If you build this board, please check that the correct voltage is present on the SID chip's pin 28 (VDD) before you plug in the chip. It should read 9V for a 8580 board and 12V for a 6581 board.<br/>
<br/>
6581-specific component values:<br/>
C1 : 470pF<br/>
C2 : 470pF<br/>
R1 : 1K<br/>
R4 : 13K<br/>
R6 : 1K5<br/>
U2 : MOS 6581 :-)<br/>
<br/>
8580-specific component values:<br/>
C1 : 22nF<br/>
C2 : 22nF<br/>
R1 : Not connected<br/>
R4 : 6K2<br/>
R6 : 1K<br/>
U2 : MOS 8580 :-)<br/>
<br/>
The rest of the component values can be found in the KiCAD project files.<br/>
<br/>
------------<br/>
KNOWN ISSUES<br/>
------------<br/>
<br/>
1) There are no C6 or C7. These were added for the analog paddle inputs, but this feature was scrapped.<br/>
<br/>
2) The design specifies 560pF for C10. However, this yielded a too-low switching frequency in the step-up converter. As far as I remember, I switched this with a 220pF. The step-up converter is still noisy, but at least it doesn't have a very annoying audible tone.<br/>
<br/>
3) The output stage was copied verbatim from an old C128 schematic. However, it seems to have a large gain, which makes the output very loud.<br/>
<br/>
