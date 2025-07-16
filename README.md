# fakeTec_pcb_modified

This project is forked from [gargomoma/fakeTec_pcb](https://github.com/gargomoma/fakeTec_pcb).

## Main Changes
- Added newly designed schematic and PCB using EasyEDA.
- Modified the footprint to make soldering the NRF52840 board easier.
- Changed some components.

# Pictures
<details><summary>Click to open</summary>

| Front | Back |
| :------------ | :---------------------------- |
|![image](https://github.com/pashiran/fakeTec_pcb_modified/blob/main/pics/pashiran_PCB_V1_Top.jpg) | ![image](https://github.com/pashiran/fakeTec_pcb_modified/blob/main/pics/pashiran_PCB_V1_Bottom.jpg) |

</details>

## Features
- i2c side ports ready to connect an OLED SSD1306 screen.
- Battery sensing: You can use SMD resistors or through-hole.
- 2mm mounting holes.
- Compatible with HT-RA62 / RA-01SH LoRa modules (and probably others with similar footprint).
- The variant & design is based on the DIY
<a href="https://github.com/mrekin/MeshtasticCustomBoards/tree/main/firmware/variants/diy/promicro_diy_m" target="_blank">ProMicro variant</a>.
- As MCU board its used <a href="https://github.com/joric/nrfmicro/wiki/Alternatives#supermini-nrf52840l" target="_blank">ProMicro/SuperMini</a>


## PCB Versions

| Version | Author | Description |
|--------|--------|--------|
| 1 | gargomoma | Original layout. |
| 2 | gargomoma | OledPins moved; Voltage divider resistors moved; added 2mm holes. |
| 3 | gargomoma | Bigger pads; Added 2 x pushbuttons; Access to charge boost option. |
| [4](https://github.com/gargomoma/fakeTec_pcb/issues/16) * | lupusworax | Same as v3 with 3 x smd power mosfets for swithching external hardware.| 
| [5](https://github.com/gargomoma/fakeTec_pcb/issues/24) * | ShimonHoranek | Battery protection, low profile, JST connector, dedicated battery pins.|
| [6](https://github.com/gargomoma/fakeTec_pcb/issues/26) * | ShimonHoranek | ⚠️UNTESTED⚠️ Similar to v5 + SOLAR (CN3791 MPPT).|

* The Gerber files in the repository may not be the most recent. Always verify the user's original post for updates before using a community-submitted design.

Hint: Newer versions aren't necessarily superior; when unsure use v3 or v4.

# Notes

### Bootloader
>Check if the bootloader version is >0.8, update if needed from [here](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases)
>
>Look for: "update-nice_nano_bootloader-X.X.X_nosd" where X.X.X is the version.
>
>Latest version is: [update-nice_nano_bootloader-0.9.2_nosd.uf2](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases/download/0.9.2/update-nice_nano_bootloader-0.9.2_nosd.uf2)
>
>To flash all you need to do is to connect the device via USB and double tap RST and GND pins with tweezers. After doing so you should see in your OS a USB storage device named "NICENANO". Copy/move the .uf2 file into the storage device and wait for the reboot.
>
>If you cannot do this, consider the board came without bootloader, keep reading to know how to flash it.


### My ProMicro is dead. What can i do?
##### ⚠️ALWAYS TEST THE ProMicros BEFORE SOLDERING!⚠️
>Some sellers sell the ProMicros for very very cheap, but they don't provide bootloader (so you basically got a very smol brick), no problem.

Download the .hex bootloader from [here](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases) and prepare an ESP32 with the instructions provided [here](https://github.com/atc1441/ESP32_nRF52_SWD).

Latest .hex bootloader is [nice_nano_bootloader-0.9.2_s140_6.1.1.hex](https://github.com/adafruit/Adafruit_nRF52_Bootloader/releases/download/0.9.2/nice_nano_bootloader-0.9.2_s140_6.1.1.hex).

Once you got the ESP32 board ready, solder `CLK`,`DIO`,`GND`,`VDD` (or the `3v`) to the corresponding pins on the ESP32. (The ProMicro pins are on the back of the board.)

Then:
 1. Power the ESP32 on, on your browser open swd.local (or the IP assigned)
 2. Click Init SWD (if the "Status" shows not okay, check the wiring)
 3. Erase nRF -> Ok: Everything erased (if nRF info mentions locked, erase & reset)
 4. Flash Uploaded File -> Select file (the .hex bootloader), offset = 0
 5. Flash uploaded File; Wait for the upload to complete.
 6. 🧟‍♀️IT'S ALIVEEEE🧟‍♀️
