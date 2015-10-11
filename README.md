RA8875 library [gold release]
==============================

**Wiki added!** https://github.com/sumotoy/RA8875/wiki<br>
Moved a lot of 'bla bla' in the wiki, readme cleaned.<br>

Want try 0.70b11 version? Click here https://github.com/sumotoy/RA8875/tree/0.70b11<br><br>

##### Current Version: 0.70b10(preview 2) <br>

Current beta 0.70 **tested only with**:
* EastRising RA8875 5"Inch (480x272) with resistive Touch or FT chip capacitive<br>
* EastRising RA8875 7"Inch (800x480) with FT chip capacitive<br>
* EastRising RA8875 5"Inch (800x480) with resistive Touch<br>
 All tested with Teensy 3.0, Teensy 3.1, Teensy LC, Arduino DUE, Arduino UNO, Arduino MEGA<br>
Check 'Proof of working' in wiki.<br>

##### Not Working? <br>
I have tested 0.70b6 with several CPU and <b>worked</b>:<br>
 - Teensy 3.1
 - Teensy 3.0
 - Teensy LC
 - Arduino UNO
 - Arduino NANO
 - Arduino DUE
 - Arduino MEGA
 - Arduino YUN
 Display tested:
 - EastRising RA8875 5" (480x272)
 - EastRising RA8875 5" (800x480)
 - EastRising RA8875 7" (800x480)<br>
 If your display not works, please check your connections, supply values, etc.<br>
 Remember it's an SPI connection so there's hardware limitations on some CPU, for example DUE can use as CS pin 4,10   or 52, Teensy can use more but not all, 8Bit arduino can use almost any, etc..<br>
 Still not working? Check my wiki, check carefully!<br>
 When testing, do not connect other devices on the same SPI line! This chip uses SPI mode 3 that it's not compatible
 with most stuff (check my wiki).<br>
 Are you sure you connect everything fine, settings are ok, you are using the correct CS pin, you don't have any other  SPI devices sharing the same line, the display has correct jumper set and you are sure that display it's correct supplied (and the supply it's stable, check also this!) but you still have nothing on screen?<br>
  Ok, in that case you may ask help but you need to double check that you do not make mistakes! Please understand that   I cannot spend time to fix something that it's not a library fault!!!

A couple of users tested also with:
* Adafruit RA8875 board with 7" (800x600) and 5" (480x272) displays

<b>NOTE</b>:If your do not work please ask here but remember that this is a preview to test new capabilities!<br>

##### Current version 0.70b5p1, it's the first preview of the 0.70b5! Please read!!!.<br>
**0.70b5**<br>
massive changes, lot of fixing,rendering fonts,some command changed!<br>
**0.70b6**<br>
changes in the FONT ROM code, added GT30L16U2W support, fixed an IRQ error.<br>
**0.70b7**<br>
fixed Color565 (color ordering, thanks gmartau).<br>
**0.70b8**<br>
better functions for round gauges, added 2 examples, fixed RoundGaugeBallistic examples<br>
**0.70b10**<br>
fixed PROGMEM missed template for 8bit arduino, added colorInterpolation(neat!), introduced gauges (with examples), fixed some value boudary fix to compensate RA8875 hardware limitations, added Color565ToRGB,setTextGrandient(works with all text, see examples),colorInterpolation,ringMeter(with great example),roundGaugeTicker(with example), updated basicTextFunctions example.<br>

##### Rendering Font Note [new b11!!!]
The current font rendering code it's obsolete, b11 has a brand new support that is much faster and has the font conversion application, I solved by creating a template for the application and avoided a custom version. The new font scheme it's simple than current one, use use just a font file and correctly handle PROGMEM for tiny memory CPU's (like UNO) that cannot handle big font sizes. The upcoming font rendering it's completely rebuilded from scratch and never released in any library, uses several algorithm to analyze chunks of font data for grouping and uses the accellerated graphic primitives of the RA, the result it's much faster than current one and maintain all the current features, even more the new font rendering engine it's ready for RLE compressed font (btw not in the b11, you have to wait for that) so in the near future it's possible use really large fonts.<br>
I will provide a wiki that explain how to convert your fonts step by step when b11 it's out.<br>


##### Teensy notes:
I love Teensy 3 MCU's, so every library has special features for this micro. You need to read my notes about wiring first. Some examples works only for Teensy 3.<br>

##### Description
A Fast and Optimized library for RAiO RA8875 display driver for Teensy 3.x, Teensy LC and Arduino's (and I hope for other MCU's).<br>
This is the first attemp to create a library that use all the features of this chip _from scratch_ and have nothing to share with the Adafruit_RA8875 library.<br>
As always I provide a lot of examples (check video), more coming soon...<br>

This library will work also with the Adafruit board but was mainly coded for the many TFT displays from china makers that use this chip, some are quite good and cheap, like the EastRising from buydisplay.com, much cheaper than adafruit.<br>I'm not related to EastRising or BuyDisplay, in any way, but I appreciate that I don't have to spend a little fortune for DIY stuff.<br>


####  The goals...
  - All features supported
  - 8 bit and 16 bit color depth support (done)
  - Layer support (now support large screen but only at 256 colors) (done)
  - Scalable complexity, start with basics but you can go trough... (done)
  - Support for the many external ROM Font chip (done)
  - Support for the external SPI FLASH (on develop)
  - Working with Teensy 3.x, Teensy LC, Arduino's, Energia IDE supported MCU's (stellaris, etc.)
  - Correct use of Print, Write and Println (done)
  - Correct use of setCursor to mimic LiquidCrystal library (done)
  - Compatibility with alternative SPI pinouts on Teensy 3.x,Teensy LC, this will let you use it with Audio board! (done)
  - Can use capacitive and resistive touch screen, the capacitive with gesture and max 5 concurrent touches. (done)
  - Full rotation support. (done)
  - External copyright free fonts support plus large font rendering. (done)
  - Support for Keypad Matrix. (still working on)
  - Internal support for IRQ's (done for Touch, still develop for other stuff)
  - Use of BTE (almost done)
  - A lot of examples. (done)


#### Wiring with your MCU
I support only _native SPI_.<br>
**MOSI,MISO,SCK** pins can be different between MCU's (UNO and Teensy3 uses 11,12,13) but DUE and other are different so check!)<br>
For **RST** it's your choice, it's really possible use _any_ pin. Apparently only Adafruit board need this, the 2 chinese boards I have here have internal reset circuit so it's optional, but I suggest to use it.<br>
For **CS** pin you have to choose between these pin on **Teensy3.1: 2,6,9,10,15,20,21,22,23**. Arduino UNO,MEGA and almost all 8 bit variants can use any pin, DUE can use as CS only 4,10 or 52 (please check DUE specifications)<br>
You also need another pin for **INT** used by Touch Screen (I used pin 2)<br>
From version 0.6, Energia IDE will be supported so many MCU's can be used but should wait 0.6 and since I have only Stellaris LM4F120XL I cannot be sure of the various MCU's wiring so drop me a note, at list I can add to the documentation!

#### Compatible with PJRC Audio Board! (teensy3.1 only)
Current beta has a optional Teensy instance that can use alternative SPI pinouts, this let you use Audio Board from PJRC that uses the classic SPI pinouts for RX and SD cs. You can test it with Spectrum Analyzer example that uses the Audio Board with a RA8875 TFT screen and thanks to the hardware accelleration of this chip and the use of onchip screen buffer it let you have large screen with touch capabilities with high-end audio manipulation.
see wiky:<br>
https://github.com/sumotoy/RA8875/wiki/Teensy-3.1---Working-with-PJRC-Audio-Board-with-SD-card-and-RA8875
