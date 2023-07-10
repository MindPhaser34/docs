# Flash xiaomi.eu ROM (macOS)

In this article, I will show you how I flashed xiaomi.eu ROM with MIUI 14 to my new device - Xiaomi Mi 13 Ultra. But I think this guide is suitable for owners of other models with Snapdragon Gen 1/2. 

## 1. Unlock bootloader

It's hardest step of whole manual, because official tool for flash ROMs properly works only on Windows OS! Latest version for macos user was released more than 2 years ago and could be found here, but it doesn't work well for new version of macOS:
https://github.com/francescotescari/XiaoMiToolV2

You could find some actual manuals from users in this thread: https://forum.xda-developers.com/t/tool-win-lin-mac-miunlocktool-unlock-bootloader-of-xiaomi-devices-on-mac-linux.3782444/post-85932539

Finally, if you cant find any solution, just run Virtual machine with Windows (virtaulbox, parallels, etc)  and use this unlocker https://en.miui.com/unlock/index.html

Wait for unlock.

#### So, before go ahead, you should do one IMPORTANT thing -  Put this song in the background! :)
https://www.youtube.com/watch?v=jC2ZY2loo74


## 2. Prepare environment

Download latest ROM version: https://sourceforge.net/projects/xiaomi-eu-multilang-miui-roms/files/xiaomi.eu/MIUI-STABLE-RELEASES/MIUIv14/

Download platform tools and unpack: https://dl.google.com/android/repository/platform-tools-latest-darwin.zip

Download latest TWRP version for device (ishtar), unpack, rename img-file to **recovery.img** and move to folder with platform tools: https://sourceforge.net/projects/recovery-for-xiaomi-devices/files/ishtar/

Enable USB debugging: 
- Settings > My Device > Detailed info & spec. Then click on 'MIUI version' 7 times to enable Developer Options.
- Go to Setting > Additional Settings > Developer options. Switch on "Developer options" and "USB debugging".

## 3. Flash recovery (TWRP)

It's very easy. Boot your device in fastboot mode:
- Turn off the Mi phone completely.
- On the switched off smartphone, press the power and volume down buttons simultaneously.
- Keep them pressed until orange text FASTBOOT appears on a black background.

 Plug in your device and go to the folder with platform tools. To be sure that your device is correctly recognized type in terminal:
```
./fastboot devices -l
```

You will see string with the model of your device. Let's flash TWRP.

```
./fastboot flash recovery_ab recovery.img
./fastboot reboot recovery
```

Then your device will boot to the new recovery.

## 4. Flash xiaomi.eu ROM

- CHeck this link if you need to change language: https://rootunroot.com/wp-content/uploads/2018/06/change-twrp-language-to-english.gif
- Clear data: Wipe > Format Data
- Mount device to OS: Mount > USB-storage
- Copy ROM: On macOS copy your zip-file with ROM to the internal storage of device via any tools like this https://www.android.com/filetransfer/
- Flash ROM: Install > Select ROM file > Install Image > Reboot (select current partition)

Profit!

## PS.
If you have any reason to restore stock recovery, you could do this:
- Download latest official ROM from here https://xiaomifirmwareupdater.com/miui/
- Unpack it and copy **recovery.img** to platform-tools folder with fastboot
- Flash it as TWRP:
```
./fastboot flash recovery_ab recovery.img
./fastboot reboot recovery
```

Done.