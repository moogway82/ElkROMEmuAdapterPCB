Electron ROM Emulator
=====================
A simple adaptor board to use a STM32 F4VE STM32F407VET6 based Development Board with [Kernel Crash's Electron ROM Emulator project](https://github.com/kernelcrash/electron-rom-emulator). Includes the analogue joystick port and Pi Tube Direct interface.

Quick Start Guide
=================
Once you've got the adaptor PCB made up, here's how to get building levels in Magic Mushrooms:

1. Program Firmware **Using a ST-Link v2 Debugger** the STM32 F4VE firmware:

    1. (see AliExpress/eBay/Amazon for cheap clones) wire up the following to the J-TAG port (the 20 pin one at a right angle on the end as follows):

    ![Connecting the STM32 F4VE board to the ST-LINKv2 Clone debugger](imgs/STM32_F4VE_to_ST-LINKv2.jpg)

    2. Ubuntu Linux:
    ```
    sudo apt install stlink
    cd [wherever the .bin file is]
    st-flash write electron-rom-emulator.bin 0x8000000
    ```

    3. Windows
    Ummm, not sure, not tried it but probably using the STM32CubeProgrammer and selecting the ST-LINK next to the connect button and loading the [electron-rom-emulator.bin](firmware/electron-rom-emulator.bin) file and select "Start Programming" from the Erasing & Programming tab.

    4. Remove ST-Link from the board
    

2. OR Program Firmware **Using a mini USB Cable**:

    1. Set BOOT0 pin to 3V3 (ie, '1') and BOOT1 to GND (ie, '0'):

    ![Setting the BOOT jumpers on the STM32 F4VE board](imgs/BOOT0-jumpers.jpg)

    2. Connect the mini USB cable (you know the USB cable that came with you webcam in 2003)

    3. Press the wee RST button in the corner

    4. Start the STM32CubeProgrammer, select USB and select a DFU from the Port selector, hit connect (may need to set the PID and VID if you have a fake, see **)

    5. Load the [electron-rom-emulator.bin](firmware/electron-rom-emulator.bin) file and select "Start Programming" from the Erasing & Programming tab.

    6. Disconnect the USB cable and remove the BOOT jumpers

2. Insert the STM32 F4VE board into the adaptor board - SD-Card slot and JTag port away from the Elk

3. Get a micro SD-Card. It's recommended to use an old, smallish (1-8 GB), slow thing.

4. Write the .img file inside [quick_start_sdcard.zip](sdcard/quick_start_sdcard.zip) - Google this as I can't go into details here - I used a Disk Manager thing on my Ubunutu Laptop. This has a BEEB.MMB file on it, the MMFS and Plus1 ROMs and *some* of the folder structure used to load ROM files to sideways RAM slots. This should get you to the Gamez quick and show you all the sweet RAM on startup! See the original project page for more detials on how to set this up and use it: [Kernel Crash's Electron ROM Emulator project](https://github.com/kernelcrash/electron-rom-emulator)

5. Stick SD Card into the slot, insert the adaptor board into the Elk and power it up.

6. Should see 160K RAM at top of the screen and Shift + Break should load up the gamez: Enjoy!

** I had a fake STM32 chip on my STM32 F4VE board, was actually a Geehy chip. But I could programm it using DFU mode, I just had to change the PID and VID to the ones my chip used. I found that in linux using the lsusb command, Windows users might be able to use Device Manager or something. 