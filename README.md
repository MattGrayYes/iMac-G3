# iMac G3 Resources

Collated documentation on the iMac G3, from the perspective of trying to reuse the iMac G3 CRT and peripherals, with the iMac G3 computer removed.

The [Documents folder](./Documents/) of this repository contains Apple service manuals for different versions of the iMac G3, and other useful resources.

There are two main subtypes of iMac G3, named for their type of CD Drive:

* Tray Loading iMac G3
* Slot Loading iMac G3

A lot of my understanding came from the information and links in [Rocky Hill](https://github.com/qbancoffee)'s [iMac\_G3\_IVAD\_init](https://github.com/qbancoffee/imac_g3_ivad_board_init) repository. If you want to use a slot-loading iMac G3 as a monitor, check out that repo first, as it has some PCBs that you can use to do this. They adapt the iMac's connectors into VGA + minijack + screw terminals, make it power on properly, and output EDID via the VGA.


## WARNING
* **These CRT screens run at 26,000 volts**. Twenty-six thousand.
* Even if the computer has been turned off for years, the CRT could still hold this voltage.
* **You can get shocked by the CRT directly, or any of the boards connected to it**, which may also have components or traces at this high voltage.
* Never open a device while connected to mains electricity.
* Never go anywhere near a CRT or its components unless you know what you're doing and understand the risks.
* Discharge the CRT before going anywhere near it or its components.

## Tray Loading iMac G3
* The Bondi Blue one is the original, oldest one.
	* Has an IRDA port on the left speaker.
* Other colour tray loaders are newer, and don't have IRDA.
* Has 3 or 4 flying cables to connect the computer to the CRT and chaissis peripherals.
	* Audio Cable
		* A small female Molex-style plug
		* Connections from (TBC):
			* Power Button & LED
			* Speakers
			* Audio IO ports
			* Mic
		* Plugs into the A/V Interconnect Board
	* Main Power Cable
		* A larger female Molex-style plug
		* Connections from the Power Supply Board
		* Plugs into the Power Filter Board
		* Different pinout to ATX PSUs with similar connectors
	* RGB Cable
		* Male DB-15 plug. (two rows of pins. Not three-row VGA connector)
		* Video input to the CRT
	* IrDA Cable (optional)
		* It's the DIN-looking plug
		* Connects to the IrDA Board

### RGB Cable (DB-15 CRT Video Input)
There's a flying DB-15 cable that plugs into the computer chassis.

* It's signal compatible with VGA if you make an adapter from one connector type to the other,
* It does not announce its resolution and frame rate in any manner, or speak EDID (Extended Display Identification Data)
	* You need to be able to force your computer to output one of:
		*  1024x768 @ 75Hz
		*  800x600 @ 95Hz
		*  640x480 @ 117Hz
	*  On a Mac you can use [Better Display](https://github.com/waydabber/BetterDisplay)'s Load Custom EDID feature with the attached [EDID](./iMac G3 CRT EDID.bin). (sourced from Rocky Hill's [iMac\_G3\_IVAD\_init](https://github.com/qbancoffee/imac_g3_ivad_board_init) repository.)

### DB-15 Pinout
According to Table S-3 in [Technical Note HW30](./Documents/Technical%20Note%20HW30%20-%20Sense%20Lines%20DB-15%20Video%20Connector.pdf). I've put the pins that are irrelevant here in brackets. Unconnected pins are labelled with a `.` full stop.

1. Red Ground
2. Red Video
3. *(CSync)*
4. *(Sense 0)*
5. Green Video
6. Green Ground
7. *(Sense 1)*
8. .
9. Blue Video
10. *(Sense 2)*
11. VSync Ground *(& CSync Ground)*
12. VSync
13. Blue Ground
14. HSync Ground
15. HSync

### VGA Pinout
For reference, if you want to make a VGA Adapter, here are the VGA Pins you need to connect

1. Red Video
2. Green Video
3. Blue Video
4. .
5. .
6. Red Ground
7. Green Ground
8. Blue Ground
9. .
10. Sync Ground
11. .
12. .
13. HSync
14. VSync
15. .

### Power Cable
Without the logic board, to turn on the PSU, it needs two pins connecting, and a minimum current draw on the 5V rail.

I read somewhere that without the the rest of the PSU on, the 5V trickle line is still on.

In his [Tray loading iMac G3 CRT monitor conversion](https://www.youtube.com/watch?v=hGWNIdyYnic) video, Mandrewsss works round these requirements.

* Connecting a switch between pins 23(brown) / 24(purple) on the Power connector
* Connecting a 5W 10Ω resistor on the 5V rail between pins 2(black) / 10 (red)	
	* This dissipates 2.5W as heat, so the resistor is placed by the fan.

![Resistor and switch whires on power connector](./images/Mandrewsss%20power%20close%20up.png)

![](./images/Mandrewsss%20power%20pinout.png)

## Slot Loading iMac G3

The CRT screen runs at 26,000 volts. Twenty-six thousand. The dangerous bits seem way more accessible on slot-loading iMacs than the tray-loading iMacs. Be very careful.

* The CD Drive is a thin slot in the front
* The VGA port on the back is output-only
* There are no useful cables inside to connect to the CRT.
* These models are much harder to get into, and have a thick faraday cage encasing the logic board.
* The logic board connects to the CRT and other peripherals by mounting onto molex-style connectors in in the chassis.
	* Rocky Hill's [iMac\_G3\_IVAD\_init](https://github.com/qbancoffee/imac_g3_ivad_board_init) repository has PCBs to adapt these.
* The thin dangly wire that comes through the chassis to near the RAM on the logic board leads to the antenna for the optional AirPort card. 

# Legal / Disclaimer

* "Apple" and "iMac" are registered trademarks of Apple, Inc.
* Nothing here is endorsed by Apple, Inc.
* Any hardware or software here is for development and prototyping by qualified individuals, and comes with no warranty.
* Opening an iMac or any other device with a CRT screen can expose you to tens of thousands of volts, even if it hasn't been connected to power for years. This may hurt you or worse. 