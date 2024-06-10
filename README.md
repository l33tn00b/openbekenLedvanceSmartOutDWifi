# openbekenLedvanceSmartOutDWifi
Openbeken on Ledvance Outdoor Floodlight (Smart+ Wifi Flood, 50W, EAN 4058075474666, Warm White)

Disclaimer: You're working with mains voltage. Only do this if you're a trained professional. Don't flash while on mains voltage. 

# What?
Getting rid of that China cloud because we like local control.

# How?
The hard way. Disassembling the floodlight, unsoldering the control module, flashing it and putting the parts back together.

# Why the hard way?
Because I was stupid enough to update the firmware before deciding to uncloud it.

# Why at all?
Main motivation was being able to control the flood light locally.   
Long story: There's a location around the house where I needed some illumination and there's mains power as well as WiFi available. But no possibility for triggering the light before going there. So I needed something that would be switched remotely. ZigBee/Bluetooth coverage wasn't available, so I went for a WiFi controlled floodlight by Ledvance. Turns out these are controlled via the Tuya Cloud (China) and you'd need a separate app from Ledvance because Ledvance doesn't integrate with all the other Tuya stuff. Dooh. There's a Samsung SmartThings integration behind the scenes, though. But I don't like the Smartthings API. And it still takes the phone to activate the light. A physical button was more like what I wanted. Ok, Zigbee button, Home Automation, call Smartthings API. But: No Cloud, no lights... Sry.

# Required Tools  
I might have missed some.. Main requirements are given:
- USB/Serial Converter
- Jumper Wires (depending on your converter)
- 40mm heat shrink tube (approx. 15cm)
- Soldering Station
- Hot Air Gun
- Hot glue (gun)
- Knife
- Screwdriver(s)

# Opening Up.
Not much to see, here. The LED panel with some Low Side Switches for PWM and the Control module (wrapped in white heat shrink tube). The white goo below the control module actually is hot glue. 
Oh, the wires (grey, white) going to the LED panel do carry 230V mains voltage. 
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/48d4adc8-fb54-415b-98e4-30f677f82f51)

Carefully open the white heat shrink tube with a knife along the long edge...

There's a WB2S module inside (don't mind showing the serial, here. It's not available in the Tuya cloud anymore :P))
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/44b6c8e7-0e31-4638-b894-d619216c6a8d)

Slide the knife all the way along the top of the heat shrink tube. Apply moderate force to pull out the PCB.

Keep the black sheet of plastic from the PCB's bottom side.

Remove the heat shrink tube still attached to the floodlight's case. Might take more than moderate force to come off. Leave the white glue attached to the case. Discard the white heat shrink tube.

Remove silicone from the small 2-pin connector on the LED panel. Unfasten the connector. 

Unsolder the WB2S module.

# Flashing
Nice guide to flashing (for another module but basics apply all the while): https://community.home-assistant.io/t/detailed-guide-on-how-to-flash-the-new-tuya-beken-chips-with-openbk7231t/437276  
WB2S datasheet: https://developer.tuya.com/en/docs/iot/wb2s-module-datasheet?id=K9ghecl7kc47  
Unsoldered module, attached to a USB/Serial Converter with some wires. 
Please note: You'll need some way of manually toggling GND at CEN to the module during flashing. So make it easy by having a jumper wire. This is not shown in the picture below.  
Wires: 
- Brown: CEN
- Red: Vbat (3V3)
- Black: GND
- Orange: 1RX (goes to TX of USB/serial converter (at least for this converter model))
- Purple: 1TX (goes to RX of USB/serial converter (at least for this converter model))


![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/80b61c00-fc81-4a1d-94b1-fc86599e0aac)

Flashing as per https://github.com/openshwprojects/OpenBK7231T_App/blob/main/FLASHING.md

# Settings
Pretty simple, there's only one PWM channel (delivered to the LED board with that two-pin connector (grey, black wires).
Go to your newly flashed device's config page:  
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/f1131f18-09e7-477b-96fb-a4b62e602de8)  

Column Pin Settings, set pin #26 to PWM, channel of your choice. I chose 0.  
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/cd2dd773-9203-4047-bec4-a73948f29ff5)  

Save.

# Re-Assemble
Put it back together.

Re-Solder the module onto the PCB.

Put the black plastic sheet below the PCB.

Slide the PCB beginning at the side of the small PWM into a piece of 40mm heat shrink tube. Keep the plastic sheet centered below the PCB. Shrink the tube.

Carefully heat the white glue still attached to the floodlight case for approx. 10 seconds. Put the PCB wrapped in heat shrink tube into the glue. Wait some seconds. Check attachment.

Plug in small PWM connector. Fix with a drop of hot glue. 

Re-Assemble case.

# Check:
Check on the status page, light should turn on, off, dim.
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/a99d98dc-01cc-4871-ac5f-6204e59133bc)



Check on the status page, light should turn on, off, dim.
![grafik](https://github.com/l33tn00b/openbekenLedvanceSmartOutDWifi/assets/28904067/a99d98dc-01cc-4871-ac5f-6204e59133bc)

# OpenBeken Template:
```
{
  "vendor": "Tuya",
  "bDetailed": "0",
  "name": "Full Device Name Here",
  "model": "enter short model name here",
  "chip": "BK7231T",
  "board": "TODO",
  "flags": "1024",
  "keywords": [
    "TODO",
    "TODO",
    "TODO"
  ],
  "pins": {
    "26": "PWM;0"
  },
  "command": "",
  "image": "https://obrazki.elektroda.pl/YOUR_IMAGE.jpg",
  "wiki": "https://www.elektroda.com/rtvforum/topic_YOUR_TOPIC.html"
}
```




