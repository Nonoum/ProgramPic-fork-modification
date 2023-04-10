# Minimized Arduino programmer to flash PIC12F675 in 5 minutes

## Origins
The project is forked from here https://github.com/makerprojects/ProgramPic and consists from source code for Arduino and user app for Windows ( https://github.com/makerprojects/ArdPicProgHost ) for programming PIC processors.
Picked executable of the app from commit 1c9dcbe8fd1606cc00d45b58babb520a78751c89.
Picked base of Arduino programmer version 1.0, as it's vefiried to work correctly, while latest 1.9 version appears buggy.

## Howto
The sketch has minimal modifications and defines one more PWM pin (high frequency PWM) in tact with MCLR control, which is used for a voltage-doubler to not need external "high voltage" source.

Programmer requires:
- an Arduino board based on Atmega328p (maybe Atmega168p works too): refered processor registers for configuring high frequency PWM;
- two shottky diodes;
- two similar capacitors (I used ceramic in range 0.047uf ... 4.7uf : tested these two nominals as well);
- optional capacitor of 10uf ... 100uf connected to Arduino's RST pin (+ to RST, - to GND) - otherwise you would need to re-launch user app after first selection of COM port, this PREVENTS entering Arduino's bootloader, so only connect capacitor (and PIC!) after you already programmed the Arduino board itself;
- .. that's it. Connections to PIC's pins (except GND/VSS) can/SHOULD have also limiting resistors IN CASE ANYTHING IS CONNECTED WRONG to prevent damaging Arduino, you can use 1k resistors, maybe some 200ohm for VCC line (D2 pin). I didn't use resistors in examples on photo as they have very poor connection with already poor breedboard and can prevent it from working.
If PIC is detected by the app but 'erase' doesn't seem to work - check robustness of VSS/GND and VCC/D2 connections.

See arduino-pic12f675-minimal-programmer-breedboard-commented.png and arduino-pic12f675-minimal-programmer-schematics.jpg and doublecheck everything before powering Arduino with PIC connected,
if anything is connected wrong and has no resistors - it can damage Arduino.


- Launch ArdPicProgHost.exe, select COM port (expected to be the only one)
- if there's no capacitor on RST line - relaunch app and select port again
- PIC should be detected now and you'll see it in top left corner ('Device name: PIC12F675')
- press 'Erase' button and wait for it to finish (until it stops blinking)
- press 'Source File' and select a .hex file you need to program to the PIC
- press 'Write' and wait for it to finish
- done.