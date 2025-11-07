# Arduino iot webvideo
A doorbell with a camera linking to different devices will be using autodesk's hobbist circuit maker, fusion 360.

## Hardware
-Arduino Uno Wifi
-LM386(amplifer to increase the noise)
-Speaker
-12v powersupply will be attached to the arduino.
-LCD screen and button will be attached  to the arduino.
-Camera module(ov7670) will be attached and send information in Uart RX Tx. 

have on and low power mode (pwm implemintation) on will send information provided by the camera onto the cloud (IOT device) information can be viewed from any monitor that can connect to the cloud the cloud will have a user and password to it.


Extra features if time avaliable:
a sensor that will turn on and send a notification to the device

libraries would have to be installed to save time and have the video recorder to work

provided (https://github.com/indrekluuk/LiveOV7670)

https://www.youtube.com/watch?v=R94WZH8XAvM&t=325s&ab_channel=Indrek

This video will connect a little 128x160 pixal screen, I will be sending the information onto a the cloud

Autodesk Fusion will be used to create the schematic

Part two would be creating a server possibly with IoT applications help with ESP8266-01 MODULE

server should be compatibale with any device that can connect to the internet.

iot would be part of connecting and grabbing information from the internet such as the tempature, local time and brightness of day.


