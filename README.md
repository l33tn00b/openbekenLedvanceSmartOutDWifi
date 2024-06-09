# openbekenLedvanceSmartOutDWifi
Openbeken on Ledvance Outdoor Floodlight

Disclaimer: You're working with mains voltage. Only do this if you're a trained professional. 

# What?
Getting rid of that China cloud because we like local control.

# How?
The hard way. Disassembling the floodlight, unsoldering the control module, flashing it and putting the parts back together.

# Why the hard way?
Because I was stupid enough to update the firmware before deciding to uncloud it.

# Why at all?
Main motivation was being able to control the flood light locally.   
Long story: There's a location around the house where I needed some illumination and there's mains power as well as WiFi available. But no possibility for triggering the light before going there. So I needed something that would be switched remotely. ZigBee/Bluetooth coverage wasn't available, so I went for a WiFi controlled floodlight by Ledvance. Turns out these are controlled via the Tuya Cloud (China) and you'd need a separate app from Ledvance because Ledvance doesn't integrate with all the other Tuya stuff. Dooh. There's a Samsung SmartThings integration behind the scenes, though. But I don't like the Smartthings API. And it still takes the phone to activate the light. A physical button was more like what I wanted. Ok, Zigbee button, Home Automation, call Smartthings API. But: No Cloud, no lights... Sry.

# Opening Up.
Not much to see, here. The LED panel with some Low Side Switches for PWM and the Control module (wrapped in white heat shrink tube). The white goo below the control module actually is hot glue. 
Oh, the wires (grey, white) going to the LED panel do carry 230V mains voltage. 
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/48d4adc8-fb54-415b-98e4-30f677f82f51)

There's a WB2S module inside (don't mind showing the serial, here. It's not available in the Tuya cloud anymore :P))
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/44b6c8e7-0e31-4638-b894-d619216c6a8d)

# Flashing
Unsoldered the module, attached to a USB/Serial Converter with some wires. Please note: You'll need some way of manually toggling 3V3 power to the module during flashing. So make it easy by having a jumper wire.
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/80b61c00-fc81-4a1d-94b1-fc86599e0aac)

Flashing as per https://github.com/openshwprojects/OpenBK7231T_App/blob/main/FLASHING.md

# Settings
Pretty simple, there's only one PWM channel (delivered to the LED board with that two-pin connector (grey, black wires).
